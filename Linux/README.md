# SSH public key add to Remote server
```
ssh-copy-id user@remote_server

or

cat ~/.ssh/id_rsa.pub | (ssh user@host "cat >> ~/.ssh/authorized_keys")
```