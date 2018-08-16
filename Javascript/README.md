# ObjectのJSON化
```Javascript
var j={"name":"binchen"};
JSON.stringify(j); // '{"name":"binchen"}'
```

# 引数チェック
```Javascript
if (typeof variable !== 'undefined') {
    // the variable is defined
}
```

# get JSON from URL
```Javascript
$.getJSON('YourURL', function(data) {
    //data is the JSON string
});
```