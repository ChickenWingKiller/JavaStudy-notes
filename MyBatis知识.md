# MyBatis简介
* MyBatis是一款持久层框架，用于简化JDBC开发。
* 持久层：负责将数据保存到数据库的那一层代码。（JavaEE三层架构：表现层，业务层，持久层）
* 框架：一个半成品软件，是一套可重用、通用的、软件基础代码模型。
* MyBatis简化：硬编码->配置文件，操作繁琐->自动完成。Mybatis免除了几乎所有的JDBC代码以及设置参数和获取结果集的工作。
---
# Mybatis快速入门
## 查询emp表中所有数据
1. 创建emp表，添加数据
2. 创建模块，导入坐标
3. 编写MyBatis核心配置文件 --> 替换连接信息，解决硬编码问题
4. 编写SQL映射文件 --> 统一管理sql语句，解决硬编码问题
5. 编码：
    * 定义POJO类
    * 加载核心配置文件，获取SqlSessionFactory对象
    * 获取SqlSession对象，执行SQL语句
    * 释放资源 
## 解决SQL映射文件的警告信息
* 产生原因：Idea和数据库没有建立连接，不识别表信息。
* 解决方式：在Idea中配置MySQL数据库连接。
---
# Mapper代理开发
## 目的
* 解决原生方式中的硬编码
* 简化后期执行SQL
## 使用Mapper处理方式完成入门案例
1. 定义与SQL映射文件同名的Mapper接口，并且将Mapper接口和SQL映射文件放置在同一目录下。（在resource下创建包的结构，要用‘/’作为分隔符）
2. 设置SQL映射文件的namespace属性为Mapper接口全限定名。
3. 在Mapper接口中定义方法，方法名就是SQL映射文件中sql语句的id，并保持参数类型和返回值类型一致。
4. 编码
    1. 通过SqlSession的getMapper方法获取Mapper接口的代理对象
    2. 调用对应方法完成sql的执行
- 细节：如果Mapper接口名称和SQL映射文件名称相同，并在同一目录下，则可以使用包扫描的方式简化SQL映射文件的加载
---
# Mybatis核心配置文件
MyBatis核心配置文件的顶层结构如下：
- Configuration(配置)
    - properties(属性)
    - setting(设置)
    - typeAliases(类型别名)
    - typeHandlers(类型处理器)
    - objectFactory(对象工厂)
    - plugins(插件)
    - environments(环境配置)
        - environment(环境变量)
          - transactionManager(事务管理器)
          - dataSource(数据源)
    - databaseIdProvider(数据库厂商标识)
    - mappers(映射器)
- 类型别名(typeAliases)
```xml
<typeAliases>
    <package name="com.itheima.pojo"/>
</typeAliases>
```

**细节：配置各个标签时，需要遵循前后顺序。**

---
# 配置文件完成增删改查
### 编写接口方法（Mapper接口）->编写SQL（SQL映射文件）->执行方法
- 要完成的功能列表清单
    1. 查询
       1. 查询所有数据
       2. 查看详情 `Brand selectById(int id);`
       3. 条件查询
            - 多条件查询
              - 编写接口方法：Mapper接口
                - 参数：所有查询条件，可使用模糊查询
                - 结果：List<Brand>
              - 编写SQL语句：SQL映射文件
              - 执行方法，测试
            - 多条件查询-动态条件查询
                SQL语句会随着用户的输入或外部条件的变化而变化，称为动态SQL
              - MyBatis对动态SQL有很强大的支撑：
                - if
                - choose（when，otherwise）
                - trim（where，set）
                - foreach
            - 单条件-动态条件查询
                从多个条件中选一个。choose(when,otherwise):选择，类似于switch语句
    1. 添加
        - 编写接口方法：Mapper接口 `void add(Brand brand);`
            - 参数：除了id之外的所有数据
            - 结果：void
        - 编写SQL语句：SQL映射文件
        - 执行方法，测试
            - MyBatis事务：
                - openSession():默认开启事务，进行增删改操作后需要使用sqlSession.commit();手动提交事务
                - openSession(true):可以设置为自动提交事务（关闭事务）
        - 主键返回
        在数据添加成功后，需要获取插入数据库数据的主键的值
        返回添加数据的主键`<insert useGeneratedKeys="true" keyProperty="id">`
    2. 修改
       1. 修改全部字段
       2. 修改动态字段（要修改哪个字段，是不固定的）
            - 用`<if></if>`标签和`<set></set>`标签
    3. 删除
       1. 删除一个
       2. 批量删除
## Mybatis参数传递
如果传递多个参数，在接口中不用@Param注解
```sql
where
    username = #{arg0} 或 #{param1}
and password = #{arg1} 或 #{param2}
```
建议：将来都使用@Param注解来修改Map集合中默认的键名（arg0），并使用修改后的名称来获取值，这样可读性更高。
# 注解完成增删改查
```java
@Select("select * from emp where id=#{id}")
public Emp selectById(int id);
```
- 查询：@Select
- 添加：@Insert
- 修改：@Updata
- 删除：@Delete
**提示：注解完成简单功能，配置文件完成复杂功能。**
# 动态SQL
[百度](https://www.baidu.com/)