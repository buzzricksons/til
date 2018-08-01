# はじめに
JUnit 5 = JUnit Platform + JUnit Jupiter + JUnit Vintage

# @Before, @After
```text
+-------------------------------------------------------------------------------------------------------+
¦                                       Feature                            ¦   Junit 4    ¦   Junit 5   ¦
¦--------------------------------------------------------------------------+--------------+-------------¦
¦ Execute before all test methods of the class are executed.               ¦ @BeforeClass ¦ @BeforeAll  ¦
¦ Used with static method.                                                 ¦              ¦             ¦
¦ For example, This method could contain some initialization code          ¦              ¦             ¦
¦-------------------------------------------------------------------------------------------------------¦
¦ Execute after all test methods in the current class.                     ¦ @AfterClass  ¦ @AfterAll   ¦
¦ Used with static method.                                                 ¦              ¦             ¦
¦ For example, This method could contain some cleanup code.                ¦              ¦             ¦
¦-------------------------------------------------------------------------------------------------------¦
¦ Execute before each test method.                                         ¦ @Before      ¦ @BeforeEach ¦
¦ Used with non-static method.                                             ¦              ¦             ¦
¦ For example, to reinitialize some class attributes used by the methods.  ¦              ¦             ¦
¦-------------------------------------------------------------------------------------------------------¦
¦ Execute after each test method.                                          ¦ @After       ¦ @AfterEach  ¦
¦ Used with non-static method.                                             ¦              ¦             ¦
¦ For example, to roll back database modifications.                        ¦              ¦             ¦
+-------------------------------------------------------------------------------------------------------+
```

# Tag
Instead of copying and pasting @Tag("fast") throughout your code base (see Tagging and Filtering), you can create a custom composed annotation named @Fast as follows. @Fast can then be used as a drop-in replacement for @Tag("fast").
```Java
@Target({ ElementType.TYPE, ElementType.METHOD })
@Retention(RetentionPolicy.RUNTIME)
@Tag("fast")
public @interface Fast {
}
```

# TestFactory
https://github.com/junit-team/junit5/issues/1101
```Java
interface TestInterfaceDynamicTestsDemo {

    @TestFactory
    default Collection<DynamicTest> dynamicTestsFromCollection() {
        return Arrays.asList(
            dynamicTest("1st dynamic test in test interface", () -> assertTrue(true)),
            dynamicTest("2nd dynamic test in test interface", () -> assertEquals(4, 2 * 2))
        );
    }

}
```

# Conditionally Disabling Tests in JUnit 5

- Annotation

```Java
@Retention(RetentionPolicy.RUNTIME)
@ExtendWith(AssumeConnectionCondition.class)
public @interface AssumeConnection {

  String uri();

}
```

- Condition Class

```Java
public class AssumeConnectionCondition implements ExecutionCondition {

  @Override
  public ConditionEvaluationResult evaluateExecutionCondition(ExtensionContext context) {
    Optional<AssumeConnection> annotation = findAnnotation(context.getElement(), AssumeConnection.class);
    if (annotation.isPresent()) {
      String uri = annotation.get().uri();
      ConnectionChecker checker = new ConnectionChecker(uri);
      if (!checker.connect()) {
        return ConditionEvaluationResult.disabled(String.format("Could not connect to '%s'. Skipping test!", uri));
      } else {
        return ConditionEvaluationResult.enabled(String.format("Successfully connected to '%s'. Continuing test!", uri));
      }
    }
    return ConditionEvaluationResult.enabled("No AssumeConnection annotation found. Continuing test.");
  }

}
```

- Test Case

```Java
@AssumeConnection(uri = "http://my.integration.system")
public class ConnectionCheckingJunit5Test {

  @Test
  public void testOnlyWhenConnected() {
    ...
  }

}
```

# DynamicTest
 ## Using Java 8 Features
```Java
@TestFactory
Stream<DynamicTest> dynamicTestsFromStreamInJava8() {
         
    DomainNameResolver resolver = new DomainNameResolver();
         
    List<String> domainNames = Arrays.asList(
      "www.somedomain.com", "www.anotherdomain.com", "www.yetanotherdomain.com");
    List<String> outputList = Arrays.asList(
      "154.174.10.56", "211.152.104.132", "178.144.120.156");
         
    return inputList.stream()
      .map(dom -> DynamicTest.dynamicTest("Resolving: " + dom, 
        () -> {int id = inputList.indexOf(dom);
  
      assertEquals(outputList.get(id), resolver.resolveDomain(dom));
    }));       
}
```

## Demo
```Java
class DynamicTestsDemo {

    // This will result in a JUnitException!
    @TestFactory
    List<String> dynamicTestsWithInvalidReturnType() {
        return Arrays.asList("Hello");
    }

    @TestFactory
    Collection<DynamicTest> dynamicTestsFromCollection() {
        return Arrays.asList(
            dynamicTest("1st dynamic test", () -> assertTrue(true)),
            dynamicTest("2nd dynamic test", () -> assertEquals(4, 2 * 2))
        );
    }

    @TestFactory
    Iterable<DynamicTest> dynamicTestsFromIterable() {
        return Arrays.asList(
            dynamicTest("3rd dynamic test", () -> assertTrue(true)),
            dynamicTest("4th dynamic test", () -> assertEquals(4, 2 * 2))
        );
    }

    @TestFactory
    Iterator<DynamicTest> dynamicTestsFromIterator() {
        return Arrays.asList(
            dynamicTest("5th dynamic test", () -> assertTrue(true)),
            dynamicTest("6th dynamic test", () -> assertEquals(4, 2 * 2))
        ).iterator();
    }

    @TestFactory
    Stream<DynamicTest> dynamicTestsFromStream() {
        return Stream.of("A", "B", "C")
            .map(str -> dynamicTest("test" + str, () -> { /* ... */ }));
    }

    @TestFactory
    Stream<DynamicTest> dynamicTestsFromIntStream() {
        // Generates tests for the first 10 even integers.
        return IntStream.iterate(0, n -> n + 2).limit(10)
            .mapToObj(n -> dynamicTest("test" + n, () -> assertTrue(n % 2 == 0)));
    }

    @TestFactory
    Stream<DynamicTest> generateRandomNumberOfTests() {

        // Generates random positive integers between 0 and 100 until
        // a number evenly divisible by 7 is encountered.
        Iterator<Integer> inputGenerator = new Iterator<Integer>() {

            Random random = new Random();
            int current;

            @Override
            public boolean hasNext() {
                current = random.nextInt(100);
                return current % 7 != 0;
            }

            @Override
            public Integer next() {
                return current;
            }
        };

        // Generates display names like: input:5, input:37, input:85, etc.
        Function<Integer, String> displayNameGenerator = (input) -> "input:" + input;

        // Executes tests based on the current input value.
        ThrowingConsumer<Integer> testExecutor = (input) -> assertTrue(input % 7 != 0);

        // Returns a stream of dynamic tests.
        return DynamicTest.stream(inputGenerator, displayNameGenerator, testExecutor);
    }

    @TestFactory
    Stream<DynamicNode> dynamicTestsWithContainers() {
        return Stream.of("A", "B", "C")
            .map(input -> dynamicContainer("Container " + input, Stream.of(
                dynamicTest("not null", () -> assertNotNull(input)),
                dynamicContainer("properties", Stream.of(
                    dynamicTest("length > 0", () -> assertTrue(input.length() > 0)),
                    dynamicTest("not empty", () -> assertFalse(input.isEmpty()))
                ))
            )));
    }

}
```

# Parameterized Test
## dependency
- Maven
```xml
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-params</artifactId>
    <version>5.1.0</version>
    <scope>test</scope>
</dependency>
```

- Gradle
```script
testCompile(
        'org.junit.jupiter:junit-jupiter-params:5.1.0'
)

```

# Customizing Display Names
```Java
@DisplayName("Display name of container")
@ParameterizedTest(name = "{index} ==> first=''{0}'', second={1}")
@CsvSource({ "foo, 1", "bar, 2", "'baz, qux', 3" })
void testWithCustomDisplayNames(String first, int second) {
}
```
- result
```text
Display name of container ✔
├─ 1 ==> first='foo', second=1 ✔
├─ 2 ==> first='bar', second=2 ✔
└─ 3 ==> first='baz, qux', second=3 ✔
```


## Sources of Arguments

### @ValueSource
```Java
@ParameterizedTest
@ValueSource(strings = { "racecar", "radar", "able was I ere I saw elba" })
void palindromes(String candidate) {
    assertTrue(isPalindrome(candidate));
}
```

```text
palindromes(String) ✔
├─ [1] racecar ✔
├─ [2] radar ✔
└─ [3] able was I ere I saw elba ✔
```

### @EnumSource
```Java
@ParameterizedTest
@EnumSource(TimeUnit.class)
void testWithEnumSource(TimeUnit timeUnit) {
    assertNotNull(timeUnit);
}



@ParameterizedTest
@EnumSource(value = TimeUnit.class, names = { "DAYS", "HOURS" })
void testWithEnumSourceInclude(TimeUnit timeUnit) {
    assertTrue(EnumSet.of(TimeUnit.DAYS, TimeUnit.HOURS).contains(timeUnit));
}



@ParameterizedTest
@EnumSource(value = TimeUnit.class, mode = EXCLUDE, names = { "DAYS", "HOURS" })
void testWithEnumSourceExclude(TimeUnit timeUnit) {
    assertFalse(EnumSet.of(TimeUnit.DAYS, TimeUnit.HOURS).contains(timeUnit));
    assertTrue(timeUnit.name().length() > 5);
}



@ParameterizedTest
@EnumSource(value = TimeUnit.class, mode = MATCH_ALL, names = "^(M|N).+SECONDS$")
void testWithEnumSourceRegex(TimeUnit timeUnit) {
    String name = timeUnit.name();
    assertTrue(name.startsWith("M") || name.startsWith("N"));
    assertTrue(name.endsWith("SECONDS"));
}
```

### @MethodSource
```Java
@ParameterizedTest
@MethodSource("stringProvider")
void testWithSimpleMethodSource(String argument) {
    assertNotNull(argument);
}

static Stream<String> stringProvider() {
    return Stream.of("foo", "bar");
}
```

#### Multiple Parameterを利用する場合はArgumentsクラスを利用
```Java
@ParameterizedTest
@MethodSource("stringIntAndListProvider")
void testWithMultiArgMethodSource(String str, int num, List<String> list) {
    assertEquals(3, str.length());
    assertTrue(num >=1 && num <=2);
    assertEquals(2, list.size());
}

static Stream<Arguments> stringIntAndListProvider() {
    return Stream.of(
        Arguments.of("foo", 1, Arrays.asList("a", "b")),
        Arguments.of("bar", 2, Arrays.asList("x", "y"))
    );
}
```

#### 外部のstatic factory methodも利用可能
```Java
class ExternalMethodSourceDemo {

    @ParameterizedTest
    @MethodSource("example.StringsProviders#blankStrings")
    void testWithExternalMethodSource(String blankString) {
        // test with blank string
    }
}

class StringsProviders {

    static Stream<String> blankStrings() {
        return Stream.of("", " ", " \n ");
    }
}
```

### @CsvSource
```Java
@ParameterizedTest
@CsvSource({ "foo, 1", "bar, 2", "'baz, qux', 3" })
void testWithCsvSource(String first, int second) {
    assertNotNull(first);
    assertNotEquals(0, second);
}
```

| Example Input | Resulting Argument List |
| ------------- |:-------------:|
| @CsvSource({ "foo, bar" }) | "foo", "bar" |
| @CsvSource({ "foo, 'baz, qux'" }) | "foo", "baz, qux" |
| @CsvSource({ "foo, ''" }) | "foo", "" |
| @CsvSource({ "foo, " }) | "foo", null |

### @CsvFileSource
```Java
@ParameterizedTest
@CsvFileSource(resources = "/two-column.csv", numLinesToSkip = 1)
void testWithCsvFileSource(String first, int second) {
    assertNotNull(first);
    assertNotEquals(0, second);
}
```

- tow-column.csv
```text
Country, reference
Sweden, 1
Poland, 2
"United States of America", 3
```

### @ArgumentsSource
```Java
@ParameterizedTest
@ArgumentsSource(MyArgumentsProvider.class)
void testWithArgumentsSource(String argument) {
    assertNotNull(argument);
}

public class MyArgumentsProvider implements ArgumentsProvider {

    @Override
    public Stream<? extends Arguments> provideArguments(ExtensionContext context) {
        return Stream.of("foo", "bar").map(Arguments::of);
    }
}
```






