在IE9+和firefox中,开始支持event.isTrusted属性,如果是用户发生的,就是true,否则就是false,并且这个属性不能被修改
```js
if(e.hasOwnProperty('originalEvent'))

if(e.hasOwnProperty('originalEvent')){
  console.log('--Probably a real click.');
 }else{
  console.log('-- Probably a fake click.');
}

if(e.which) {
  console.log('--Actually clicked--');
}else {
  console.log('---Triggered by code-')
}
```
http://stackoverflow.com/questions/6674669/in-jquery-how-can-i-tell-between-a-programmatic-and-user-click

### eval也可以将字符串解析为JSON对象
```js
var json = '{"name":"GDT","age":23,"University":"GDUT"}';
var info = eval('(' + json + ')');  //解析为JSON对象
```


```
"37"-7  -->30
"37"+7  -->377
0+"1"   -->01
"1"+"1" -->"11"
(+"1")+(+"1") -->2
+"1"+ +"1"  -->2

+null -->0
1+null-->1
!null true

Undefined用作数字时类型表现为NaN, 用作布尔时表现为false.
var a;
typeof(a) -->
"undefined"
1+a -->NaN
typeof(1+a) -->number
typeof+""  -->number"
```

Number函数 Number函数将字符串转为数值
数值：转换后还是原来的值
字符串：如果可以被解析为数值,则转换为相应的数值,否则得到NaN空字符串转为0
布尔值：true转成1,false转成0
undefined：转成NaN
null：转成0

parseInt逐个解析字符,而Number函数整体转换字符串的类型
parseInt('42 cats') // 42
Number('42 cats') // NaN

Number('\t\v\r12.34\n') // 12.34

对象的转换规则
先调用对象自身的valueOf方法  -->原始类型?
再调用对象自身的toString方法 -->原始类型?
报错
Number({a:1})// NaN

undefined  --> NaN
null       --> 0
true       --> 1
false      --> 0

String函数
数值：转为相应的字符串
字符串：转换后还是原来的值
布尔值：true转为“true”，false转为“false”
undefined：转为“undefined”
null：转为“null”

String(true) // "true"
String(undefined) // "undefined"
String(null) // "null"

先调用toString方法 -->原始类型?
调用valueOf方法    -->原始类型?
报错
String({a:1}) // "[object Object]"

[1,2,3].toString() // --> "1,2,3"
1+1+"2"  -->22
1+"2"  -->12

Boolean函数：强制转换成布尔值
转为false
undefined
null
-0
+0
NaN
''(空字符串)

所有对象的布尔值都是true
Boolean(new Boolean(false)) -->true
Boolean([]) // true
Boolean({}) // true

字符串的自动转换
主要发生在加法,当一个值为字符串，另一个值为非字符串，则后者转为字符串
```
'5' + false // "5false"
'5' + {} // "5[object Object]"
'5' + [] // "5"
'5' + function (){} // "5function (){}"
'5' + undefined // "5undefined"
'5' + null // "5null"
```

加法运算符+是双目运算符，只要其中一个是String类型，表达式的值便是一个String
对于其他的四则运算，只有其中一个是Number类型，表达式的值便是一个Number
对于非法字符的情况通常会返回NaN
```
'5' - '2' // 3
'5' * '2' // 10
true - 1  // 0
false - 1 // -1
'1' - 1   // 0
'5'*[]    // 0
false/'5' // 0
'abc'-1   // NaN
+'abc' // NaN
-'abc' // NaN
+true // 1
-false // 0
```

```
1 + [1,2] --> "11,2"
1 + {a:1} -->"1[object Object]"
{a:1} + 1  -->1  --> {a:1};+1
({a:1})+1  -->"[object Object]1"
```

空数组 + 空数组
[]+[] -->""

空数组 + 空对象
[] + {}  -->"[object Object]"  ""+{}

空对象 + 空数组
{} + []   -->0 {]视为代码块
({}) + []  -->"[object Object]"

空对象 + 空对象
{} + {} -->  "[object Object][object Object]"

两次非操作将会返回等同于变量转换成布尔值
!!a

随机字符串 [0-9a-z]（36个),截掉起始的"0."
Math.random().toString(36).substr(2);

```js
function trim(str) {
    if(str == null || typeof str == "undefined"){
        return "";
    }
    return str.replace(/(^\s*)|(\s*$)/g, "");
};
$.trim(str)
```

```js
data = data.replace(/\+/g, "%2B");
data = data.replace(/\&/g, "%26");
```

### 不缓存
```
<META HTTP-EQUIV="pragma" CONTENT="no-cache">
<META HTTP-EQUIV="Cache-Control" CONTENT="no-cache, must-revalidate">
<META HTTP-EQUIV="expires" CONTENT="0">

$.ajax({
     url:'www.haorooms.com',
     dataType:'json',
     data:{},
     cache:false,
     ifModified :true ,
     async:false,
     success:function(response){
         //操作
     }
  });

beforeSend :function(xmlHttp){
        xmlHttp.setRequestHeader("If-Modified-Since","0");
        xmlHttp.setRequestHeader("Cache-Control","no-cache");
},

在 URL 参数后加上 "?timestamp=" + new Date().getTime();
```

### ajax的缺点
1、ajax不支持浏览器back按钮
2对搜索引擎的支持比较弱

### 浏览器地址重定向

location.href = "http://www.google.com";
window.location = "http://www.google.com";
location.assign("http://www.google.com");
前面2种方式是调用第3种方式去实现的，这样就可以在浏览器中打开一个新的URL并在历史记录中生成一条记录

location.replace("http://www.google.com"); 不会在历史记录中生成记录

location.reload(true); //相当于Ctrl+F5，从服务器中加载
### json和字符串的相互转换
```js
var stringFromPerson = JSON.stringify(person);
var personFromString = JSON.parse(stringFromPerson);
```
### 避免特殊字符引起的参数错误问题
```js
data: {
    'option': 'delete',
    'name': '11&adb'
},

escape(encodeURIComponent())
```

```js
if (Array.prototype.indexOf) {
     alert("你的浏览器支持indexOf方法");
}
```

### 检查事件的触发对象和绑定对象是否一致
```js
$('.overlay').click(function(e){
  if (e.target == e.currentTarget)
    closeOverlay();
});
```

```js
var a = [];
a[0] = 1;
a['foobar'] = 2;
console.log(a.length);  1
console.log(a.foobar);  2
当一个变量被声明后，扩充其属性并不会改变原数据类型
```
查看jquery版本
```
if (typeof jQuery != 'undefined') {
  console.log(jQuery.fn.jquery);-->jQuery().jquery
}
jquery 属性返回的字符串包含 jquery 的版本号
```

```js
function setname(obj){
    obj.name = 'aaa';
    obj = new Object();
    obj.name = 'bbb';
}
var me = new Object();
setname(me);
console.log(me.name) // 'aaa'
```
当实参是引用类型的对象的时候，如果对形参重新赋值，就会不再与实参指同一个对象

setHeader("Access-Control-Allow-Origin", "*") # 允许所有域名访问

基本类型(number,string,boolean,null,undefined)是不可变

### 引用类型的比较是引用的比较

```js
var person1 = {};
var person2 = {};
console.log(person1 == person2); // false
```

### jquery阻止事件冒泡

event.stopPropagation(); 事件处理过程中，阻止了事件冒泡，但不会阻击默认行为
return false; 事件处理过程中，阻止了事件冒泡，也阻止了默认行为

event.preventDefault();  事件处理过程中，不阻击事件冒泡，但阻击默认行为

### 事件传播策略

1. 事件捕获
   事件首先交给外层的元素，然后再往内交给更具体的元素： div -> span -> a

2. 事件冒泡
   当点击 a 标签后，首先会发送到最具体的元素，在这个元素得到响应后，事件会往上冒泡到更外层的元素
   a -> span -> div

```js
$(document).on('mouseenter','#sam',function(){
    alert("hey it's sam.");
});
```

### 清空file文件

```js
function resetFileInput(file){
    file.after(file.clone().val(""));
    file.remove();
}
```

### 绑定一次的点击事件

```js
$('#killBtn').one("click",function(){ //执行方法

}) ;
```

### IE下无法获取文件的实际路径

```js
var file = $(this)[0].files[0];
var url = null;
if (window.createObjectURL != undefined) { // basic
    url = window.createObjectURL(file);
} else if (window.URL != undefined) { // mozilla(firefox)
    url = window.URL.createObjectURL(file);
} else if (window.webkitURL != undefined) { // webkit or chrome
    url = window.webkitURL.createObjectURL(file);
}
return url;
```

```js
$(".haorooms").on({
        click:function(){
                  alert("我是点击事件")
        },
        mouseover:function(){
            alert("mouseover");
        },
        mouseout:function(){
            alert("out")
        }
    })
```

```js
$(".demo").css({"height":"100px","background-color":"red"});
```

不是所有的事件都能冒泡，如：blur、focus、load、unload都不能

### 判断微信浏览器

```js
/**
 * 判断微信浏览器
 * @returns {Boolean}
 */
function isWeiXin() {
    var ua = window.navigator.userAgent.toLowerCase();
    if (ua.match(/MicroMessenger/i) == 'micromessenger') {
        return true;
    } else {
        return false;
    }
}
```
### 页面滑动到顶部
```js
$('html,body').scrollTop(0);
$('html, body').animate({ scrollTop: 0 }, 'fast');
```

```js
var str1 = str2 = "web";
(function () {
var str1 = str2 = "前端";
})();
console.log(str2); 前端 全局变量
consloe.log(str1); web 局部变量

str1 = "web";
(function () {
     var str1 = "前端";

     //str1剩下的功能
)();
console.log(str1);  web
```

```js
function stopDefault( e ) {
     // 阻止默认浏览器动作(W3C)
     if ( e && e.preventDefault ) {
         e.preventDefault();
     } else {
        // IE中阻止函数器默认动作的方式 ie8
        window.event.returnValue = false;
    }
    return false;
}
```
### js阻止页面关闭

```js
js阻止页面关闭
window.isCloseHint = true;
//初始化关闭
window.addEventListener("beforeunload", function(e) {
    if (window.isCloseHint) {
        var confirmationMessage = "要记得保存！你确定要离开我吗？";
        (e || window.event).returnValue = confirmationMessage; // 兼容 Gecko + IE
        return confirmationMessage; // 兼容 Gecko + Webkit, Safari, Chrome
    }
});
```

[].concat[1,2,3]  undefined
[].concat([1,2,3]) [1,2,3]
concat() 方法将传入的数组或非数组值与原数组合并，组成一个新的数组并返回

[].concat，这个的结果是 Array.prototype.concat执行一个逗号操作符。逗号操作符对它的每个操作对象求值（从左至右），然后返回最后一个操作对象的值 1,2,3 -->3
Array.prototype.concat[3]

Array.prototype.concat[3] = [1,2,3]
[].concat[1,2,3] 就会得到结果 [1,2,3]

```
/*
解决思路:
   增加若干个对应的闭包域空间(这里采用的是匿名函数),专门用来存储原先需要引用的内容(下标),不过只限于基本类型(基本类型值传递,对象类型引用传递)
*/
for(var i= 0;i<arr.length;i++){

   //声明一个匿名函数,若传进来的是基本类型则为值传递,故不会对实参产生影响,
   //该函数对象有一个本地私有变量arg(形参) ,该函数的 function scope 的 closure 对象属性有两个引用,一个是 arr,一个是 i
   //尽管引用 i 的值随外部改变 ,但本地私有变量(形参) arg 不会受影响,其值在一开始被调用的时候就决定了.
   (function (arg) {
       arr[i].onclick= function () { //onclick函数实例的 function scope 的 closure 对象属性有一个引用 arg,
           alert(arg);               //只要 外部空间的 arg 不变,这里的引用值当然不会改变
       }
   })(i);                             //立刻执行该匿名函数,传递下标 i(实参)
}


/*
解决思路:
   与解决办法一有点相似但却有点不太相似.
   相似点:同样是增加若干个对应的闭包域空间用来存储下标
   不同点:解决办法一是在新增的匿名闭包空间内完成事件的绑定,而此例是将事件绑定在新增的匿名函数返回的函数上

   此时绑定的函数中的 function scope 中的 closure 对象的 引用 arg 是指向将其返回的匿名函数的私有变量 arg
*/
for(var i= 0;i<arr.length;i++){
   arr[i].onclick= (function(arg){
       return function () {
           alert(arg);
       }
   })(i);
}
```

### 前端路两种实现方式

location.hash+hashchange事件
history.pushState()+popState事件

location.hash始终指向页面url 中#之后的内容
```js
function Router(){
  this.currentUrl='';
  this.routes={};
}
Router.prototype.route = function(path,callback){
  this.routes[path] = callback || function(){}
}
Router.prototype.refresh = function(){
  this.currentUrl = location.hash.slice(1) || '/';
  this.routes[this.currentUrl]();
}
Router.prototype.init = function(){
  window.addEventListener('load',this.refresh.bind(this),false);
  window.addEventListener('hashchange',this.refresh.bind(this),false);
}

var route = new Router();
route.init();
function changecolor(color){
  var body = document.getElementsByTagName('body')[0];
  body.style['background-color'] = color;
}
route.route('/',changecolor.bind(null,'skyblue'));
route.route('/blue',changecolor.bind(null,'blue'));
route.route('/green',changecolor.bind(null,'green'));
route.route('/color',function(){
  var p= document.getElementsByTagName('a');
  [].forEach.call(p,function(item){item.style['color'] = '#'+((~~(Math.random()*(1<<24))).toString(16));})
});
```
缺点就是#的存在，让一些人看了觉得不是很舒服

pushState()修改url的地址，popstate监听地址的改变，不同的是，手动的进行pushState()并不会触发popstate事件

```js
const name = 'xiaobo'
const person={
  name,
  age:16
};
console.log(person.name);//xiaobo
```

### 设置按钮不可用

```js
$("#queryBtn").attr("disabled",true);
$("#rbutton_"+i).prop("disabled",true);
```

### 判断myObj是否有定义

```js
if (typeof myObj == "undefined") {
　　　　var myObj = { };
}
```

### javascript的数据类型

字符串,数值型,boolean型,数组,对象,null型,undefined型

### 重置表单

```
$('#myform')[0].reset()
```

### 禁用 input 字段

```js
$('input[type="submit"]').prop('disabled', true);
$('input[type="submit"]').removeAttr('disabled');

checkbox
$("#saleBtn").prop("disabled",true);//禁用
$("#saleBtn").prop("disabled",false);//去除禁用

$("#saleBtn").prop("disabled","disabled");//禁用
$("#saleBtn").prop("disabled","");//去除禁用
```

自定义的DOM属性处理这些属性时,建议使用attr方法

判断前一个
if (typeof $("#div1").prev().html() != "undefined") {
​                alert("没啦");
}

```js
/**
 * 字符串替换
 * @param  {string} str    要被替换的字符串
 * @param  {string} substr 要替换的字符串
 * @param  {string} newstr 用于替换的字符串
 * @return {string}        替换后的新字符串
 */
function replace(str, substr, newstr) {
  var p = -1; // 字符出现位置
  var s = 0; // 下一次起始位置

  while((p = str.indexOf(substr, s)) > -1) {
    s = p + newstr.length; // 位置 + 值的长度
    str = str.replace(substr, newstr);
  }

  return str;
}

console.log( replace("ssssss", "ss", "s") ); // sss
```

### 延迟加载js代码

```
<script type="text/javascript" src="" id="my"></script>
<script type="text/javascript">
    setTimeout("document.getElementById('my').src='include/php100.php'; ",3000);//延时3秒
</script>
```


### == 与 === 的区别
js
==         等于
===         全等（值和类型）

```
$('#CheckBox').is(':checked')
```

```
$.ajaxSetup ({ cache: false });
```

```
$("input:checked").length
```

```
$('#newlog li:eq(3) a').css('color','red');
```

```
$("#id").is(":visible")==true
```
### javascript的同源策略

一段脚本只能读取来自于同一来源的窗口和文档的属性,这里的同一来源指的是主机名、协议和端口号的组合

$() 函数是 jQuery() 函数的别称 $() 函数用于将任何对象包裹成 jQuery 对象

ready() 函数用于在文档进入ready状态时执行代码当DOM 完全加载（例如HTML被完全解析DOM树构建完成时）
使用$(document).ready()的最大好处在于它适用于所有浏览器

$(this) 返回一个 jQuery 对象 this 代表当前元素

```js
var arr = [['a', 'aa', 'aaa'], ['b', 'bb', 'bbb'], ['c', 'cc', 'ccc']]
$.each(arr, function(i, item){
      $.each(item,function(j,val){
    　　　　 alert(j);
    　　　　alert(val);
    　});
});

return false;——跳出所有循环；相当于 javascript 中的 break 效果
return true;——跳出当前循环
```
对象字面量
```js
var obj = {};
```
构造函数
```js
var obj = new Object();
```
### 立即执行函数

使用IIFE

```js
(function(){
    //......
})()
```
### 选择器

1. 子选择器$( "parent > child" )：选取所有指定元素的直接后代元素，即子元素，可以用children()代替它。
    eg:$(“body>div”)相当于$(“body”).children(“div”);

2. 后代选择器$("ancestor descendant")：选取给定的祖先元素的所有后代元素，可以用find()代替它
    eg:$(“ul li”)相当于$(“ul”).find(“li);

3. 相邻兄弟选择器$("prev + next")：选取所有紧接在“prev”元素后的“next”元素,可以用next()替代它。
    eg :    $(“a+ul”)相当于$(“a”).next();
    相邻兄弟选择器要满足三个条件：
    1）它们必须是兄弟，即他们的父元素为同一个
    2）next必须在prev后面
    3）它们必须相邻

4. 一般兄弟选择器 $("prev ~ siblings")，选取“prev”元素之后的所有兄弟元素,可以用nextAll()代替它。
     eg : $(“a~span”)相当于$(“a”).nextAll("span");
      一般兄弟选择器两个条件：
     1.它们必须是兄弟，即他们的父元素为同一个
     2.siblings必须在prev后面

子选择器 仅是指它的直接后代 后代选择器是作用于所有子后代元素

siblings()可以跟同辈的元素匹配，无论位置的先后。
next()只能跟紧随其后的一个同辈元素匹配
nextAll()只能跟其后的同辈元素匹配
区分$(“ul.active”)和$(“ul .active”)
二者的差别在于空格，前者会被解析为“获取class为active的ul元素”，
而后者则是“获取ul元素的后代元素中class为active的元素”

$(“input”)获取的是<input>元素，
:input选取所有的<input>、<textarea>、<select>、<button>元素

