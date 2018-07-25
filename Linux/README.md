# SSH public key add to Remote server
```
ssh-copy-id user@remote_server
```

or

```
cat ~/.ssh/id_rsa.pub | (ssh user@host "cat >> ~/.ssh/authorized_keys")
```

# File転送
### 外からここに
```Shell
scp username@hostname:/path/to/remote/file /path/to/local/file
```

### ここから外へ
```Shell
scp /path/to/local/file username@hostname:/path/to/remote/file
```

### 外から外へ
```Shell
scp username1@hostname1:/path/to/file username2@hostname2:/path/to/other/file
```


