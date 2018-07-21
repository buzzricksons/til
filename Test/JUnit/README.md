# JUnit5
### Conditionally Disabling Tests in JUnit 5
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

# DynamicTest using Java 8 Features
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