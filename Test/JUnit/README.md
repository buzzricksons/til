# JUnit5
### Conditionally Disabling Tests in JUnit 5
- Annotation
```
@Retention(RetentionPolicy.RUNTIME)
@ExtendWith(AssumeConnectionCondition.class)
public @interface AssumeConnection {

  String uri();

}
```

- Condition Class
```
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
```
@AssumeConnection(uri = "http://my.integration.system")
public class ConnectionCheckingJunit5Test {

  @Test
  public void testOnlyWhenConnected() {
    ...
  }

}
```