### 深度克隆

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