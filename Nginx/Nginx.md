# error handling
```
Apr 27 15:32:27 freemarket-v2 nginx[55304]: nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
Apr 27 15:32:27 freemarket-v2 nginx[55304]: nginx: [emerg] bind() to [::]:80 failed (98: Address already in use)
Apr 27 15:32:27 freemarket-v2 nginx[55304]: nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
Apr 27 15:32:27 freemarket-v2 nginx[55304]: nginx: [emerg] bind() to [::]:80 failed (98: Address already in use)
Apr 27 15:32:28 freemarket-v2 nginx[55304]: nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
Apr 27 15:32:28 freemarket-v2 nginx[55304]: nginx: [emerg] bind() to [::]:80 failed (98: Address already in use)
Apr 27 15:32:28 freemarket-v2 nginx[55304]: nginx: [emerg] still could not bind()
Apr 27 15:32:28 freemarket-v2 systemd[1]: nginx.service: Control process exited, code=exited status=1
Apr 27 15:32:28 freemarket-v2 systemd[1]: nginx.service: Failed with result 'exit-code'.
Apr 27 15:32:28 freemarket-v2 systemd[1]: Failed to start The nginx HTTP and reverse proxy server.
```


対応
```
sudo pkill -f nginx & wait $!
sudo systemctl start nginx
```