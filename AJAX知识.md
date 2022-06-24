# AJAX
- 概念：AJAX(Asychronous JavaScript And XML): 异步的JavaScript和XML
- AJAX作用：
  1. 与服务器进行数据交换：通过AJAX可以给服务器发送请求，并获取服务器响应的数据。使用了AJAX和服务器进行通信，就可以使用HTML+AJAX来<font color=red>替换JSP</font>页面了。
  2. 异步交互：可以在<font color=red>不重新加载整个页面</font>的情况下，与服务器交换数据并<font color=red>更新部分</font>网页的技术，如：搜索联想、用户名是否可以校验，等等。。。
- AJAX快速入门
  1. 编写AjaxServlet，并使用response输出字符串
  2. 创建XMLHttpRequest对象：用于和服务器交换数据
  3. 向服务器发送请求
  4. 获取服务器响应数据
- 案例-使用AJAX验证用户名是否存在
  - 需求：在完成用户注册时，当用户名输入框失去焦点时，校验用户名是否在数据库已存在
- Axios异步框架
  - Axios对原生的AJAX进行封装，简化书写
  - 官网：<https://www.axios-http.cn>
  - Axios快速入门
    1. 引入axios的js文件
    2. 使用axios发送请求，并获取响应结果
  - Axios请求方式别名
    - 为了方便起见，Axios已经为所有支持的请求方法提供了别名
- JSON
  - 概念：JavaScript Object Notation。 JavaScript对象表示法。
  - 由于其语法简单，层次结构鲜明，现多用于作为<font color=red>数据载体</font>，在网络中进行数据传输
  - JSON基础语法
    - 定义
    ```json
    var 变量名 = {
        "key1":value1,
        "key2":value2,
        ...
    }
    ```
    value的数据类型为：数字；字符串（在双引号中）；逻辑值（true，false）；数组（在方括号内）；对象（在花括号内）；null
    - 获取树蕨：`变量名.key`
  - JSON数据和Java对象转换
    - 请求数据：JSON字符串转为Java对象
    - 响应数据：Java对象转为JSON字符串
    - 使用Fastjson，可以实现Java对象和JSON字符串的相互转换
    - 使用：
      1. 导入坐标
      2. Java对象转JSON `String jsonStr = JSON.toJSONString(obj);`
      3. Json字符串转Java对象 `User user = JSON`
  - 案例-品牌列表数据（使用Axios + JSON完成品牌列表数据查询和添加）