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