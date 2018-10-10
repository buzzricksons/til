# 初期設定
## インストール
### 通常の場合
https://php-osx.liip.ch/

#### 5.5の場合
```Shell
curl -s https://php-osx.liip.ch/install.sh | bash -s 5.5
```

#### バージョンの確認
```Shell
/usr/local/php5/bin/php -v
```

### phpenvを利用する場合
https://qiita.com/fgnhssb/items/2263c79284c612c7d6ed

#### うまくインストールできない場合
https://qiita.com/ryoichi-u/items/43ebfe29c71bca072846

# php.iniファイルの場所
```Shell
php -i | grep "Loaded Configuration File"
```

## IntelliJの設定
### phpプラグインのインストール
### インタプリタの設定
https://qiita.com/keitakn/items/638b080a1420b401c315
1. Preferences → Languages & Frameworks → PHPからインタプリタの設定を行う。
2. PHP Language levelを7に設定し先ほどインストールした、`usr/local/php5/bin/php`を設定する。

# PHPDOC reference
http://docs.phpdoc.org/references/phpdoc/index.html

# PHP performance tips from Google
https://web.archive.org/web/20140625191431/https://developers.google.com/speed/articles/optimizing-php

# double quotes vs single quotes
### escape
```Php
echo 'This is \'test\' string';
//Output: This is 'test' string
```

### single quotes
```Php
$count = 1;
echo 'The count is $count';
//Output: The count is $count
```

### double quotes
```Php
$count = 1;
echo "The count is $count";
//Output: The count is 1
```

### equal result
```Php
$count = 1;
echo "The count is $count";
echo 'The count is ' . $count;
//両方Output: The count is 1
```

