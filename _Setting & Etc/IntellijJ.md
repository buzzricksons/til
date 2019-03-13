
# Plug In
## Git Tool Box
![](https://github.com/buzzricksons/til/blob/master/_Image/_%E8%A8%AD%E5%AE%9A%E3%81%BE%E3%81%A8%E3%82%81/gittoolbox.jpg)

https://lh4.googleusercontent.com/NwXlPvbglg97DCuUQqnIIHtQ8k4Ehyf4cahSla1o-IUtzfUojJDDJEy8u0sA_JDTIiO8-N5L_j0xCgE=w3360-h1888

Eclipseのように現在選択しているブランチ名が出て来る。

### インストール手順
1. Ctrl + Alt + SでSettingsメニューを開く
2. 左側でPluginsを選択し、右側で「Browse repositories」を押下する。
3. 出てきた検索画面で`gittoolbox`を検索しインストールする。

## Presentation Assistant
![](https://github.com/buzzricksons/til/blob/master/_Image/_%E8%A8%AD%E5%AE%9A%E3%81%BE%E3%81%A8%E3%82%81/presentation_assistant.png)
機能が実行されるたびにその機能のショートカットキーが下の部分に表示される。

###インストール手順
Ctrl + Alt + SでSettingsメニューを開く
左側でPluginsを選択し、右側で「Browse repositories」を押下する。
出てきた検索画面で`Presentation Assistant`を検索しインストールする。

## Java Stream Debugger
![](https://github.com/buzzricksons/til/blob/master/_Image/_%E8%A8%AD%E5%AE%9A%E3%81%BE%E3%81%A8%E3%82%81/RackMultipart20170524-18656-ru3a5z.png)
https://plugins.jetbrains.com/plugin/9696-java-stream-debugger

## 逆Debugプラグイン
https://www.jetbrains.com/help/idea/2017.1/debugging-with-chronon.html
https://blog.jetbrains.com/jp/2014/03/06/420

## Rainbow Brackets
https://plugins.jetbrains.com/plugin/10080-rainbow-brackets

## Grep console
https://plugins.jetbrains.com/plugin/7125-grep-console

## Markdown plugin


# ハイライトのカラーを見やすくする
http://stackoverflow.com/questions/26352197/how-to-change-usage-highlight-color-in-intellij-idea
Preferences > Editor > Color Scheme > General > 右側の Code部分を自分の好みで修正する。
修正する項目は`identifier under caret`と`identifier under caret (write)`

- identifier under caret: Backgroundを046808に変更
- identifier under caret (write): Backgroundを531314に変更

### 適用前
![](https://github.com/buzzricksons/til/blob/master/_Image/_%E8%A8%AD%E5%AE%9A%E3%81%BE%E3%81%A8%E3%82%81/before.jpg)

### 適用後
![](https://github.com/buzzricksons/til/blob/master/_Image/_%E8%A8%AD%E5%AE%9A%E3%81%BE%E3%81%A8%E3%82%81/after.jpg)

# ショートカット
| 機能名 | Mac | Window |
|:-----|:-----|:-----|
| Extend Selection | `Option` + `↑` | `Ctrl` + `W` |
| Shrink Selection | `Option` + `↓` | `Ctrl` + `Shift` + `w` |
| Column selection mode | `Shit` + `Command` + `8` | `Alt` + `Shift` + `Insert` |
| Organize imports | `Ctrl` + `Option` + `O` | `Ctrl` + `Alt` + `O` |
| remove unused import all |  | `Ctrl` + `Shift` + `Alt` + `L` |
| Go to Line | `Command` + `L` | `Ctrl` + `G` |
| Update Project | `Command` + `T` | `Ctrl` + `T` |
| View Javadoc | `F1` | `Ctrl` + `Q` |
| Scratch | | `Ctrl` + `Shift` + `Alt` + `Insert` |
| Reformat Code | `Option` + `Command` + `L` | `Ctrl` + `Alt` + `L` |
| Create file | `Ctrl` + `Option` + `N` | `Alt` + `Insert` |
| Select All Occurrence | `Ctrl` + `Option` + `G` |  |
| Start ssh seissions | `Ctrl` + `Shift` + `A` |  |
| bookmark | `F3` | ? |
| view bookmark | `Command` + `F3` | ? |
| view methods | `Command` + `F12` | ? |

# Gitの同期化エラー発生
```
Error updating changes: The Git process exited with the code -1,073,741,819 during executing git "C:\Program Files\Git\cmd\git.exe" -c core.quopath=false ls-files --exclude-standard --others-z--
```
### 対応
Using the terminal and changing your directory to your repository you can do the following (making sure you back up your repository first, just in case):
※下記の対応は解決策ではありません。自分の一時凌ぎを記述します。
1. IntelliJを終了する
2. gitフォルダがある場所に移動して下記を行う(git bashを利用) 
    ```Text
    rm .git/index
    git add .
    ```
3. IntelliJを起動する
4. 各モジュールフォルダをrevertする
5. Changelistを作り、残りのファイル(約150個)を移動させる。今後このファイルは使いません。

# frontモジュールのoverlaysフォルダのファイルがCtrl+Shift+n検索結果に出てくる場合
Project Structure -> 右側のModulesを選択 -> 右側のSourcesタブでoverlaysを選択しExcluded処理する

# Lombok
http://qiita.com/abetd/items/c586ca375fb1b9e4145a

# Repoisitory Settingを聞かれる時
```
Intellij Repository SettingでgitのＵＲＬに@などのアカウント名が入っていると、パスワードを毎回聞かれるようです。とりあえず、urlからアカウントとれば回避できるという。。。。
修正前：https://yaksaa21@bitbucket.org/yaksaa21/intellijconf-macbookpro.git
修正後：https://bitbucket.org/yaksaa21/intellijconf-macbookpro.git
```

# JDKの変更
IntellJではデフォルトでOpenJDkになっているためOracleJDKに変更するためには
```
Enter Actionから switch IDE boot JDK でJDKを変更できます。
```

# VM options
Help -> Edit Custom Vm Options
```
# custom IntelliJ IDEA VM options

-Xms2048m
-Xmx4096m
-XX:ReservedCodeCacheSize=240m
-XX:+UseCompressedOops
-Dfile.encoding=UTF-8
-XX:+UseConcMarkSweepGC
-XX:SoftRefLRUPolicyMSPerMB=50
-ea
-Dsun.io.useCanonCaches=false
-Djava.net.preferIPv4Stack=true
-Djdk.http.auth.tunneling.disabledSchemes=""
-XX:+HeapDumpOnOutOfMemoryError
-XX:-OmitStackTraceInFastThrow
-Xverify:none

-XX:ErrorFile=$USER_HOME/java_error_in_idea_%p.log
-XX:HeapDumpPath=$USER_HOME/java_error_in_idea.hprof

-Duser.name=Hyungcheol Kim
```

# Remote Host
1. Help > Find Action で「Browse Remote Host」
2. IntelliJ > Preference... の Build, Execution, Deployment > Deploymentでサーバを登録する
3. 利用するときはBrowse Remote Hostで実行

### IntelliJで開発時に、SFTPで高速なファイル同期によるディスク共有をする 
https://qiita.com/eudyptesc/items/48e27921c08966885231

# Preference
1. folderble source
2. view white space


