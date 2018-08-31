# execute order
- @BeforeClass – Run once before any of the test methods in the class, public static void
- @AfterClass – Run once after all the tests in the class have been run, public static void
- @Before – Run before @Test, public void
- @After – Run after @Test, public void
- @Test – This is the test method to run, public void

## @Beforeと@BeforeClassの違い
- @Before：テストクラスの中でテストケース毎に実行される
- @BeforeClass：テストクラス全体として一回実行される

### 例：
```Java
public class JunitTestExample {
    private ArrayList testList;
        @BeforeClass
        public static void onceExecutedBeforeAll() {
            System.out.println("@BeforeClass: onceExecutedBeforeAll");
        }

        @Before
        public void executedBeforeEach() {
            testList = new ArrayList();
            System.out.println("@Before: executedBeforeEach");
        }

        @Test
        public void EmptyCollection() {
            assertTrue(testList.isEmpty());
            System.out.println("@Test: EmptyArrayList");
        }

        @Test
        public void OneItemCollection() {
            testList.add("oneItem");
            assertEquals(1, testList.size());
            System.out.println("@Test: OneItemArrayList");
        }
}
```

#### 結果
```
@BeforeClass: onceExecutedBeforeAll
@Before: executedBeforeEach
@Test: EmptyArrayList
@Before: executedBeforeEach
@Test: OneItemArrayList
```

# Test Order
## class
```Java
@Suite.SuiteClasses({OneTests.class, TwoTests.class})
```

## method
```Java
@FixMethodOrder(MethodSorters.JVM)
```

### ex
Junit 4.11 comes with @FixMethodOrder annotation. Instead of using custom solutions just upgrade your junit version and annotate test class with FixMethodOrder(MethodSorters.NAME_ASCENDING). Check the release notes for the details.

```Java
import org.junit.runners.MethodSorters;

import org.junit.FixMethodOrder;
import org.junit.Test;

@FixMethodOrder(MethodSorters.NAME_ASCENDING)
public class SampleTest {

    @Test
    public void firstTest() {
        System.out.println("first");
    }

    @Test
    public void secondTest() {
        System.out.println("second");
    }
}
```

# Data Provider
## Default

```Java
@DataProvider
public static Object[][] provideStringAndExpectedLength() {
    return new Object[][] {
        { "Hello World", 11 },
        { "Foo", 3 }
    };
}

@Test
@UseDataProvider( "provideStringAndExpectedLength" )
public void testCalculateLength( String input, int expectedLength ) {
    assertThat( calculateLength( input ) ).isEqualTo( expectedLength );
}
```

Edit: Since v1.7, it also supports other ways to provide data (strings, lists) and can inline the provider so that a separate method is not necessarily needed.
A full, working example can be found on the manual page on github. It also has a few more features, like collecting the providers in utility classes and accessing them from other classes etc. The manual page is very detailed, I'm sure you'll find any questions answered there.

## Using @Parameter for Field injection instead of Constructor
It is also possible to inject data values directly into fields without needing a constructor using the @Parameter annotation, like so:

```Java
import static org.junit.Assert.assertEquals;

import java.util.Arrays;
import java.util.Collection;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Parameterized;
import org.junit.runners.Parameterized.Parameter;
import org.junit.runners.Parameterized.Parameters;

@RunWith(Parameterized.class)
public class FibonacciTest {
    @Parameters
    public static Collection<Object[]> data() {
        return Arrays.asList(new Object[][] {
                 { 0, 0 }, { 1, 1 }, { 2, 1 }, { 3, 2 }, { 4, 3 }, { 5, 5 }, { 6, 8 }  
           });
    }

    @Parameter // first data value (0) is default
    public /* NOT private */ int fInput;

    @Parameter(1)
    public /* NOT private */ int fExpected;

    @Test
    public void test() {
        assertEquals(fExpected, Fibonacci.compute(fInput));
    }
}

public class Fibonacci {
    ...
}
```

This currently only works for public fields (see https://github.com/junit-team/junit/pull/737).

