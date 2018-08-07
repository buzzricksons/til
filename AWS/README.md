# On EC2: sudo node command not found, but node without sudo is ok
```Shell
which node
```
上記のコマンドで探し、移動させる。

### ex
```
sudo ln -s /usr/local/bin/node /usr/bin/node
sudo ln -s /usr/local/lib/node /usr/lib/node
sudo ln -s /usr/local/bin/npm /usr/bin/npm
sudo ln -s /usr/local/bin/node-waf /usr/bin/node-waf
```

# その他
- BOTO 3
    - https://boto3.readthedocs.io/en/latest/
- aws cli
    - https://aws.amazon.com/jp/cli/