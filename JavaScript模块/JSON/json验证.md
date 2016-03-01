# JSON验证

1. `try catch`  验证

```
function IsJsonString(str) {
    try {
        JSON.parse(str);
    } catch (e) {
        return false;
    }
    return true;
}
```

```
//解析json数据
function tryParseJSON (jsonString){
    try {
        var o = JSON.parse(jsonString);

        // Handle non-exception-throwing cases:
        // Neither JSON.parse(false) or JSON.parse(1234) throw errors, hence the type-checking,
        // but... JSON.parse(null) returns 'null', and typeof null === "object", 
        // so we must check for that, too.
        if (o && typeof o === "object" && o !== null) {
            return o;
        }
    }
    catch (e) { }

    return false;
};
```

2. `jQuery` + 正则表达式

```

function isJsonString (string){
    if (typeof jsonString == 'string') {
        if (! /^[\[|\{](\s|.*|\w)*[\]|\}]$/.test(jsonString)) {
            return true;
        }else{
            return false;
        }
    }
}

```

```
function isJsonString (string){

    try {
       $.parseJSON(jsonData);
    } catch (e) {
        return false;
    }
    return true;
}
```

3. 使用`JSON`库

[json2.js](https://github.com/douglascrockford/JSON-js/blob/master/json2.js)