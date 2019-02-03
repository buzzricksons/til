# JDK11のインストール
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