# 初期設定
## 設定 → トラックパッド → タップでクリックを有効にする
## karabinerのインストール
### 共通
無し

### マックの標準キーボード(英語バージョン)の場合
#### Complex Modifications（import）
- コマンドキーを単体で押したときに、英数・かなキーを送信する。（左コマンドキーは英数、右コマンドキーはかな）（rev 2）

#### Simple Modifications
| From key | To key |
| ------------- |:-------------:|
| caps lock | right control |
| left control | caps lock |

### Filco キーボードの場合
#### Simple Modifications
| From key | To key |
| ------------- |:-------------:|
| PCキーボードのかなキー | かなキー |
| PCキーボードの無変換キー | 英数キー |
| left command | left option |
| left option | left command |
| right option | right command |

※Fキーがうまく聞かない場合、USキーボードの場合Function Keys>Use All F1, F2,...にチェック

## Google 日本語入力をインストール
https://www.google.co.jp/ime/

## マックのbarに自分の名前を設定
- http://insidemac.tistory.com/21

## Dock自動最小化
### 設定
```Shell
defaults write com.apple.dock autohide -bool true && defaults write com.apple.dock autohide-delay -float 0 && defaults write com.apple.dock autohide-time-modifier -float 0 && killall Dock
```

### 元に戻す
```Shell
defaults delete com.apple.dock autohide && defaults delete com.apple.dock autohide-delay && defaults delete com.apple.dock autohide-time-modifier && killall Dock
```

## homebrewのインストール
https://brew.sh/index_ja

## spectacleインストール
https://www.spectacleapp.com/

## iterm2のインストール
https://www.iterm2.com/

## NeoVimのインストール
https://neovim.io/

## sublime textのインストール
https://www.sublimetext.com/3

## clipyのインストール
https://clipy-app.com/

## Go2Shellのインストール
http://macnews.tistory.com/1216

## システム環境設定
### セキュリティとプライバシー
- アクセシビリティの修正
- フルディスクアクセス修正

## その他
設定 → ミッションコントロール → 最新の使用状況に基づいて操作スペースを自動的に並べ替えるのチェックを外す

# keyboardの言語変換
```
ひらがな変換: Ctrl+J
カタカナ変換: Ctrl+K
英語変換: Ctrl+L
半角変換: Ctrl+;
```

# Touch Barの設定
http://macnews.tistory.com/5176

# Macのキャプチャ
http://inforati.jp/apple/mac-tips-techniques/system-hints/how-to-capture-a-specific-window-with-macos-screen-shot-function.html

# view hidden file
```Shell
Shift + Command + .
```

# No Css paste in safari
```Shell
Shift + Option + Command + v
```

# Mac OS 쓸모없는 파일 정리를 통한 하드 공간 확보
https://www.letmecompile.com/mac-os-%EC%93%B8%EB%AA%A8%EC%97%86%EB%8A%94-%ED%8C%8C%EC%9D%BC-%EC%A0%95%EB%A6%AC%EB%A5%BC-%ED%86%B5%ED%95%9C-%ED%95%98%EB%93%9C-%EA%B3%B5%EA%B0%84-%ED%99%95%EB%B3%B4/

# Disalbe Gatekeeper in macOS Sierra
```
sudo spctl --master-disable
```

# CPU 100%
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
