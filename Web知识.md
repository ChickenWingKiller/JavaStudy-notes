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