# adopt openJDK 11のインストール
https://adoptopenjdk.net/index.html?variant=openjdk11&jvmVariant=hotspotでtar.gzファイルをダウンロードする

## 1.tar.gzファイルを解凍する。
```
tar -xf OpenJDK11U-jdk_x64_mac_hotspot_11.0.1_13.tar.gz
```

## 2.解凍したファイルをJavaフォルダに移動させる
```
/Library/Java/JavaVirtualMachines/jdk-11.0.1+13
```

## 3.java PATH追加
上記のフォルダで下記を実行する
```
export PATH=$PWD/jdk-11.0.1+13/Contents/Home/bin:$PATH
```

## 4.versionの確認
```
MBP-15UAU-003:JavaVirtualMachines hyukim$ java -version
openjdk version "11.0.1" 2018-10-16
OpenJDK Runtime Environment AdoptOpenJDK (build 11.0.1+13)
OpenJDK 64-Bit Server VM AdoptOpenJDK (build 11.0.1+13, mixed mode)
```

## 5.IDEに追加する
File→Project Structureで
No.2のjdk-11.0.1+13を選択する
![](https://github.com/buzzricksons/til/blob/master/_Image/_設定まとめ/jdk11.png)

# Install OpenJDK with homebrew
```Shell
brew tap AdoptOpenJDK/openjdk
brew cask install adoptopenjdk8
```

# インストール済みJDK(JAVA_HOME)の確認
```Shell
$ /usr/libexec/java_home -V
```

# Switch Java version
```
export JAVA_8_HOME=$(/usr/libexec/java_home -v1.8)
export JAVA_9_HOME=$(/usr/libexec/java_home -v9)
export JAVA_10_HOME=$(/usr/libexec/java_home -v10)
export JAVA_11_HOME=$(/usr/libexec/java_home -v11)
export JAVA_12_HOME=$(/usr/libexec/java_home -v12)

alias java8='export JAVA_HOME=$JAVA_8_HOME'
alias java9='export JAVA_HOME=$JAVA_9_HOME'
alias java10='export JAVA_HOME=$JAVA_10_HOME'
alias java11='export JAVA_HOME=$JAVA_11_HOME'
alias java12='export JAVA_HOME=$JAVA_12_HOME'

# default to Java 12
java12
```

### example
```Shell
export OPEN_JDK_8_202_HOME=/Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk/Contents/Home
export ORACLE_JDK_8_201_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_201.jdk/Contents/Home
export ORACLE_JDK_8_73_HOME=Library/Java/JavaVirtualMachines/jdk1.8.0_73.jdk/Contents/Home


alias openjdk8_202='export JAVA_HOME=$OPEN_JDK_8_202_HOME'
alias oraclejdk8_201='export JAVA_HOME=$ORACLE_JDK_8_201_HOME'
alias oraclejdk8_73='export JAVA_HOME=$ORACLE_JDK_8_73_HOME'
```







