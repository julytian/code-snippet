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
