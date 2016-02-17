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

#### 判断手机号和邮箱

```javascript
// 判断是否为邮箱地址
function isEmail(emailStr) {
    var pattern = /^(\w+\.)*\w+@\w+(\.\w+)+$/;
    return pattern.test(emailStr);
}

// 判断是否为手机号
function isMobilePhone(phone) {
    var pattern = /^(\+\d{1,4})?\d{7,11}$/;
    return pattern.test(phone);
}
```
#### 使用原生JS实现jQuery的addClass, removeClass, hasClass函数功能

```javascript
function hasClass(obj, cls) {  
    return obj.className.match(new RegExp('(\\s|^)' + cls + '(\\s|$)'));  
}  
  
function addClass(obj, cls) {  
    if (!this.hasClass(obj, cls)) obj.className += " " + cls;  
}  
  
function removeClass(obj, cls) {  
    if (hasClass(obj, cls)) {  
        var reg = new RegExp('(\\s|^)' + cls + '(\\s|$)');  
        obj.className = obj.className.replace(reg, '');  
    }  
}  
  
function toggleClass(obj,cls){  
    if(hasClass(obj,cls)){  
        removeClass(obj, cls);  
    }else{  
        addClass(obj, cls);  
    }  
}  
```
#### 绑定注册事件与移除事件

```javascript
/ 给一个element绑定一个针对event事件的响应，响应函数为listener
function addEvent(element, event, listener) {
    if (element.addEventListener) {
        element.addEventListener(event,listener);
    } else if(element.attachEvent){
        element.attachEvent("on"+event,listener);
    }
}

// 移除element对象对于event事件发生时执行listener的响应
function removeEvent(element, event, listener) {
    if (element.removeEventListenr) {
        element.removeEventListenr(event,listener);
    } else if(element.detachEvent){
        element.detachEvent("on"+event,listener);
    }
}
```

#### 事件代理

```javascript
function delegateEvent(element,tag,eventName,listener){
    addEvent(element, eventName, function(event){
        var target = event.target || event.srcElement;
        if(target.tagName.toLowerCase() == tag.toLowerCase()) {
            listener.call(target, event);
        }
    });
}
```

#### cookie获取与设置

```javascript

// 设置cookie
function setCookie(cookieName, cookieValue, expiredays) {
    var cookie = cookieName + "=" + encodeURIComponent(cookieValue);
    if (typeof expiredays === "number") {
        cookie += ";max-age=" + (expiredays * 60 * 60 * 24);
    }
    document.cookie = cookie;
}

// 获取cookie值
function getCookie(cookieName) {
    var cookie = {};
    var all = document.cookie;
    if (all==="") {
        return cookie;
    }
    var list = all.split("; ");
    for (var i = 0; i < list.length; i++) {
        var p = list[i].indexOf("=");
        var name = list[i].substr(0, p);
        var value = list[i].substr(p + 1);
        value = decodeURIComponent(value);
        cookie[name] = value;
    }
    return cookie;
}
```
#### Ajax简单封装

```javascript
function ajax(url, options) {

    var dataResult; //结果data

    // 处理data
    if (typeof(options.data) === 'object') {
        var str = '';
        for (var c in options.data) {
            str = str + c + '=' + options.data[c] + '&';
        }
        dataResult = str.substring(0, str.length - 1);
    }

    // 处理type
    options.type = options.type || 'GET';

    //获取XMLHttpRequest对象
    var xhr = window.XMLHttpRequest ? new XMLHttpRequest() : new ActiveXObject('Microsoft.XMLHTTP');

    // 发送请求
    oXhr.open(options.type, url, true);
    if (options.type == 'GET') {
        oXhr.send(null);
    } else {
        oXhr.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');
        oXhr.send(dataResult);
    }

    // readyState
    xhr.onreadystatechange = function() {
        if (xhr.readyState === 4) {
            if (xhr.status === 200) {
                if (options.onsuccess) {
                    options.onsuccess(xhr.responseText, xhr.responseXML);
                }
            } else {
                if (options.onfail) {
                    options.onfail();
                }
            }
        }
    };
}

```
