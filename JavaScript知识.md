JavaScript是一门跨平台、面向对象的脚本语言，来控制网页行为的，它能使网页可交互
# JS引入方式
1. 内部脚本：将JS代码定义在HTML页面中
在HTML中，JavaScript代码必须位于`<script>`与`<script>`标签之间
```html
<script>
    alert("hello JS~");
</script>
```
提示:
在html文档中可以在任意地方，放置任意数量的`<script>`
一般把脚本置于`<body>`元素的底部，可改善显示速度，因为脚本执行会拖慢显示
2. 外部脚本：将JS代码定义在外部JS文件中，然后引入到HTML页面中
外部文件:demo.js `alert("hello JS~");`
引入外部js文件 `<script src="../js/demo.js"></script>`
注意：1.外部脚本不能包含`<script>`标签.
2.`<script>`标签不能自闭合
# JS基础语法
### 书写语法
1. 区分大小写
2. 每行结尾的分号可有可无
3. 注释
    - 单行注释：//注释内容
    - 多行注释：/\*注释内容*/
4. 大括号表示代码块
### 输出语句
- 使用window.alert()写入警告框
- 使用document.write()写入HTML输出
- 使用console.log()写入浏览器控制台
### 变量
- JavaScript中用var关键字来声明变量（作用域：全局变量。变量可以重复定义。）
- 变量名的组成字符可以是任何字母、数字、下划线或美元符；数字不能作为开头；建议使用驼峰命名。
- ECMAScript6新增了**let**关键字来定义变量。它的用法类似于var，但是所声明的变量，只在let关键字所在的代码块内有效，且不允许重复声明。
- ECMAScript6新增了**const**关键字，用来声明一个只读的常量。一旦声明，常量的值就不能改变。
### 数据类型
JavaScript中分为：原始类型和引用类型
5中原始类型：
- number：数字（整数，小数，NaN）
- string：字符，字符串，单双引皆可
- boolean：布尔。true，false
- null：对象为空
- undefined：当声明的变量未初始化时，该变量的默认值是undefined

使用typeof运算符可以获取数据类型`alert(typeof age);`
### 运算符(和java很相似，除了全等于号)
- 一元运算符：++，--
- 二元运算符：+，-，*，/，%
- 赋值运算符：=，+=，-=
- 关系运算符：>,<,>=,<=,!=,\==,===
==：1.判断类型是否一样，如果不一样，则进行类型转换。2.再去比较其值
===：1.判断类型是否一样，如果不一样，直接返回false。2.再去比较其值
- 逻辑运算符：&&，||，!
- 三元运算符：条件表达式? true_value:false_value
- 类型转换：
    - 其他类型转为number：
        1. string：按照字符串的字面值，转为数字。如果字面值不是数字，则转为NaN。一般使用parseInt
        `var str = +"20";`
        `parseInt("20")`
        2. boolean：true转为1，false转为0
        `var str = +false`
    - 其他类型转为boolean：
        1. number：0和NaN转为false，其他的数字转为true
        2. string：空字符串转为false，其他的字符串转为true
        3. null：false
        4. undefined：false
### 流程控制语句（和Java一摸一样）
- if
- switch
- for
- while
- do...while
### 函数
函数（方法）是被设计为执行特定任务的代码块
- 定义：JS函数通过**function**关键字进行定义，语法为：
  ```JavaScript
  function functionName(参数1，参数2){
      要执行的代码块
  }
  ```
  注意：
  - 形式参数不需要类型，因为JS是弱类型语言。
  - 返回值也不需要定义类型，可以在函数内部直接使用return返回即可。
- 调用：函数名(实际参数列表) `let result = add(1,2);`
- 定义方式二：
  ```JavaScript
  var functionName = function(参数列表){
      要执行的代码块
  }
  var add = function(a,b){
      return a+b;
  }
  ```
- JS中，函数调用可以传递任意个数参数。可以正常调用，但是多的参数不接收。
# JS常用对象
### Array
JS Array对象用于定义数组
- 定义
  ```JavaScript
  var 变量名 = new Array(元素列表);     var arr = new Array(1,2,3);
  ```
  ```JavaScript
  var 变量名 = [元素列表];     var arr = [1,2,3];
  ```
- 定义
  ```JavaScript
  arr[索引]=值;     arr[0]=1;
  ```
- 注意：JS数组类似于Java的集合，长度，类型都可变。
- 属性：length（数组中元素的个数）
- 方法：push（添加元素），splice（删除元素）（从哪删，删几个）
### String
- 定义
  ```javascript
  var 变量名 = new String(s);       var str = new String("hello");  
  ```
  ```javascript
  var 变量名 = s;       var str = "hello";      var str = 'hello';  
  ```
- 属性：length（字符串的长度）
- 方法：charAt()返回在指定位置的字符，IndexOf()检索字符串，trim()去掉字符串前后两端的空白字符
### 自定义对象
- 格式
  ```javascript
  var 对象名称 = {
      属性名称1:属性值1，
      属性名称2:属性值2，
      函数名称:function(形参列表){}
  };
  ```
  ```javascript
  var person = {
      name:"张三"，
      age:22，
      eat:function(){
          alert("干饭！");
      }
  };
  ```
# BOM
- Browser Object Model 浏览器对象模型
- JavaScript将浏览器的各个组成部分封装为对象
- 组成：
  - Window：浏览器窗口对象
    - 获取：直接使用window，其中window.可以省略
    - 属性：获取其他BOM对象（history，Navigator，Screen，location）
    - 方法：
      - alert(""):显示带有一段消息和一个确认按钮的警告框
      - confirm(""):显示带有一段消息以及确认按钮和取消按钮的对话框
        `var flag = confirm("确认删除？");`点击确定按钮返回true，点击取消按钮返回false。
      - setInterval(function,毫秒值):按照指定的周期（以毫秒计）来调用函数或计算表达式（循环执行）
      - setTimeout(function,毫秒值):在指定的毫秒数后调用函数或计算表达式（只执行一次）
  - Navigator：浏览器对象
  - Screen：屏幕对象
  - History：历史记录对象
    - 获取：使用window.history获取，其中window.可以省略
      ```JavaScript
      window.history.方法();
      history.方法();
      ```
    - 方法：back() 加载history列表中的前一个url。forward() 加载history列表中下一个url。
  - Location：地址栏对象
    - 获取：使用window.history获取，其中window.可以省略
      ```JavaScript
      window.location.方法();
      location.方法();
      ```
    - 属性：href 设置或返回完整的url
# DOM
- Document Object Model 文档对象模型
- 将标记语言的各个组成部分封装为对象
  - Document：整个文档对象
  - Element：元素对象
  - Attribute：属性对象
  - Text：文本对象
  - Comment：注释对象
- JS通过DOM，就能够对HTML进行操作了
  - 改变HTML元素的内容
  - 改变HTML元素的样式（CSS)
  - 对HTML DOM事件作出反应
  - 添加和删除HTML元素
- 获取Element对象
  - Element：元素对象
  - 获取：使用Document对象的方法来获取
    1. getElementById：根据id属性值获取，返回一个Element对象
    2. getElementsByTagName：根据标签名称获取，返回Element对象数组
    3. getElementsByName：根据name属性值获取，返回Element对象数组
    4. getElementsByClassName：根据class属性值获取，返回Element对象数组
- 常见HTML Element对象的使用
# 事件监听
- 事件：HTML事件是发生在HTML元素上的“事情”。比如：
  - 按钮被点击
  - 鼠标移动到元素之上
  - 按下键盘按键
- 事件监听：JS可以在事件被侦测到时执行代码
  - 事件绑定
    - 两种方式
      - 方式一：通过HTML标签中的事件属性进行绑定
        ```javascript
        <input type="button" onclick="on()">
        function on(){
          alert("我被点了");
        }
        ```
      - 方式二：通过DOM元素属性绑定
        ```javascript
        <input type="button" id="btn">
        document.getElementById("btn").onclick = function(){
          alert("我被点了");
        }
        ```
  - 常见事件
    - onsubmit事件：当表单提交时触发该事件。onsubmit=function(){//返回true则表单会被提交，返回false则表单不提交}
    - onclick：鼠标单击事件
    - onblur：元素失去焦点
    - onfocus：元素获得焦点
    - onload：某个页面或图像被完成加载
    - onkeydown：某个键盘的键被按下
    - onmouseover：鼠标被移到某元素之上
    - onmouseout：鼠标从某元素移开
  - Event代表事件对象
---
# 正则表达式
- 概念：正则表达式定义了字符串组成的规则
- 定义：
  1. 直接量：注意不要加括号。`var reg = /^\w{6,12}$/;`
  2. 创建RegExp对象。`var reg = new RegExp("^\\w{6,12}$");`
- 方法：test(str):判断指定字符串是否符合规则，返回true或者false
- 语法：
  - ^：表示开始
  - $：标识结束
  - []：代表某个范围内的单个字符，比如：[0-9]单个数字字符
  - .：代表任意单个字符，除了换行和行结束符
  - \w：代表单词字符：字符、数字、下划线、相当于[A-Za-z0-9_]
  - \d：代表数字字符，相当于[0-9]
  - 量词：
    - +：至少一个
    - *：零个或多个
    - ?：零个或一个
    - {x}：x个
    - {m,}：至少m个
    - {m,n}：至少m个，最多n个