
njoyTeam™ Laboratory

이클립스 속도 향상 (eclipse.ini 수정)
Posted by colorweb on 2012년 4월 26일 Leave a comment (0) Go to comments

이클립스 속도 향상 (eclipse.ini 수정)

 

최근 이클립스가 버벅대서 오랜만에 이클립스 속도 향상 정보를 정리해본다.

 

eclipse.ini 수정

 

1) Before

 

 

-startup

plugins/org.eclipse.equinox.launcher_1.1.0.v20100507.jar

–launcher.library

plugins/org.eclipse.equinox.launcher.win32.win32.x86_1.1.1.R36x_v20100810

-product

org.eclipse.epp.package.jee.product

–launcher.defaultAction

openFile

–launcher.XXMaxPermSize

256M

-showsplash

org.eclipse.platform

–launcher.XXMaxPermSize

256m

–launcher.defaultAction

openFile

-vmargs

-Dosgi.requiredJavaVersion=1.5

-Xms40m

-Xmx512m

 

 

2) After

 

 

-vmargs

-Dosgi.requiredJavaVersion=1.6

-Xverify:none

-XX:+UseParallelGC

-XX:-UseConcMarkSweepGC

-XX:+AggressiveOpts  ==> 적용시 Location Type Conversion to Dalvik format failed 에러남

-XX:PermSize=128M

-XX:MaxPermSize=128M

-XX:MaxNewSize=128M

-XX:NewSize=128M

-Xms512m

-Xmx512m

 

  3) 설명

-Dosgi.requiredJavaVersion=1.6 => JDK 1.6 이상을 설치했을 경우에 1.6으로 설정하면 속도가 빨라진다.

-Xverify:none => 클래스의 유효성을 검사 생략. (시작 시간이 줄어 빨라진다.)
-XX:+UseParallelGC => 병렬 가비지 컬렉션 사용. (병렬 처리로 속도 향상)
-XX:+AggressiveOpts => 컴파일러의 소수점 최적화 기능을 작동시켜 빨라진다.
-XX:-UseConcMarkSweepGC => 병행 mark-sweep GC 수행하여 이클립스 GUI의 응답을 빠르게한다.

-XX:PermSize=128M        => Permanent Generation(영구 영역) 크기(Out Of Memory 에러시 크기 조절)

-XX:MaxPermSize=128M  => 최대 Permanent Generation 크기

-XX:NewSize=128M         => New Generation(새 영역) 크기

-XX:MaxNewSize=128M   => New Generation(새 영역) 의 최대 크기


-Xms512m : 이클립스가 사용하는 최소 Heap 메모리 1024
-Xmx512m : 이클립스가 사용하는 최대 Heap 메모리 1024
                     최소와 최대를 같은 값으로 설정하면 오르락 내리락 하지않아 빨라진다.

혹시, 오류로 이클립스가 죽는다면 설정값을 한줄씩 지우거나 숫자를 변경해서 테스트 후 사용하기바람.

[메모리 정의 예]
1 기가 이하 메모리인 컴퓨터인 경우 => -Xms256m -Xmx256m
2 기가 ~ 3 기가 메모리인 컴퓨터    => -Xms512m -Xmx512m
4기가 이상 메모리인 컴퓨터            => -Xms1024m -Xmx1024m

[ 참고 ]
JVM 은 3가지 메모리 영역을 관리합니다.
 1. Permanent(영구) 영역 : JVM 클래스와 메소드를 위한 공간. = PermSize 설정
 2. New/Young 영역 : 새로 생성된 개체들을 위한 공간. = NewSize 설정
 3. Old 영역 : 만들어진지 오래된 객체들의 공간.(New 영역에서 이동해 온다)







1.마이 ini파일세팅


-vm
C:/Program Files/Java/jdk1.8.0_66/bin/javaw.exe
-startup
plugins/org.eclipse.equinox.launcher_1.3.100.v20150511-1540.jar
--launcher.library
plugins/org.eclipse.equinox.launcher.win32.win32.x86_64_1.1.300.v20150602-1417
-product
org.eclipse.epp.package.jee.product
--launcher.defaultAction
openFile
--launcher.XXMaxPermSize
256M
-showsplash
org.eclipse.platform
--launcher.XXMaxPermSize
256m
--launcher.defaultAction
openFile
--launcher.appendVmargs
-vmargs
-Dosgi.requiredJavaVersion=1.8
-Xms6144m
-Xmx6144m
-Xverify:none
-XX:+UseParallelGC
-XX:+AggressiveOpts
-Duser.name=Luke
-Duser.language=en


2.이클립스 내부 세팅
1)General > Editors > Text Editorsの設定
以下を推奨する。

   Insert spaces for tabs を有効にする
   Show line numbers を有効にする
   Show whitespace characters を有効にする
   Show print marginを有効に、値は100（狭山の改行推奨長）にする


[編集]2)General > Appearance > Coloers and Fonts
기본은 Consolas 폰트 크기 10
各環境のバージョンにもよるが、デフォルトのフォントが非常に読みづらいものになっている場合がある。その場合、

   Basic - Text Fontを"MS ゴシック"などに変える。"@MS ゴシック"は違うので注意。


[編集]3)Java > Code Style > Formatter
   Indentation/Tab policyをSpaces onlyに。
   Line Wrapping/Maximum line lengthを120（狭山の絶対改行長）に。 
4)General > Edtors > Text Editors > Quick Diff
1.Show differences in overview ruler체크
2.Colors의 Changes는 파란색
→色合い120, 輝かさ240,明るさ120(적0녹255청255)
, Additions는 형광색으로세팅
→色合い400, 輝かさ240,明るさ120(적255,녹255,청0)
3.Use this reference source를 svn또는 git로.

5)상단 메뉴의 Toggle breadcrumb 활성화





3.플러그인

http://eclipsenotepad.sourceforge.net/updates/ 
AnyEdit
db viewer plugin
subversive - svn team provider
m2e-subversive
git
maven
Eclipse ResourceBundle Editor
spring
jadclipse








