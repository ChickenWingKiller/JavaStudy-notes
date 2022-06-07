# JSP
- 概念：Java Server Pages，Java服务端页面
- 一种动态的网页技术，其中既可以定义HTML，JS，CSS等静态内容，还可以定义Java代码的动态内容
- JSP = HTML + Java
- JSP的作用：简化开发，避免了在Servlet中直接输出HTML标签
---
## JSP快速入门
1. 导入JSP坐标
2. 创建JSP文件
3. 编写HTML标签和Java代码
## JSP原理
- JSP本质上就是一个Servelt
- JSP在被访问时，由JSP容器（Tomcat）将其转换为Java文件（Servlet），再由JSP容器（Tomcat）将其编译，最终对外提供服务的其实就是这个字节码文件
## JSP脚本
- JSP脚本用于在JSP页面内定义Java代码
- JSP脚本分类
  1. <%...%>：内容会直接放到_jspService()方法之中
  2. <%=...%>：内容会放到out.print()中，作为out.print()的参数
  3. <%!...%>：内容会放到_jspService()方法之外，被类直接包含
## EL表达式 (替换获取数据的代码)
- Expression Language 表达式语言，用于简化JSP页面内的Java代码
- 主要功能：获取数据
- 语法：`${expression}`
    `${Brands}`:获取域中存储的key为brands的数据
- JavaWeb中的四大域对象：
  1. page：当前页面有效
  2. request：当前请求有效
  3. session：当前会话有效
  4. application：当前应用有效
el表达式获取数据，会依次从这4个域中寻找，直到找到为止
## JSTL标签（替换循环遍历的代码）
- JSP标准标签库（Jsp Standard Tag Library），使用标签取代JSP页面上的Java代码
- JSTL快速入门
  1. 导入坐标
  2. 在JSP页面上引入JSTL标签库
  3. 使用
  `<c:if test="">   </c:if>`
  `<c:forEach items="${}" var="">    </c:forEach>`  items：被遍历的容器。var：遍历产生的临时变量。varStatus：遍历状态对象
  `<c:forEach begin="0" end="10" step="1" var="i"> ${i} </c:forEach>`   begin:开始数。end：结束数。step：步长。
## MVC模式和三层架构
- MVC模式
  - MVC是一种分层开发的模式，其中：
    - M：Model，业务模型，处理业务
    - V：View，试图，界面展示
    - C：Controller，控制器，处理请求，调用模型和试图
- 三层架构
  - 数据访问层：对数据库的CRUD基本操作。(com.web/controller)
  - 业务逻辑层：对业务逻辑进行封装，组合数据访问层层中基本功能，形成复杂的业务逻辑功能。(com.service)
  - 表现层：接受请求，封装数据，调用业务逻辑层，响应数据。(com.dap/mapper)
## 案例
- 准备环境
  - 创建新的模块brand_demo，引入坐标
  - 创建三层架构的包结构
  - 数据库表tb_brand
  - 实体类Brand
  - MyBatis基础环境
    - Mybatis-config.xml
    - BrandMapper.xml
    - BrandMapper接口
- 查询所有
  - DAO层
    - BrandMapper，`List<Brand> selectAll()`
  - Service层
    - BrandService，selectAll调用brandMapper中的方法
  - Web层
    - SelectAllServlet：1.调用service查询 2.将数据存入request 3.转发到brand.jsp
- 添加
  - DAO层
    - BrandMapper，`void add(brand)`
  - Service层
    - BrandService，add调用brandMapper中的方法
  - Web层
    - SelectAllServlet：1.接收数据，封装Brand对象 2.调用service完成添加 3.转发到查询所有Servlet
- 修改-回显数据
  - DAO层
    - BrandMapper，`Brand selectById(id)`
  - Service层
    - BrandService，selectById调用brandMapper中的方法
  - Web层
    - SelectByIdServlet：1.接收id 2.调用service查询Brand 3.存储request 4.转发修改页面
- 修改-修改数据
  - DAO层
    - BrandMapper，`void update(brand)`
  - Service层
    - BrandService，add调用brandMapper中的方法
  - Web层
    - UpdateServlet：1.接收数据，封装Brand对象 2.调用service修改 3.转发到查询所有Servlet