# Maven基本使用：
## Maven常用命令
compile 编译  
clean 清理  
test 测试  
package 打包  
install 安装

# Idea配置Maven
## Maven坐标详解
**什么是坐标**：Maven中的坐标是资源的唯一标识，使用坐标来定义项目或引入项目中需要的依赖  
Maven坐标主要组成：groupId（定义当前Maven项目隶属组织名称），artifactId（定义当前Maven项目名称），version（定义当前项目版本号）。  
**Idea创建Maven项目**：1，创建模块，选择Maven，点击Next。2，填写模块名称，坐标信息，点击finish，创建完成。3，编写HelloWorld，并运行。  
**Idea导入Maven项目**：1，选择右侧Maven面板，点击+号。2，选中对应项目的pom.xml文件，双击。

# 依赖管理
## 使用坐标导入jar包
1，在pom.xml中编写\<dependencies>标签  
2，在\<dependencies>标签中使用\<dependency>引入坐标  
3，定义坐标的groupId，artifactId，version  
4，点击刷新按钮，是坐标生效