# 初期設定

## Trackpad

* 設定 → トラックパッド → タップでクリックを有効にする
* Tracking speed -> 5 from fast

## Window & Apps

設定 → ミッションコントロール → uncheck to `Automatically rearrange Spaces based on most recent use`

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

### Security & Privacy

- アクセシビリティの修正
- フルディスクアクセス修正

## Touch Barの設定

http://macnews.tistory.com/5176


## マックのbarに自分の名前を設定

http://insidemac.tistory.com/21


## プロフィール画像の変更

https://macnews.tistory.com/4202

## Finder
### Check belows

```
View -> Show Path Bar
view -> Show Status Bar
```

### vieiw extension
Finder -> Preferences -> Advanced -> Show all filename extensions


# キーボード

## Google 日本語入力をインストール

https://www.google.co.jp/ime/


## 言語変換設定(Karabiner)

https://github.com/buzzricksons/etc-korean-for-karabiner



## Function Key

- check belows
    - `USE F1, F2, etc. keys as standard function keys`
- keyboard -> shortcut -> Fn을 선택.오른쪽에 인텔리제이 추가

## Keyboard
Keychron F6 -> FN+K+C press for 3s

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
![](https://github.com/buzzricksons/til/blob/master/_Image/_%E8%A8%AD%E5%AE%9A%E3%81%BE%E3%81%A8%E3%82%81/karabiner.png?raw=true)

| From key | To key |
| ------------- |:-------------:|
| left gui | left option |
| left alt | left command |
| right alt | right command |
| application | fn |
| right shift | delete forward |
| delete forward | right shift |


### 言語変換 Shortcut

```etc
ひらがな変換: Ctrl+J
カタカナ変換: Ctrl+K
英語変換: Ctrl+L
半角変換: Ctrl+;
```


## off the correct spelling

Keyboard -> Text -> off the belows

```etc
Correct spelling automatically
Capitalize words automatically
Add period with double-space
```

## tab 有効化
Keyboard → ショートカット → すべてのコントロールにチェック(Use keyboard navigation to move focus between controls)


# Browser

## Chrome

### Add on

- Markdownhere
    - https://chrome.google.com/webstore/detail/markdown-here/elifhakcjgalahccnjkneoccemfahfoa/related?utm_source=chrome-ntp-icon

## Safari

```etc
Preference -> Advanced
```

- check `Show full website address`
- set Default encoding to `UTF-8`

### Add on

- Markdownhere
    - https://markdown-here.com/get.html

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

### tree

```Shell
$ brew install tree
```

## spectacleインストール(비추천. Rectangle사용을 추천합니다.)
https://www.spectacleapp.com/

## iterm2のインストール

https://www.iterm2.com/


### iterm customize
↓recommend

- https://beomi.github.io/2017/07/07/Beautify-ZSH/
- https://www.freecodecamp.org/news/how-to-configure-your-macos-terminal-with-zsh-like-a-pro-c0ab3f3c1156/


### ssh folder
```
chown -R YOUR_USER: ~/.ssh
chmod 700 ~/.ssh
chmod 600 ~/.ssh/*
```


### change iterm2 color

In your .bash_profile set CLICOLOR before setting TERM:

```Shell
# Set CLICOLOR if you want Ansi Colors in iTerm2
export CLICOLOR=1

# Set colors to match iTerm2 Terminal Colors
export TERM=xterm-256color
```

save bash file and source:

```Shell
source ~/.bash_profile
```

Then, in your iTerm2 Preferences > Profiles > Terminal > Report Terminal Type, set to either xterm-256color or xterm
Close iTerm2, restart it and type ls. That did the trick for me.


### 터미널 단축키
| 동작 | key |
| ------------- |:-------------:|
| 삽입점으로 위치 변경 | Option 키를 누른 상태로 포인터를 새로운 삽입점으로 이동하십시오. |
| 삽입점을 명령어 라인의 시작 부분으로 이동 | Control-A |
| 삽입점을 명령어 라인의 끝 부분으로 이동 | Control-E |
| 삽입점을 한 문자 앞으로 이동 | 오른쪽 화살표 |
| 삽입점을 한 문자 뒤로 이동 | 왼쪽 화살표 |
| 삽입점을 한 단어 앞으로 이동 | Option-오른쪽 화살표 |
| 삽입점을 한 단어 뒤로 이동 | Option-왼쪽 화살표 |
| 명령어 라인의 시작 부분까지 삭제 | Control-U |
| 명령어 라인의 끝 부분까지 삭제 | Control-K |
| 단어의 끝 부분으로 이동 | Option-D(Option을 Meta 키로 사용을 선택한 경우에만 사용 가능) |
| 단어의 시작 부분으로 이동 | Control-W |
| 1개의 문자 삭제 | Delete |
| 오른쪽 방향으로 한 문자 삭제 | 오른쪽 방향 삭제(또는 Fn-Delete 사용) |
| 두 문자의 위치를 서로 바꾸기 |  Control-T|

### 유저 이름 변경, 패스 변경
#### 패스 삭제

$ vi ~/.zshrc

```shell
add to belows at end of file
prompt_context() { 
	if [[ "$USER" != "$DEFAULT_USER" || -n "$SSH_CLIENT" ]]; then 
    	prompt_segment black default "%(!.%{%F{yellow}%}.)$USER" 
    fi 
}
```


#### 패스 삭제 & 유저이름 변경
$ vi ~/.zshrc

```shell
add to belows at end of file
prompt_context() { 
	if [[ "$USER" != "$DEFAULT_USER" || -n "$SSH_CLIENT" ]]; then 
    	prompt_segment black default "my name" 
    fi 
}
```


## NeoVimのインストール

https://neovim.io/

## sublime textのインストール

https://www.sublimetext.com/3

### 他の設定

https://github.com/buzzricksons/til/blob/master/_Setting%20%26%20Etc/Sublime%20Text.md


## clipyのインストール

https://clipy-app.com/

### setting
- Max clipboard history size to 50
- Shortcuts Main: option + dobule tap



## Rocket Fuel
https://apps.apple.com/jp/app/rocket-fuel/id1114196460?l=en&mt=12

## Go2Shellのインストール
http://macnews.tistory.com/1216

### ターミナルをiterm2に変更

```Shell
$ open -a Go2Shell --args config
```

## horo
https://apps.apple.com/us/app/horo-timer-for-menu-bar/id1437226581?mt=12

## Meld
https://meldmerge.org

## keka
https://www.keka.io/en/

## paint x
https://apps.apple.com/us/app/paint-x-paint-draw-and-edit/id668502966?mt=12

## easy find
https://www.macupdate.com/app/mac/11076/easyfind

## gas mask
https://github.com/2ndalpha/gasmask

## Disk Inventory X
불필요하게 용량 큰 파일 삭제
- http://www.derlien.com/downloads/index.html

## iStat menu
https://bjango.com/mac/istatmenus/


## firefox
## edge

## Rectangle
https://rectangleapp.com

## Input Source Pro
https://inputsource.pro



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

```Shell
sudo spctl --master-disable
```

# CPU使用率 100%を起こす

### On

1.コマンド実行

```Shell
yoda@localhost:~/Downloads$yes > /dev/null & yes > /dev/null & yes > /dev/null & yes > /dev/null & yes > /dev/null & yes > /dev/null & yes > /dev/null & yes > /dev/null &
```

2.結果

```etc
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

```etc
[1]   Terminated: 15          yes > /dev/null
[2]   Terminated: 15          yes > /dev/null
[3]   Terminated: 15          yes > /dev/null
[4]   Terminated: 15          yes > /dev/null
[5]   Terminated: 15          yes > /dev/null
[6]   Terminated: 15          yes > /dev/null
[7]-  Terminated: 15          yes > /dev/null
[8]+  Terminated: 15          yes > /dev/null
```

# Kill port
```Shell
lsof -i :3000 (where 3000 is your current port in use)
ps ax | grep <PID>
kill -QUIT <PID>
```

# Mac 노트북에서 SMC를 재설정하는 방법
1. Apple 메뉴 > 시스템 종료를 선택합니다.
2. Mac이 종료되면 내장 키보드 왼쪽에 있는 shift-control-option 키를 누르고 전원 버튼을 동시에 누릅니다.
3. 모든 키에서 손을 뗍니다.
4. 전원 버튼을 다시 눌러 Mac을 켭니다.
=======
4. 전원 버튼을 다시 눌러 Mac을 켭니다.

# Mission Control not working (Mac OS Catalina 10.15)

```
defaults write com.apple.dock mcx-expose-disabled -bool FALSE

killall Dock
```

# 영어연속입력

```
defaults write -g ApplePressAndHoldEnabled -bool false
```
