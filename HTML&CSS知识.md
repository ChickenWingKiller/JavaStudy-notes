# HTML
- HTML是一门语言，所有的网页都是用HTML这门语言编写出来的。
- HTML运行在浏览器上，HTML标签由浏览器来解析
- W3C（万维网联盟）标准：网页主要由三部分组成
    - 结构：HTML
    - 表现：CSS
    - 行为：JavaScript
## HTML快速入门
1. 新建文本文件，后缀名改为.html
2. 编写HTML结构标签
3. 在`<body>`中定义文字
```html
<html>
    <head>
        <title></title>
    </head>
    <body>

    </body>
</html>
```
**HTML的标签不区分大小写，标签属性值单双引号皆可**
**HTML的语法比较松散**

## 基础标签
|标签|描述|
|----|----|
|`<h1>`-`<h6>`|定义标题，h1最大，h6最小|
|`<font>`|定义文本的字体，字体尺寸，字体颜色|
|`<b>`|定义粗体文本|
|`<i>`|定义斜体文本|
|`<u>`|定义文本下划线|
|`<center>`|定义文本居中|
|`<p>`|定义段落|
|`<br>`|定义拆行，换行|
|`<hr>`|定义水平线|

## 图片、音频、视频标签
- img：定义图片
    - src：规定显示图像的URL（统一资源定位符）（当前目录：./a.jpg 可以省略）（上一级目录：../）
    - height：定义图像的高度 （尺寸单位：px和%）
    - width：定义图像的宽度
- audio：定义音频。支持的音频格式：MP3、WAV、OGG
    - src：规定音频的URL
    - controls：显示播放控件
- video：定义视频。支持的视频格式：MP4、WebM、OGG
    - src：规定视频的URL
    - controls：显示播放控件

## 超链接标签&列表标签
`<a>`定义超链接，用于链接到另一个资源
- href：指定访问资源的URL
- target：指定打开资源的方式
    - _self：默认值，在当前页面打开
    - _blank：在空白页面打开

有序列表（order list）
```html
<ol>
    <li>a</li>
    <li>b</li>
</ol>
```
无序列表（unorder list）
```html
<ul>
    <li>a</li>
    <li>b</li>
</ul>
```
type：设置项目符号

## 表格标签
- table：定义表格
    - border：规定表格边框的宽度
    - width：规定表格的宽度
    - cellspacing：规定单元格之间的空白
- tr：定义行
    - align：定义表格行的内容对齐方式
- td：定义单元格
    - rowspan：规定单元格可横跨的行数
    - colspan：规定单元格可横跨的列数
- th：定义表头单元格

## 布局标签
- div：定义HTML文档中的一个区域部分，经常与CSS一起使用，用来布局网页
- span：用于组合行内元素

## 表单标签
表单：在网页中主要负责数据采集功能，使用`<form>`标签定义表单
表单项（元素）：不同类型的input元素，下拉列表，文本域等
- form：定义表单
    - action：规定当提交表单时向何处发送表单数据，URL
    - method：规定用于发送表单数据的方式
        - get：浏览器会将数据直接附在表单的action URL之后。大小有限制
        - post：浏览器会将数据方法http请求消息体中。大小无限制
- input：定义表单项，通过type属性控制输入形式
    - type取值：text、password、radio、checkbox、file、hidden、submit、reset、button。
- label：为表单项定义标注
- select：定义下拉列表
- option：定义下拉列表的列表项
- textarea：定义文本域

---
# CSS
CSS是一门语言，用于控制网页表现
CSS（Cascading Style Sheet）：层叠样式表
## CSS导入方式（css和html的结合方式）
- CSS导入HTML有三种方式
    1. 内联样式：在标签内部使用style属性，属性值是css属性键值对
    ```html
    <div style="color:red">Hello CSS~</div>
    ```
    2. 内部样式：定义`<style>`标签，在标签内部定义css样式
    ```html
    <style type="text/css">
        div{
            color:red;
        }
    </style>
    ```
    3. 外部样式：定义link标签，引入外部的css文件
    ```html
    <link rel="stylesheet" href="demo.css">
    ```
    demo.css：
    ```html
    div{
        color:red;
    }
    ```
## CSS选择器
- 概念：选择器是选取需设置样式的元素（标签）
```html
div{
    color:red;
}
```
- 分类
    1. 元素选择器
    ```html
    元素名称{color:red;}
    ```
    ```html
    div{color:red;}
    ```
    2. id选择器
    ```html
    #id属性值{color:red;}
    ```
    ```html
    #name{color:red;}
    <div id="name">hello css</div>
    ```
    3. 类选择器
    ```html
    .class属性值{color:red;}
    ```
    ```html
    .cls{color:red;}
    <div class="cls">hello css</div>
    ```
## CSS属性
