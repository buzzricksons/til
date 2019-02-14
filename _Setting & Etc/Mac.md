# 初期設定
## Trackpad 
設定 → トラックパッド → タップでクリックを有効にする

## Mission Control
設定 → ミッションコントロール → 最新の使用状況に基づいて操作スペースを自動的に並べ替えるのチェックを外す

## Dock自動最小化
ターミナルで下記を実行する

### 設定
```Shell
defaults write com.apple.dock autohide -bool true && defaults write com.apple.dock autohide-delay -float 0 && defaults write com.apple.dock autohide-time-modifier -float 0 && killall Dock
```

### 元に戻す
```Shell
defaults delete com.apple.dock autohide && defaults delete com.apple.dock autohide-delay && defaults delete com.apple.dock autohide-time-modifier && killall Dock
```

## システム環境設定
### セキュリティとプライバシー
- アクセシビリティの修正
- フルディスクアクセス修正

## Touch Barの設定
http://macnews.tistory.com/5176

## マックのbarに自分の名前を設定
http://insidemac.tistory.com/21

## プロフィール画像の変更
https://macnews.tistory.com/4202

## Finder
Check belows
```
View -> Show Path Bar
view -> Show Status Bar
```

# キーボード
まずKarabinerをインストールする

## Keyboard
### マックの標準キーボード(英語バージョン)の場合
#### Simple Modifications
| From key | To key |
| ------------- |:-------------:|
| caps lock | left control |
| left control | caps lock |

### Filco キーボードの場合
#### JISキーボード
##### Simple Modifications
| From key | To key |
| ------------- |:-------------:|
| PCキーボードのかなキー | かなキー |
| PCキーボードの無変換キー | 英数キー |
| left command | left option |
| left option | left command |
| right option | right command |

※Fキーがうまく聞かない場合、USキーボードの場合Function Keys>Use All F1, F2,...にチェック

#### US キーボード
##### Simple Modifications
| From key | To key |
| ------------- |:-------------:|
| left gui | left option |
| left alt | left command |
| right alt | right command |
| application | fn |
| right shift | delete forward |
| delete forward | right shift |

## Google 日本語入力をインストール
https://www.google.co.jp/ime/

### 言語変換 Shortcut
```
ひらがな変換: Ctrl+J
カタカナ変換: Ctrl+K
英語変換: Ctrl+L
半角変換: Ctrl+;
```

## 言語変換設定
https://github.com/buzzricksons/etc-korean-for-karabiner

## off the correct spelling
Keyboard -> Text -> off the belows
```
Correct spelling automatically
Capitalize words automatically
Add period with double-space
```

# Browser
## Chrome

## Safari
```
Preference -> Advanced
```
- check `Show full website address`
- set Default encoding to `UTF-8`

### Without CSS paste in safari
```Shell
Shift + Option + Command + v
```

### Add safari extension manually
https://georgegarside.com/blog/macos/install-any-safari-extension-macos-mojave/

# Install app
## homebrewのインストール
https://brew.sh/index_ja

### Node & npm
```Shell
brew install node
```

### gulp
```Shell
sudo npm install gulp-cli -g
```

## spectacleインストール
https://www.spectacleapp.com/

## iterm2のインストール
https://www.iterm2.com/

### change iterm2 color
In your .bash_profile set CLICOLOR before setting TERM:

```
# Set CLICOLOR if you want Ansi Colors in iTerm2 
export CLICOLOR=1

# Set colors to match iTerm2 Terminal Colors
export TERM=xterm-256color
```

save bash file and source:
```
source ~/.bash_profile
```

Then, in your iTerm2 Preferences > Profiles > Terminal > Report Terminal Type, set to either xterm-256color or xterm
Close iTerm2, restart it and type ls. That did the trick for me.

## NeoVimのインストール
https://neovim.io/

## sublime textのインストール
https://www.sublimetext.com/3

## clipyのインストール
https://clipy-app.com/

## Go2Shellのインストール
http://macnews.tistory.com/1216

### ターミナルをiterm2に変更
```Shell
$ open -a Go2Shell --args config
```

# その他
## Macのキャプチャ
http://inforati.jp/apple/mac-tips-techniques/system-hints/how-to-capture-a-specific-window-with-macos-screen-shot-function.html

## view hidden file
Finderで下記を実行する
```Shell
Shift + Command + .
```

# Mac OS 쓸모없는 파일 정리를 통한 하드 공간 확보
https://www.letmecompile.com/mac-os-%EC%93%B8%EB%AA%A8%EC%97%86%EB%8A%94-%ED%8C%8C%EC%9D%BC-%EC%A0%95%EB%A6%AC%EB%A5%BC-%ED%86%B5%ED%95%9C-%ED%95%98%EB%93%9C-%EA%B3%B5%EA%B0%84-%ED%99%95%EB%B3%B4/

# Disalbe Gatekeeper in macOS Sierra
```
sudo spctl --master-disable
```

# CPU使用率 100%を起こす
### On

1.コマンド実行
```Shell
yoda@localhost:~/Downloads$yes > /dev/null & yes > /dev/null & yes > /dev/null & yes > /dev/null & yes > /dev/null & yes > /dev/null & yes > /dev/null & yes > /dev/null &
```

2.結果
```
[1] 36964
[2] 36965
[3] 36966
[4] 36967
[5] 36968
[6] 36969
[7] 36970
[8] 36971
```

### Off
1.コマンド実行
```Shell
yoda@localhost:~/Downloads$killall yes
```

2.結果
```
[1]   Terminated: 15          yes > /dev/null
[2]   Terminated: 15          yes > /dev/null
[3]   Terminated: 15          yes > /dev/null
[4]   Terminated: 15          yes > /dev/null
[5]   Terminated: 15          yes > /dev/null
[6]   Terminated: 15          yes > /dev/null
[7]-  Terminated: 15          yes > /dev/null
[8]+  Terminated: 15          yes > /dev/null
```