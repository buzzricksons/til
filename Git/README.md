
# 既存のソースをgitに上げる
```Text
cd プロジェクト
git init
git remote add origin  https://hyungcheol_kim@bitbucket.org/****/*******.git
git add .
git commit -m "Initial commit"
git push -u origin master
```

# 特定のBranchのみcloneする
`git clone -b ブランチ名 --single-branch gitアドレス`
```Shell
$ git clone -b luke-branch --single-branch https://XXX.XXX.git
```

# autoCRLFをfalseにする方法
```Shell
git config --global core.autoCRLF false
```

## 設定ファイルの確認
`\Users\ユーザー名` 配下の「.gitconfig」を開く
```
[user]
    name = hoge
    email = hogehoge@seeds-std.co.jp
[core]
    preloadindex = true
    autoCRLF = false
```

# 既存のフォルダをgit repositoryにpushする方法
```
git init gitレポジトリのアドレス
git init
git add .
git commit -m 'first commit.'
git config --global user.email "luke@test.test"
git config --global user.name "shared-auto"
git remote add origin gitレポジトリのアドレス
git push origin master
```

# diff
## 特定の拡張子のみ検知する
```Text
git diff --name-only <前回のrevision番号>  <今回のrevision番号> -- '*.txt' '*.sql'
```

### 例
```
$ git diff --name-only b2332226c4801883af506ed1fbfe2227959a7d20  5fc3d158df668469e5a158456447b71ad5494038 -- '*.txt' '*.sql'
yoda-module-main/src/main/config/yoda_conf/data_download/yoda_item.txt
yoda-module-main/src/main/config/yoda_conf/support/yoda_entity_postgresql.sql
yoda-module-main/src/main/config/yoda_conf/support/yoda_entity_postgresql.sql
```

## 特定のフォルダのみ検知する
```Text
git diff --name-only <前回のrevision番号> <今回のrevision番号> --relative=フォルダpath
```

### 例
```
$ git diff --name-only 0097fae10ec91dae7b6ce62f8d836a480e3f32dc 85225d56b43e56f16826fa15c9f23837439228d7 --relative=yoda/meta/src/main/resources/
config/language/yoda/label/yoda-txt-point-YodaGrantPolicy$Label.properties
config/language/yoda/message/message.properties
config/language/yoda/validation/validation_yoda.properties
config/rule/yoda_rule.properties
config/regulation.properties
ddl/yoda_entity_postgresql.sql
```

# whatchanged
2017年1月14日から2月1日までに変更されたファイルを以下のような一覧で取得する。
- ファイル一覧をソートして、重複は除外する
- ファイル名に「sql」または「meta」を含むファイルを絞り込む

```Text
git whatchanged --since '01/14/2017' --until '02/01/2017' --oneline --name-only --pretty=format: | sort | uniq | grep -e sql -e meta
```

# Setting your email address for every repository on your computer
### 確認
```Text
$ git config --global user.email
```

### 設定
```Text
$ git config --global user.email "email@example.com"
```

# 認証を保存する
```
git config credential.helper store
```

# エラー
## fatal: The remote end hung up unexpectedly
pushする時
```Text
fatal: The remote end hung up unexpectedly
```
というメッセージが出てくる場合
```Text
git config http.postBuffer 524288000
```
を実行する
