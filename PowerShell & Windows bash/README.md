# Portチェック

```Shell
netstat -a -b
```

# Update

```Shell
sudo apt-get update
```

# Customize
http://windowsitpro.com/powershell/powershell-basics-console-configuration

## 手順
PowerShellは管理者権限で実行

### プロフィールの確認
```
$profile
```

### 新しいプロフィールを作成
```
New-Item -path $profile -type file -force
```

### プロフィールの編集
```
notepad $profile
```

* プロフィールの内容(例)

```
[console]::ForegroundColor = "Green"
[console]::BackgroundColor = "black"

Set-Location C:\
Clear-Host
```

### 権限の付与
```
Set-ExecutionPolicy RemoteSigned
```