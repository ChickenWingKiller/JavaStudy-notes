Web:全球广域网，万维网(WWW)，能够通过浏览器访问的网站
JavaWeb：是用Java技术来解决相关web互联网领域的技术栈
### Java技术栈
- B/S架构：Browser/Server，浏览器/服务器架构模式，它的特点是，客户端只需要浏览器，应用程序的逻辑和数据都储存在服务器端。浏览器只需要请求服务器，获取Web资源，服务器把Web资源发送给浏览器即可。
好处：易于维护升级。服务器升级后，客户端无需任何部署就可以使用到新的版本。
- 静态资源：HTML、CSS、JavaScript、图片等。负责页面展现
- 动态资源：Servlet、JSP等。负责逻辑处理
- 数据库：负责存储数据
- HTTP协议：定义通信规则
- Web服务器：负责解析HTTP协议，解析请求数据，并发送响应数据。（Apache Tomcat）
---
# HTTP
- 概念：超文本传输协议，规定了浏览器和服务器之间数据传输的规则
- HTTP协议特点：
  1. 基于TCP协议：面向连接，安全
  2. 基于请求-相应模型的：一次请求对应一次相应
  3. HTTP协议是无状态的协议：对于事务处理没有记忆能力。每次请求-相应都是独立的
     - 缺点：多情请求间不能共享数据。（会话技术Cookie、Session解决）
     - 优点：速度快
### HTTP-请求数据格式
- 请求数据分为三个部分：
  1. **请求行**：请求数据的第一行。其中GET表示请求方式, / 表示请求资源路径, HTTP/1.1 表示协议版本
  2. **请求头**：第二行开始，格式为key: value形式。
  3. **请求体**：请求体：POST请求的最后一部分，存放请求参数。和响应头之间有一行空行。
### HTTP-响应数据格式
- 相应数据分为3部分
  1. 相应行：相应数据的第一行。其中HTTP/1.1代表协议版本，200代表相应状态码，OK代表状态码描述。
  2. 相应头：第二行开始，格式为key：value形式
  3. 响应体：最后一部分。存放相应数据。和响应头之间有一行空行。
---
# Web服务器 - Tomcat
- Web服务器是一个应用程序（软件），对HTTP协议的操作进行封装，使得程序员不必直接对协议进行操作，让Web开发更加便捷。主要功能是“提供网上信息浏览服务”。
  - 封装HTTP协议操作，简化开发
  - 可以将web项目部署到服务器中，对外提供网上浏览服务。
- 简介
  - 一个开源免费的轻量级Web服务器，支持Servlet/JSP少量JavaEE规范。
  - Tomcat也被称为Web容器、Servlet容器。Servlet需要依赖于Tomcat才能运行。
  - [官网](https://tomcat.apache.org/)
- 基本使用：安装、卸载、启动、关闭、配置、部署项目
  - 启动：双击 bin\startup.bat
  - 关闭：
    - 直接x掉运行窗口，强制关闭
    - bin\shutdown.bat，正常关闭
    - crtl+C，正常关闭
  - 配置：
    - 修改启动端口号：conf\server.xml
    ```xml
    <Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectport="8443"  />
    ```
    - HTTP协议默认端口号为80，如果将Tomcat端口号改为80，则将来访问Tomcat时，将不用输入端口号。
  - 部署项目
    - 将项目放置到webapps目录下，即部署完成
    - 一般JavaWeb项目会被打成war包，然后将war包放到webapps目录下，Tomcat会自动解压缩war文件。
- IDEA中创建Maven Web项目
  - Web项目结构
    - Maven Web项目结构：开发中的项目
    - 部署的JavaWeb项目结构：开发完成，可以部署的项目（package后的）
  - 使用骨架（骨架：项目模板）
    1. 选择Web项目骨架，创建项目
    2. 删除pom.xml中多余的坐标
    3. 补充缺失的目录结构
  - 不使用骨架
    1. 选择web项目骨架，创建项目
    2. pom.xml中添加打包方式为war
    3. 补充缺失的目录结构：webapp
- IDEA中使用Tomcat
  - 集成本地Tomcat，将本地Tomcat集成到Idea中，然后进行项目部署即可。
  - Tomcat Maven插件
    1. pom.xml添加Tomcat插件
    2. 使用Maven Helper插件快速启动项目，选中项目，右键 -> Run Maven -> tomcat7:run
---
# Servlet
#### Servlet是Java提供的一门动态web资源开发技术
#### Servlet是JavaEE规范之一，其实就是一个接口，将来我们需要定义Servlet类实现Servlet接口，并由web服务器运行Servlet
- 快速入门
  1. 创建web项目，导入Servlet依赖坐标
  ```xml
  <dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>3.1.0</version>
    <scope>provided</scope>
  </dependency>
  ```
  2. 创建：定义一个类，实现Servlet接口，并重写接口中所有方法，并在service方法中输出一句话
  ```java
  public class ServletDemo implements Servlet(){
    public void service(){}
  }
  ```
  3. 配置：在类上使用@WebServlet注解，配置该Servlet的访问路径
  ```java
  @WebServlet("/demo")
  public class ServletDemo implements Servlet(){
  ```
  4. 访问：启动Tomcat，浏览器输入URL访问该Servlet
  ```url
  http://localhost:8080/web-demo/demo1
  ```
- Servlet执行流程
  - Servlet由谁创建？Servlet方法由谁调用？
Servlet由Web服务器创建，Servlet方法由Web服务器调用。
  - 服务器怎么知道Servlet中一定有service方法？
因为我们自定义的Servlet，必须实现Servlet接口并复写其方法，而Servlet接口中有serv方法。
- Servlet生命周期
  - 对象的生命周期指一个对象从被创建到被销毁的整个过程
  - Servlet运行在Servlet容器（web服务器）中，其生命周期由容器来管理，分为四个阶段：
    1. 加载和实例化
    2. 初始化，init()
    3. 请求处理，service()
    4. 服务终止，destroy()
- Servlet方法介绍
  - 初始化方法，在Servlet被创建时执行，只执行一次`void init(ServletConfig config)`
  - 提供服务方法，每次Servlet被访问，都会调用该方法`void service(ServletRequest req, ServletResponse res)`
  - 销毁方法，当Servlet被销毁时，调用该方法。在内存释放或服务器关闭时销毁Servlet`void destroy()`
  - 获取ServletConfig对象`ServletConfig getServletConfig()`
  - 获取Servlet信息`String getServletInfo()`
- Servlet体系结构
  我们将来开发B/S架构的web项目，都是针对HTTP协议，所以我们自定义Servlet，会继承HttpServlet
  - 继承HttpServlet类，复写doGet(get请求方式处理逻辑)和doPost(post请求方式处理逻辑)方法
- Servlet urlPattern配置
  - Servlet要想被访问，必须配置其访问路径（urlPattern）
  1. 一个Servlet，可以配置多个urlPattern
      ```java
      @WebServlet(urlPatterns = {"/demo1","/demo2"})
      ```
  2. urlPattern配置规则
     1. 精确匹配
      配置路径：`@WebServlet("/user/select")`
      访问路径：`localhost:8080/web-demo/user/select`
     2. 目录匹配
      配置路径：`@WebServlet("/user/*")`
      访问路径：`localhost:8080/web-demo/user/aaa`、`localhost:8080/web-demo/user/bbb`
     3. 扩展名匹配
      配置路径：`@WebServlet("*.do")`
      访问路径：`localhost:8080/web-demo/aaa.do`、`localhost:8080/web-demo/bbb.do`
     4. 任意匹配 
      配置路径：`@WebServlet("/")`、`@WebServlet("/*")`
      访问路径：`localhost:8080/web-demo/hehe`、`localhost:8080/web-demo/haha`
      - / 和 */ 区别：
        - 当我们的项目中的Servlet配置了"/"，会覆盖掉tomcat中的DefaultServlet，当其他的url-pattern都匹配不上时都会走这个Servlet。无法访问静态资源。
        - 当我们的项目中配置了"/*",意味着匹配任意访问路径
      - 优先级：精确路径>目录路径>扩展名路径>/*>/
- XML配置方式编写Servlet
  - Servlet从3.0版本后开始支持实用注解配置，3.0版本前只支持XML配置文件的配置方式
  - 步骤：
    1. 编写Servlet类
    2. 在web.xml中配置该Servlet
    ```xml
    <servlet>
      <servlet-name>demo5</servlet-name>
      <servlet-class>com.itheima.web.servlet.ServletDemo5</servlet-class>
    </servlet>
    <servlet-mapping>
      <servlet-name>demo5</servlet-name>
      <url-pattern>demo5<url-pattern>
    </servlet-mapping>
    ```
### Request(请求) & Response(响应)
- Request：获取请求数据
  - Request继承体系：
    ServletRequest(Java提供的请求对象根接口) <- HttpServletRequest(Java提供的对Http协议封装的请求对象接口) <- RequestFacade(Tomcat定义的实现类)
    1. Tomcat需要解析请求数据，封装为request对象，并且创建request对象传递到service方法中
    2. 使用request对象，查阅JavaEE API文档的HttpServletRequest接口
  - Request获取请求数据：
    - 请求数据分为3部分：
      1. 请求行：`GET/request-demo/req1?username=zhangsan HTTP/1.1`
         - String getMethod():获取请求方式：GET
         - String getContextPath():获取虚拟目录（项目访问路径）：/request-demo
         - StringBuffer getRequestURL():获取URL(统一资源定位符)：http://localhost:8080/request-demo/req1
         - String getRequestURL():获取URI(统一资源标识符):/request-demo/req1
         - String getQueryString():获取请求参数（GET方式）：username=zhangsan&password=123
      2. 请求头：`User-Agent:Mozilla/5.0 Chrome/91.0.4472.106`
         - String getHeader(String name):根据请求头名称，获取值
      3. 请求体：`username=superbaby&password=123`
         - ServletInputStream getInputStream():获取字节输入流
         - BufferedReader getReader():获取字符输入流 
  - Request请求转发：forward,一种在服务器内部的资源跳转方式
    - 实现方式：
      - `req.getRequestDispatcher("资源B路径").forward(req,resp);`
    - 请求转发资源间共享数据：使用Request对象
      - `void setAttribute(String name, Object o)`：存储数据到request域中
      - `Object getAttribute(String name)`：根据key，获取值
      - `void removeAttribute(String name)`：根据key删除该键值对
    - 请求转发特点：
      - 浏览器地址栏路径不发生变化
      - 只能转发到当前服务器的内部资源
      - 一次请求，可以在转发的资源间使用request共享数据
  - 通用方式获取请求参数：提供一种统一获取请求参数的方式，从而统一doGet和doPost方法内的代码。
    - `Map<String, String[]> getParameterMap(): 获取所有参数Map集合`
    - `String[] getParameterValues(String name)：根据名称获取参数值(数组)`
    - `String getParameter(String name): 根据名称获取参数值(单个值)`
    - 使用通用方式获取请求参数后，屏蔽了GET和POST的请求方式代码的不同，则代码可以定义为如下格式：
      ```java
      doGet(){

      }
      doPost(){
        this.doGet
      }
      ```
    - 可以使用Servlet模板创建Servlet更高效
  - 请求参数中中文乱码处理
    - Post:设置输入流的编码
      request.setCharacterEncoding("UTF-8");
    - Get:先编码，再解码
      `new String(username.getBytes("ISO-8859-1"),"UTF-8");`
- Response：设置响应数据
  - 设置响应数据功能介绍
    - 响应数据分为3部分：
      1. 相应行：`HTTP/1.1 200 OK`
         - `void setStatus(int sc)`：设置相应状态码
      2. 响应头：`Content-Type:text/html`
         - `void setHeader(String name, String value)`：设置相应头键值对
      3. 响应体：`<html><head><head><body></body></html>`
         - `PrintWriter getWriter()`：获取字符输出流
         - `ServletOuputStream getOutputStream()`：获取字节输出流
  - 完成重定向
    - 重定向（Redirect）：一种资源跳转方式。（我处理不了，找别人处理，**状态码：302**，那个人的位置是xxx，**响应头location：xxx**）
    - 实现方式：
      `resp.setStatus(302);`
      `resp.setHeader("location","资源B的路径");`（资源B的路径需要加虚拟目录）
      简化方式完成重定向：`resp.sendRedirect("资源B的路径");`
    - 重定向特点
      - 浏览器地址栏路径发生变化
      - 可以重定向到任意位置的资源（服务器内部、外部均可）
      - 两次请求，不能在多个资源使用request共享数据
    - 路径问题
      - 明确路径谁使用：
        - 浏览器使用：需要加虚拟目录（项目访问路径）
        - 服务器使用：不需要加虚拟目录
        - 动态获取虚拟目录：`String contextPath = request.getContextPath();` (contextPath + "/resp2")
  - 响应字符数据
    - 使用：
      1. 通过Response对象获取字符输出流
          `PrintWriter writer = resp.getWriter();`
          ```java
          response.setContentType("text/html;charset=utf-8"); //设置response的响应格式和字符集
          //1.获取字符输出流
          PrintWriter writer = response.getWriter();
          //2.设置响应头信息，content-type
          response.setHeader("content-type", "text/html");
          writer.write("aaa");
          writer.write("<h1>aaa</h1>");
          ```
      2. 写数据
          `writer.write("aaa");`
    - 注意：
      - 该流不需要关闭，随着相应结束，response对象销毁，由服务器关闭
      - 中文数据乱码：原因通过Response获取的字符输出流默认编码：ISO-8859-1
        `resp.setContentType("text/html;charset=utf-8");`
  - 响应字节数据
    - 使用：
      1. 通过Response对象获取字节输出流
        `ServletOutputStream outputStream = resp.getOutputStream();`
        ```java
        //1.读取数据
        FileInputStream fis = new FileInputStream("d://a.jpg");
        //2.获取response字节输出流
        ServletOutputStream os = response.getOutputStream();
        //3.完成流的copy
        byte[] buff = new byte[1024];
        int len = 0;
        while ((len = fis.read(buff)) != -1) {
          os.write(buff, 0, len);
        }
        fis.close();
        ```
        这个方法很麻烦，经过引用commons-io的依赖后，第三步可以替换为：
        `IOUtils.copy(fis,os);`
      2. 写数据
        `outputStream.write(字节数据);`
    - IOUtils工具类使用
      1. 导入坐标
        ```xml
        <dependency>
          <groupId>commons-io</groupId>
          <artifactId>commons-io</artifactId>
          <version>2.6</version>
        </dependency>
        ```
      2. 使用
        `IOUtils.copy(输入流, 输出流);`
- 案例：用户登录
  - 流程说明
    1. 用户填写用户名密码，提交到LoginServlet
    2. 在LoginServlet中使用MyBatis查询数据库，验证用户名密码是否正确
    3. 如果正确，响应“登陆成功”，如果错误，响应”登陆失败“
  - 准备环境：
    1. 复制资料中的静态页面到项目的webapp目录下
    2. 创建数据库，创建表，创建User实体类
    3. 导入MyBatis坐标，MySQL驱动坐标
    4. 创建mybatis-config.xml核心配置文件，UserMapper.xml映射文件，UserMapper接口
- 案例：用户注册
  - 流程说明：
    1. 用户填写用户名、密码等信息，点击注册按钮，提交到RegisterServlet
    2. 在RegisterServlet中使用MyBatis保存数据
    3. 保存前，需要判断用户名是否已经存在：根据用户名查询数据库
- 代码优化
  - 创建SqlSessionFactory代码优化
  - 问题：
    - 代码重复。----> 抽取到一个工具类
    - 浪费资源。SqlSessionFactory工厂应该只创建一次，不要重复创建。 ----> 静态代码块
  
---
# Filter
#### 概念：Filter表示过滤器，是JavaWeb三大组件（Servlet、Filter、Listener）之一。
#### 过滤器可以把对资源的请求<font color=red>拦截</font>下来，从而实现一些特殊的功能。
#### 过滤器一般完成一些<font color=red>通用</font>的操作，比如：权限控制，统一编码处理，敏感字符处理等等。。。
- Filtrt快速入门
  1. 定义类，实现Filter接口，并重写其所有方法
  2. 配置Filter拦截资源的路径：在类上定义@WebFilter注解
  3. 在doFilter方法中输出一句话，并放行 `chain.doFilter(request,response);`
- Filter执行流程
  - 放行后访问对应资源，资源访问完成后，还会回到Filter中。
  - 如果回到Filter中，直接执行放行后的逻辑
  - 执行放行前逻辑 -> 放行-> 访问资源 -> 执行放行后逻辑
  - 放行前，对request数据进行处理。放行后，对response数据进行处理。
- Filter使用细节
  - Filter拦截路径配置(@WebFilter("/*"))
    - 拦截具体的资源：/index.jsp: 只有访问index.jsp时才会被拦截
    - 目录拦截：/user/*: 访问/user下的所有资源，都会被拦截
    - 后缀名拦截：*.jsp: 访问后缀名为jsp的资源，都会被拦截
    - 拦截所有：/*: 访问所有资源，都会被拦截
  - 过滤器链 （多个过滤器一起起作用）
    - 一个Web应用，可以配置多个过滤器，这多个过滤器成为过滤器链
    - 注解配置的Filter，优先级按照过滤器类名（字符串）的自然排序
- 案例-登录验证
  - 需求：访问服务器资源时，需要先进行登录验证，如果没有登录，则自动跳转到登陆页面
  - 判断访问的是否是登录相关路径
    - 是：放行
    - 不是：进行登录验证
  - 判断用户是否登录：session中是否有user对象
    - 登录：直接放行
    - 未登录：跳转到登陆页面，并给出提示信息

---
# Listener
- 概念：Listener表示监听器，是JavaWeb三大组件之一。
- 监听器可以监听，就是在application，session，request三个对象创建，销毁或者往其中添加修改删除属性时<font color=red>自动</font>执行代码的功能组件。
- Listener分类：JavaWeb中提供了8个监听器。
- ServletContextListener使用
  1. 定义类，实现ServletContextListener接口
  2. 在类上添加@WebListener