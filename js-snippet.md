#### 深度克隆

```javascript
function clone(obj) {
        var o = obj.constructor === Array ? [] : {};
        for (var i in obj) {
            if (obj.hasOwnProperty(i)) {
                o[i] = typeof obj[i] === "object" ? clone(obj[i]) : obj[i];
            }
        }
        return o;
 }
```

#### 数组去重

```javascript
function uniqueArray(arr) {
    var newArray = [];
    for (var i = 0; i < arr.length; i++) {
        if (newArray.indexOf(arr[i]) == -1) {
            newArray.push(arr[i]);
        }
    }
    return newArray;
}
var a = [1, 3, 5, 7, 5, 3];
var b = uniqueArray(a);
console.log(b); // [1, 3, 5, 7]
```
#### trim去除空格

```javascript
function simpleTrim(str) {
    var i;
    var j;
    for (i = 0; i < str.length; i++) { //从头遍历字符串
        if (str.charAt(i) != " " && str.charAt(i) != "\t") { //当不为空的时候
            break; //跳出循环
        }
    }
    for (j = str.length - 1; j >= 0; j--) {
        if (str.charAt(j) != " " && str.charAt(j) != "\t") { //当不为空的时候
            break; //跳出循环
        }
    }
    return str.slice(i, j + 1); //返回子字符串
}

function trim(str) {
    return str.replace(/^\s+|\s+$/g, '');
}
```
