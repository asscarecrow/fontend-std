# JS

## 风格{#}
* 逗号后面要加空格

## 要点{#key}
* 对于在代码中的调试信息`console.log()`,`alert()`,调试完之后一定要把它去掉，避免在线上输出，否则会显得我们开发不够专业，不够严谨

## 注释{#note}

>As short as possible（如无必要，勿增注释）：尽量提高代码本身的清晰性、可读性。
>As long as necessary（如有必要，尽量详尽）：合理的注释、空行排版等，可以让代码更易阅读、更具美感。
单行注释

必须独占一行。`// `后跟一个空格，缩进与下一行被注释说明的代码一致。
多行注释

避免使用 `/*...*/` 这样的多行注释。有多行注释内容时，使用多个单行注释。

函数/方法注释

* 函数/方法注释必须包含函数说明，有参数和返回值时必须使用注释标识；
* 参数和返回值注释必须包含类型信息和说明；
* 当函数是内部函数，外部不可访问时，可以使用 @inner 标识；
* `if...else...`，`switch...case...`,表示代码分支的应该清楚标明此代码分支的意义


```javascript
/**
 * @param {string} p1 参数1的说明
 * @param {string} p2 参数2的说明，比较长
 *     那就换行了.
 * @param {number=} p3 参数3的说明（可选）
 * @return {Object} 返回值描述
 * 函数描述
 *
 */
function foo(p1, p2, p3) {
    var p3 = p3 || 10;
    if(p3==1){
        //表示个人
    }else(p3==2){
        //表示企业
    }else{
        //表示协会与产业园
    }
    return {
        p1: p1,
        p2: p2,
        p3: p3
    };
}
```
文件注释

文件注释用于告诉不熟悉这段代码的读者这个文件中包含哪些东西。应该提供文件的大体内容，它的作者，依赖关系和兼容性信息。如下:

```javascript
/**
 * @fileoverview 文件的描述，用途和相关信息还有依赖
 * 
 * @author 作者、作者联系方式一般留邮箱
 * Copyright 2009 Meizu Inc. All Rights Reserved. 版权信息
 */
 ```

 ## 命名{#name}

 *变量*，使用 Camel 命名法。非局部变量，声明要放在作用域头部，禁止在中间或者别的地方才声明变量

 ```javascript
 var loadingModules = {};
 ```
 *私有的* 属性、变量和方法以下划线 _ 开头。

 ```javascript
 var _privateMethod = function(){};
 ```
*常量*，使用全部字母大写，单词间下划线分隔的命名方式。

```javascript
var POST_URL = '/home/article/post';
```
*dom变量*，对于存储的dom变量以*$*开头。

```javascript
var $form = $("#regForm");
```

1. *函数*，及其*参数*使用Camel命名法。

```javascript
function stringFormat(source) {}

function hear(theBells) {}
```
2. *类*，使用 `Pascal` 命名法,其 *方法/属性*，使用 Camel 命名法
```javascript

function TextNode(value, engine) {
    this.value = value;
    this.engine = engine;
}

TextNode.prototype.clone = function () {
    return this;
};
```
3. *枚举变量*使用 `Pascal` 命名法。枚举的属性，使用全部字母大写，单词间下划线分隔的命名方式。

```javascript
var TargetState = {
    READING: 1,
    READED: 2,
    APPLIED: 3,
    READY: 4
};
```

## 命名语法{#sync}
*类名*，使用名词。

```javascript
function Engine(options) {}
```
*函数名*，使用动宾短语。

```javascript
function getStyle(element) {}
```
*boolean* 类型的变量使用 is 或 has 开头。

```javascript
var isReady = false;
var hasMoreCommands = false;
```
*Promise* 对象用动宾短语的进行时表达。

```javascript
var loadingData = ajax.get('url');
loadingData.then(callback);
```

## True 和 False 布尔表达式{#boolean}
类型检测优先使用 typeof。对象类型检测使用 instanceof。null 或 undefined 的检测使用 == null。或者!!

下面的布尔表达式都返回 false:
* null
* undefined
* '' 空字符串
* 0 数字 0

但小心下面的，可都返回 true:
* '0' 字符串 0
* [] 空数组
* {} 空对象

## 不要在 Array 上使用 for-in 循环{#array}

for-in 循环只用于 `object/map/hash` 的遍历，对 `Array` 用 for-in 循环有时会出错. 因为它并不是从 0 到 length - 1 进行遍历, 而是所有出现在对象及其原型链的键值。

```javascript
// Not recommended
function printArray(arr) {
  for (var key in arr) {
    print(arr[key]);
  }
}

printArray([0,1,2,3]);  // This works.

var a = new Array(10);
printArray(a);  // This is wrong.

a = document.getElementsByTagName('*');
printArray(a);  // This is wrong.

a = [0,1,2,3];
a.buhu = 'wine';
printArray(a);  // This is wrong again.

a = new Array;
a[3] = 3;
printArray(a);  // This is wrong again.

// Recommended
function printArray(arr) {
  var l = arr.length;
  for (var i = 0; i < l; i++) {
    print(arr[i]);
  }
}
```
## 二元和三元操作符{#operate}

### 条件 (三元) 操作符 (?:)
三元操作符用于替代 if else 条件判断语句。

```javascript
// Not recommended
if (val != 0) {
  return foo();
} else {
  return bar();
}

// Recommended
return val ? foo() : bar();
```
### && 和 ||
二元布尔操作符是可短路的，只有在必要时才会计算到最后一项。

```javascript
// Not recommended
function foo(opt_win) {
  var win;
  if (opt_win) {
    win = opt_win;
  } else {
    win = window;
  }
  // ...
}

if (node) {
  if (node.kids) {
    if (node.kids[index]) {
      foo(node.kids[index]);
    }
  }
}

// Recommended
function foo(opt_win) {
  var win = opt_win || window;
  // ...
}

var kid = node && node.kids && node.kids[index];
if (kid) {
  foo(kid);
}
```

## jquery规范 {#jquery}

### jQuery 变量
* 存放 jQuery 文档对象Dom的变量以 $ 开头；
* 将 jQuery 选择器返回的对象缓存到本地变量中复用；
* 使用驼峰命名变量；

```javascript

var $regForm = $("#regForm"),
    $subBtn = $regForm.find(".submit");
$subBtn.click(function(){...});
```
### 选择器

* 尽可能地使用 ID 选择器，因为它会调用浏览器原生方法`document.getElementById` 查找元素。当然直接使用原生`document.getElementById` 方法性能会更好；
* 在父元素中选择子元素使用 .find()方法性能会更好, 因为ID 选择器没有使用到 Sizzle 选择器引擎来查找元素；

```javascript
// Not recommended
var $productIds = $("#products .class");

// Recommended
var $productIds = $("#products").find(".class");
```

### DOM 操作

* 当要操作 DOM 元素的时候，尽量将其分离节点，操作结束后，再插入节点；
* 使用字符串连接或 array.join 要比 .append()性能更好；

```javascript
var $myList = $("#list-container > ul").detach();
//...a lot of complicated things on $myList
$myList.appendTo("#list-container");
// Not recommended
var $myList = $("#list");
for(var i = 0; i < 10000; i++){
    $myList.append("<li>"+i+"</li>");
}

// Recommended
var $myList = $("#list");
var list = "";
for(var i = 0; i < 10000; i++){
    list += "<li>"+i+"</li>";
}
$myList.html(list);

// Much to recommended
var array = [];
for(var i = 0; i < 10000; i++){
    array[i] = "<li>"+i+"</li>";
}
$myList.html(array.join(''));
```
### 事件
* 如果需要，对事件使用自定义的 namespace，这样容易解绑特定的事件，而不会影响到此 DOM 元素的其他事件监听；
* 对 Ajax 加载的 DOM 元素绑定事件时尽量使用事件委托。事件委托允许在父元素绑定事件，子代元素可以响应事件，也包括 Ajax 加载后添加的子代元素；

```javascript
$("#myLink").on("click.mySpecialClick", myEventHandler);
$("#myLink").unbind("click.mySpecialClick");
// Not recommended
$("#list a").on("click", myClickHandler);

// Recommended
$("#list").on("click", "a", myClickHandler);
```

### 链式写法
* 尽量使用链式写法而不是用变量缓存或者多次调用选择器方法；
* 当链式写法超过三次或者因为事件绑定变得复杂后，使用换行和缩进保持代码可读性；

```javascript
$("#myLink")
  .addClass("bold")
  .on("click", myClickHandler)
  .on("mouseover", myMouseOverHandler)
  .show();
```
### 性能优化
1. 避免不必要的 DOM 操作
浏览器遍历 DOM 元素的代价是昂贵的。最简单优化 DOM 树查询的方案是，当一个元素出现多次时，将它保存在一个变量中，就避免多次查询 DOM 树了。

```javascript
// Recommended
var myList = "";
var myListHTML = document.getElementById("myList").innerHTML;

for (var i = 0; i < 100; i++) {
  myList += "<span>" + i + "</span>";
}

myListHTML = myList;

// Not recommended
for (var i = 0; i < 100; i++) {
  document.getElementById("myList").innerHTML += "<span>" + i + "</span>";
}
```
2. 缓存数组长度
循环无疑是和 JavaScript 性能非常相关的一部分。通过存储数组的长度，可以有效避免每次循环重新计算。

注: 虽然现代浏览器引擎会自动优化这个过程，但是不要忘记还有旧的浏览器。

```javascript
var arr = new Array(1000),
    len, i;
// Recommended - size is calculated only 1 time and then stored
for (i = 0, len = arr.length; i < len; i++) {

}

// Not recommended - size needs to be recalculated 1000 times
for (i = 0; i < arr.length; i++) {

}
```
3. 异步加载第三方内容
当你无法保证嵌入第三方内容比如 Youtube 视频或者一个 like/tweet 按钮可以正常工作的时候，你需要考虑用异步加载这些代码，避免阻塞整个页面加载。

```javascript
(function() {

    var script,
        scripts = document.getElementsByTagName('script')[0];

    function load(url) {
      script = document.createElement('script');
      script.async = true;
      script.src = url;
      scripts.parentNode.insertBefore(script, scripts);
    }

    load('//apis.google.com/js/plusone.js');
    load('//platform.twitter.com/widgets.js');
    load('//s.widgetsite.com/widget.js');

}());
```
4. 避免使用 jQuery 实现动画

* 简单的动画可以用css代替
* 复杂点的动画可以使用javascript 动画库[Velocityjs](http://velocityjs.org/)、[Gsap](https://greensock.com/gsap)
* 禁止使用 slideUp/Down() fadeIn/fadeOut()等方法；
* 尽量不使用 animate()方法；


### 杂项
* 多个参数使用对象字面量存储；
* 不要将 CSS 写在 jQuery 里面；


*福利* jQuery plug template

```javascript
// jQuery Plugin Boilerplate
// A boilerplate for jumpstarting jQuery plugins development
// version 1.1, May 14th, 2011
// by Stefan Gabos

// remember to change every instance of "pluginName" to the name of your plugin!
(function($) {

    // here we go!
    $.pluginName = function(element, options) {

        // plugin's default options
        // this is private property and is  accessible only from inside the plugin
        var defaults = {

            foo: 'bar',

            // if your plugin is event-driven, you may provide callback capabilities
            // for its events. execute these functions before or after events of your
            // plugin, so that users may customize those particular events without
            // changing the plugin's code
            onFoo: function() {}

        }

        // to avoid confusions, use "plugin" to reference the
        // current instance of the object
        var plugin = this;

        // this will hold the merged default, and user-provided options
        // plugin's properties will be available through this object like:
        // plugin.settings.propertyName from inside the plugin or
        // element.data('pluginName').settings.propertyName from outside the plugin,
        // where "element" is the element the plugin is attached to;
        plugin.settings = {}

        var $element = $(element), // reference to the jQuery version of DOM element
             element = element;    // reference to the actual DOM element

        // the "constructor" method that gets called when the object is created
        plugin.init = function() {

            // the plugin's final properties are the merged default and
            // user-provided options (if any)
            plugin.settings = $.extend({}, defaults, options);

            // code goes here

        }

        // public methods
        // these methods can be called like:
        // plugin.methodName(arg1, arg2, ... argn) from inside the plugin or
        // element.data('pluginName').publicMethod(arg1, arg2, ... argn) from outside
        // the plugin, where "element" is the element the plugin is attached to;

        // a public method. for demonstration purposes only - remove it!
        plugin.foo_public_method = function() {

            // code goes here

        }

        // private methods
        // these methods can be called only from inside the plugin like:
        // methodName(arg1, arg2, ... argn)

        // a private method. for demonstration purposes only - remove it!
        var foo_private_method = function() {

            // code goes here

        }

        // fire up the plugin!
        // call the "constructor" method
        plugin.init();

    }

    // add the plugin to the jQuery.fn object
    $.fn.pluginName = function(options) {

        // iterate through the DOM elements we are attaching the plugin to
        return this.each(function() {

            // if plugin has not already been attached to the element
            if (undefined == $(this).data('pluginName')) {

                // create a new instance of the plugin
                // pass the DOM element and the user-provided options as arguments
                var plugin = new $.pluginName(this, options);

                // in the jQuery version of the element
                // store a reference to the plugin object
                // you can later access the plugin and its methods and properties like
                // element.data('pluginName').publicMethod(arg1, arg2, ... argn) or
                // element.data('pluginName').settings.propertyName
                $(this).data('pluginName', plugin);

            }

        });

    }

})(jQuery);
```
此 jQuery 插件模板出自：[jQuery Plugin Boilerplate, revisited](http://stefangabos.ro/jquery/jquery-plugin-boilerplate-revisited/)。




