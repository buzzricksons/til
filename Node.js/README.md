# Install
https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/setting-up-node-on-ec2-instance.html

## ec2にインストールする手順
```Shell
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
```

```Shell
. ~/.nvm/nvm.sh
```

```Shell
nvm install 6.11.5
```

```Shell
nvm install --lts
```

```Shell
node -e "console.log('Running Node.js ' + process.version)"
```

```
Running Node.js v6.11.5
```

# express
https://www.npmjs.com/package/express
```Shell
var express = require('express')
var app = express()
 
app.get('/', function (req, res) {
  res.send('Hello World')
})
 
app.listen(80)
```