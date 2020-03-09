# dependencyが含まれたJarファイルを作成する
https://stackoverflow.com/questions/574594/how-can-i-create-an-executable-jar-with-dependencies-using-maven

### pom.xml
```Text
<build>
  <plugins>
    <plugin>
      <artifactId>maven-assembly-plugin</artifactId>
      <configuration>
        <archive>
          <manifest>
            <mainClass>fully.qualified.MainClass</mainClass>
          </manifest>
        </archive>
        <descriptorRefs>
          <descriptorRef>jar-with-dependencies</descriptorRef>
        </descriptorRefs>
      </configuration>
    </plugin>
  </plugins>
</build>
```

### maven run
```Text
mvn clean compile assembly:single
```

# Goal
### 全体buildの場合
```Text
-X -e clean install
```

### 変更された部分のみbuildの場合
```Text
-X -e clean
```

# Skip Test
### Terminalの場合
```Shell
$ mvn package -Dmaven.test.skip=true
```

### command
```Shell
$ mvn install -DskipTests
```

# Headless & Disable gpu
```Shell
$ mvn clean test -Dchromeoptions.args="--headless --disable-gpu"
```

### pomの場合
1.pomの修正
```
<properties>
    <maven.test.skip>true</maven.test.skip>
</properties>
```

2.mavenの実行
```Shell
$ mvn package
```
