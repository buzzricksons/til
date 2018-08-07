# Gradle vs Maven
### Packaging
```Shell
mvn package

gradle assemble
```

### To Skip Unit Tests
```Shell
mvn install -DskipTests
#OR
mvn install -Dmaven.test.skip=true

gradle -x test install
```

### To run JUnits and create JAR/WAR/EAR
```Shell
mvn test package

gradle build
```

### To create JAR file
```Shell
mvn jar

gradle jar
#or 
gradle libs
```


