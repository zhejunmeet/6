# 6
### 操作表单
HTML表单的输入控件主要有以下几种：
文本框，对应的input type="text"，用于输入文本
口令框，对应的input type="password"，用于输入口令
单选框，对应的input type="radio"，用于选择一项
复选框，对应的input type="checkbox"，用于选择多项
下拉框，对应的select，用于选择
隐藏文本，对应的input type="hidden"，用户不可见，但表单提交时会把隐藏文本发送到服务器
  
### 获取值
获得了一个<input>节点的引用，可直接调用value获得对应的用户输入值：
<input type="text" id="email">
var input = document.getElementById('email');
input.value; 
应用于text、password、hidden以及select的值，
<label><input type="radio" name="weekday" id="monday" value="1"> Monday</label>
<label><input type="radio" name="weekday" id="tuesday" value="2"> Tuesday</label>
var mon = document.getElementById('monday');
var tue = document.getElementById('tuesday');
mon.value; 
tue.value; 
mon.checked; 
tue.checked; 

### 设置值
设置值和获取值类似，对于text、password、hidden以及select，设置value就可以：
<input type="text" id="email">
var input = document.getElementById('email');
input.value = 'test@example.com';
对于单选框和复选框，设置checked为true或false

### 提交表单
一通过<form>元素的submit()方法提交这种方式的缺点是扰乱了浏览器对form的正常提交。
二是响应<form>本身的onsubmit事件，在提交form时作修改

操作文件
<input type="file">

File API
File和FileReader

### AJAX
用JavaScript执行异步网络请求
Web的运作原理：一次HTTP请求对应一个页面
让用户留在当前页面中，同时发出新的HTTP请求，用JavaScript发送这个新请求，接收到数据后再用JavaScript更新页面，仍然停留在当前页面，但是数据却可以不断地更新
写AJAX主要依靠XMLHttpRequest对象
function success(text) {
    var textarea = document.getElementById('test-response-text');
    textarea.value = text;
}

function fail(code) {
    var textarea = document.getElementById('test-response-text');
    textarea.value = 'Error code: ' + code;
}

var request = new XMLHttpRequest(); // 新建XMLHttpRequest对象

request.onreadystatechange = function () { // 状态发生变化时，函数被回调
    if (request.readyState === 4) { // 成功完成
        // 判断响应结果:
        if (request.status === 200) {
            // 成功，通过responseText拿到响应的文本:
            return success(request.responseText);
        } else {
            // 失败，根据响应码判断失败原因:
            return fail(request.status);
        }
    } else {
        // HTTP请求还在继续...
    }
}

// 发送请求:
request.open('GET', '/api/categories');
request.send();

alert('请求已发送，请等待响应...');

通过检测window对象是否有XMLHttpRequest属性来确定浏览器是否支持标准的XMLHttpRequest
XMLHttpRequest对象的open()方法有3个参数，第一个参数指定是GET还是POST，第二个参数指定URL地址，第三个参数指定是否使用异步，默认是true
调用send()方法真正发送请求。GET请求不需要参数，POST请求需要把body部分以字符串或者FormData对象传进去。
