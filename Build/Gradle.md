# change version
https://stackoverflow.com/questions/25205113/how-to-change-the-version-of-the-default-gradle-wrapper-in-intellij-idea

```Shell
./gradlew wrapper --gradle-version 2.12
```

# delete cache
```
rm -rf $HOME/.gradle/caches/
```

# custom properties
gradle.properties

```
org.gradle.daemon=true
#org.gracle.jvmargs=-Xmx4096m

org.gradle.jvmargs=-Xmx4096m -XX:MaxPermSize=1024m -XX:+HeapDumpOnOutOfMemoryError -Dfile.encoding=UTF-8
org.gradle.parallel=true
org.gradle.configureondemand=true
```