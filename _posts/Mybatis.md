---
title: Mybatis复习总结（未完结）
date: 2021-01-07 09:18:08
tags: 
- mybatis
categories:
- ssm框架
---



<center>技术没有高低之分，只有使用的人有高低之分。</center>

<center>先把ssm中的mybatis重新再来一遍！</center>

<!--more-->

基础代码github地址：https://github.com/dllgdxlgy/Mybatis

时间：2020.12.29

环境：

+ JDK 1.8
+ Mysql 5.7
+ Maven 3.6.1
+ IDEA

回顾：

+ JDBC
+ Mysql （基本的增删改查）
+ Java基础
+ Maven
+ Junit



ssm框架学习都需要配置配置文件，都需要看[官网文档](https://mybatis.org/mybatis-3/zh/index.html)

# 1、简介

## 1.1、什么是Mybatis

<img src="https://gitee.com/dlutlgy/images_for_typora/raw/master/images/image-20201229201021860.png" alt="image-20201229201021860" style="zoom:67%;" />

+ MyBatis 是一款优秀的**持久层框架**，
+ 它支持自定义 SQL、存储过程以及高级映射。
+ MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作。
+ MyBatis 可以通过**简单的 XML** 或**注解**来配置和映射原始类型、接口和 Java POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。

百度百科：

MyBatis 本是apache的一个开源项目iBatis, 2010年这个项目由apache software foundation 迁移到了google code，并且改名为MyBatis 。2013年11月迁移到Github。

获取Mybatis的方式

+ Maven 

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.2</version>
</dependency>
```

+ GitHub [github上的mybatis](https://github.com/search?q=mybatis)
+ [中文文档](https://mybatis.org/mybatis-3/zh/index.html#) 

## 1.2、什么是持久化

+ 数据持久化，持久化就是将程序的数据在持状态和顺势状态转化的过程
+ 内存： **断电即失**
+ 数据库：io文件的持久化
+ 生活中：冷藏，也是持久化，就是延长保留

**为什么需要持久化？**

+ 有些数据需要保留
+ 内存太贵

## 1.3、持久层

Dao层，Service层，Controller层

+ 能完成持久化工作的代码块
+ 层界限十分明显

## 1.4、为什么需要Mybatis

+ 方便
+ 传统的JDBC太复杂，简化，框架，自动化
+ 帮助我们进行数据保存

+ 其实不用Mybatis也可以，现在主流公司都需要进行学习。

## 1.5、Mybatis特点

- 简单易学：本身就很小且简单。没有任何第三方依赖，最简单安装只要两个jar文件+配置几个sql映射文件易于学习，易于使用，通过文档和源代码，可以比较完全的掌握它的设计思路和实现。
- 灵活：mybatis不会对应用程序或者数据库的现有设计强加任何影响。 sql写在xml里，便于统一管理和优化。通过sql语句可以满足操作数据库的所有需求。
- 解除sql与程序代码的耦合：通过提供DAO层，将业务逻辑和数据访问逻辑分离，使系统的设计更清晰，更易维护，更易单元测试。sql和代码的分离，提高了可维护性。
- 提供映射标签，支持对象与数据库的orm字段关系映射
- 提供对象关系映射标签，支持对象关系组建维护
- 提供xml标签，支持编写动态sql。

**最重要的一点：使用的人多！**

# 2、第一个Mybatis程序

思路：搭建环境 -->导入Mybatis --> 编写代码 -->测试

## 2.1、搭建环境

1. 搭建数据库

```xml
USE mybaties;
create table user(
 id INT(20) NOT NULL PRIMARY KEY,
 name VARCHAR(20)DEFAULT NULL,
 pwd VARCHAR(30) DEFAULT NUll
)ENGINE=INNODB DEFAULT charset= utf8;

insert into user(id,name,pwd) values(1,'gy','123'),(2,'lgy','123'),(3,'y','123');
```

新建项目：

1. 新建一个普通的maven项目
2. 删除src目录，就可以当作父工程了。为了能进行创建子工程。
3. 导入maven依赖

```xml
<dependencies>

    <!-- https://mvnrepository.com/artifact/junit/junit -->
    <!--导入测试-->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>

    <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
    <!--导入mybatis-->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.2</version>
    </dependency>

    <!--导入数据库驱动-->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.45</version>
    </dependency>


</dependencies>
```

## 2.2、创建一个模块

new一个model，然后

+ 编写mybatis的核心配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">

<!--核心配置文件-->
<configuration>

    <!--可以配置多个环境-->
    <environments default="development">

        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">

                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=UTF-8"/>
                <property name="username" value="root"/>
                <property name="password" value="123"/>

            </dataSource>
        </environment>

    </environments>
    <mappers>
        <mapper resource="org/mybatis/example/BlogMapper.xml"/>
    </mappers>
</configuration>
```

+ 编写mybatis的工具类

```java
package com.lgy.utils;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import java.io.IOException;
import java.io.InputStream;

//编写mybatis的工具类
public class mybatisUtils {
    private static SqlSessionFactory sqlSessionFactory;

    static {
        try {
            //获取mybatis的sqlSessionFactory对象
            String resource = "mybatis-config.xml";
            InputStream inputStream = Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);

        }catch (IOException e){
            e.printStackTrace();
        }

    }
    public static SqlSession getSqlSession(){
        return sqlSessionFactory.openSession();
    }
}

```

## 2.3、编写代码

+ 编写实体类

```java
package com.lgy.pojo;

public class User {

    private int id;
    private String name;
    private String pwd;

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPwd() {
        return pwd;
    }

    public void setPwd(String pwd) {
        this.pwd = pwd;
    }

    public User() {
    }

    public User(int id, String name, String pwd) {
        this.id = id;
        this.name = name;
        this.pwd = pwd;
    }
}

```

+ 然后写Dao接口 

```java
package com.lgy.dao;
import com.lgy.pojo.User;
import java.util.List;

public interface userDao {
    public List<User> getUserList();
}

```

+ 最后写实现类(由原来的UserDaoImpl转换为Mapper配置文件)

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<!--namespace绑定一个对应的Dao/Mapper接口,就相当于之前实现了接口-->
<mapper namespace="com.lgy.dao.userDao">
    
    <!--查询语句-->
    <!--id对应着方法名字，因为之前需要写一个实现类进行实现userDao，这里没有实现，
    只是写了一个配置文件，实现类要重写之前的方法，但是这里没有重写，只是用select标签代替了-->
    <!--resultType要写他的全类名，这是返回类型-->
    <select id="getUserList" resultType="com.lgy.pojo.User" >
    select * from mybatis.user
    </select>
    
</mapper>
```

## 2.4、测试

```java
package com.lgy.dao;

import com.lgy.pojo.User;
import com.lgy.utils.mybatisUtils;
import org.apache.ibatis.session.SqlSession;
import org.junit.Test;

import java.util.List;

public class UserDaoTest {

    @Test
    public void test(){

        //获取sqlsession对象
        SqlSession sqlSession = mybatisUtils.getSqlSession();
        //执行SQl
        userDao userDao = sqlSession.getMapper(userDao.class);
        List<User> userList = userDao.getUserList();
        for (User user:userList){
            System.out.println(user);
        }

        //关闭SqlSession
        sqlSession.close();
    }
}

```

可能遇见的问题

+ 配置文件没有注册
+ 绑定接口错误
+ 方法名不对
+ 返回类型不对
+ maven导出资源问题

# 3、CRUD

namespace里面的包名要和接口的包名一致

1. select 选择语句

   + id：就是对应的namespace里面的方法名
   + resultset： 就是结果的返回值
   + parameterType：参数类型
2. insert
3. update
4. delete

流程：**编写接口--->写Mapper里面的sql语句--->测试**。 **增删改需要提交事务**

5. 万能的map

**问题描述**：如果要是传递一个实体类，比如进行修改密码，只传一个id和密码就可以， 其他的信息不需要，而进行传递一个实体类很麻烦，还带有其他信息，这时候需要map就可以， 需要什么信息直接穿进去，而且名字可以随意起，只要在mapper里面用对就可以。如果实体类中的字段或者参数过多，可以使用map。

# 4、配置解析

## 4.1、核心配置文件

+ Mybatis-config.xml

```xml
properties（属性）
settings（设置）
typeAliases（类型别名）
typeHandlers（类型处理器）
objectFactory（对象工厂）
plugins（插件）
environments（环境配置）
environment（环境变量）
transactionManager（事务管理器）
dataSource（数据源）
databaseIdProvider（数据库厂商标识）
mappers（映射器）
```

## 4.2、环境配置

可以配置多套环境

```xml
 <environments default="development">

        <environment id="development">
            <!--事务管理器-->
            <transactionManager type="JDBC"/>
            <!--默认是有数据库连接池的-->
            <dataSource type="POOLED">

                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?						 useSSL=true&amp;useUnicode=true&amp;characterEncoding=UTF-8"/>
                <property name="username" value="root"/>
                <property name="password" value="123"/>

            </dataSource>
        </environment>
        </environments>

```



## 4.3、属性

除了上面的代码直接写入数据库连接信息，还可进行配置文件的配置

db.properties文件

```properties
driver=com.mysql.jdbc.Driver

#这里面参数连接不需要进行&amp;
url=jdbc:mysql://localhost:3306/mybatis?useSSL=true&useUnicode=true&characterEncoding=UTF-8

username=root
password=123
```

在核心配置文件中引用

遇到的问题：

![image-20210104102832311](https://gitee.com/dlutlgy/images_for_typora/raw/master/images/image-20210104102832311.png)

这里面规定了配置文件中标签的顺序，所以不能乱了顺序写。

引用后

```xml
<!--引入外部配置文件-->
<properties resource="db.properties">
<!--这里面还可以进行写其他属性-->
</properties>
```

+ 可以直接引入外部配置文件
+ 也可以在其中mybatis-config.xml 的properties文件中增加配置
+ 如果两个文件有同一个字段，优先使用配置文件的中属性。

## 4.4、别名

起别名就是就是为了在XXXMapper.xml文件中的result类型中使用更方便，但是要注意在mybatis-config.xml文件的要正确使用<typeAliases>标签。

有两种使用方式，第一种，直接指定某一个实体类

例如：

```xml
 <typeAliases>
        <typeAlias type="com.lgy.pojo.User" alias="User"></typeAlias>
 </typeAliases>
```

第二种：可以指定某一个包名，Mybatis会自动扫描该包下的 java Bean,默认别名就是实体类的小写格式。

使用情况：

+ 在实体类比较少的时候可以使用第一种，这种就是比较简单，而且能够进行自己定义
+ 如果要使用第二种且要进行自己定义，不实用他默认的格式，可以添加@alias注解。

## 4.5、设置

```xml
<settings>
  <setting name="cacheEnabled" value="true"/>
  <setting name="lazyLoadingEnabled" value="true"/>
  <setting name="multipleResultSetsEnabled" value="true"/>
  <setting name="useColumnLabel" value="true"/>
  <setting name="useGeneratedKeys" value="false"/>
  <setting name="autoMappingBehavior" value="PARTIAL"/>
  <setting name="autoMappingUnknownColumnBehavior" value="WARNING"/>
  <setting name="defaultExecutorType" value="SIMPLE"/>
  <setting name="defaultStatementTimeout" value="25"/>
  <setting name="defaultFetchSize" value="100"/>
  <setting name="safeRowBoundsEnabled" value="false"/>
  <setting name="mapUnderscoreToCamelCase" value="false"/>
  <setting name="localCacheScope" value="SESSION"/>
  <setting name="jdbcTypeForNull" value="OTHER"/>
  <setting name="lazyLoadTriggerMethods" value="equals,clone,hashCode,toString"/>
</settings>
```

这里只注意mapUnderscoreToCamelCase就可以了。

## 4.6、映射器

方式一：**使用相对于类路径的资源引用**

```xml
<!-- 使用相对于类路径的资源引用 -->
<mappers>
        <mapper resource="com/lgy/dao/UserMapper.xml"/>
</mappers>
```

方式二：使用class文件进行绑定

```xml
<!-- 使用映射器接口实现类的完全限定类名 -->
<mappers>
  <mapper class="com.lgy.pojo.UserMapper"/>
</mappers>
```

注意点：

+ 接口和他的Mapper配置文件必须相同
+ 接口和他的配置文件必须在同一个包下

方式三：使用扫描包进行注入

```xml
<mappers>
  <package name="com.lgy.pojo"/>
</mappers>
```

+ 接口和他的Mapper配置文件必须相同
+ 接口和他的配置文件必须在同一个包下



# 5、解决属性名和字段名不一致的问题

数据库的字段名

<img src="https://gitee.com/dlutlgy/images_for_typora/raw/master/images/image-20210104152441089.png" alt="image-20210104152441089" style="zoom:50%;" />

实体类的属性名：

```java
private int id;
private String name;
private String password;
```

但是查出来password显示为空

![image-20210104154030017](https://gitee.com/dlutlgy/images_for_typora/raw/master/images/image-20210104154030017.png)

解决方法1：在xml文件的相应sql中进行修改，

解决方法2: resultMap（结果集映射）

```xml
<!--resultMap-->
<!-- resultMap中的id与<select>标签里面的resultMap里面的值要一样，要代表引用 -->
<resultMap id="usermap" type="User">
  <!--column代表数据库中字段，property代表实体类中的属性-->
  <result column="id" property="id"></result>
  <result column="name" property="name"></result>
  <result column="pwd" property="password"></result>
</resultMap>

<select id="getUserById"  parameterType="int" resultType="com.lgy.pojo.User" resultMap="usermap">
  select * from mybatis.user where id = #{id};
</select>
```

# 6、日志

## 6.1、日志工厂

如果数据库操作出现了异常，我们需要排错，日志就是最好的助手！这里使用日志工厂

只需要在mybatis-config.xml文件里显示添加

```xml
settings>
<!--注意name="logImpl" value="STDOUT_LOGGING"不要有空格-->
        <setting name="logImpl" value="STDOUT_LOGGING"/>
    </settings>

```



![image-20210104203938105](https://gitee.com/dlutlgy/images_for_typora/raw/master/images/image-20210104203938105.png)

## 6.2、Log4j

1. 导入Log4j依赖

```xml
<!--导入log4j依赖-->
        <dependency>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
            <version>1.2.17</version>
        </dependency>
```

2. 在resources中创建log4j.properties文件并写入：

```properties
#这里是日志输出的位置
log4j.rootLogger=DEBUG,console,file
log4j.additivity.org.apache=true

log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.Threshold=INFO
log4j.appender.stdout.Target=System.out
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%d %p [%c,%L] - %m%n

#log4j.appender.logfile.encoding=UTF-8
#log4j.appender.logfile=org.apache.log4j.RollingFileAppender
#log4j.appender.logfile.File=${lms.root}/WEB-INF/logs/lms.log
#log4j.appender.logfile.MaxFileSize=512KB
# Keep three backup files.
#log4j.appender.logfile.MaxBackupIndex=3
# Pattern to output: date priority [category] - message
#log4j.appender.logfile.layout=org.apache.log4j.PatternLayout
#log4j.appender.logfile.layout.ConversionPattern=%d %p [%c,%L] - %m%n

log4j.logger.orga.mybatis=DEBUG
log4j.logger.org.springframework=INFO
log4j.logger.com.opensymphony.xwork2=INFO
log4j.logger.org.apache.struts2=INFO
```

3. 在mybatis-config.xml文件中配置

```xml
<settings>
<!--这里LOG4J必须大写-->
<setting name="logImpl" value="LOG4J"></setting>
</settings>
```

4. Log4j的使用

   1. 在要使用Log4j类中导入包

   ```java
   import org.apache.log4j.Logger;
   ```

   2. 日志对象，参数为当前类的class

   ```java
   static Logger logger = Logger.getLogger(UserDaoTest.class);
   ```

   3. 日志级别 info、debug、error

# 7、分页

## 7.1使用limit分页

```sql
select * from user limitstartIndex,pageMax;
select * from user 0,2;  
```

使用mybatis实现分页，核心就是使用sql

1. 接口
2. MapperXml
3. 测试

## 7.2使用mybatis插件实现分页

<img src="https://gitee.com/dlutlgy/images_for_typora/raw/master/images/image-20210106140128103.png" alt="image-20210106140128103" style="zoom:50%;" />

[mybatis插件](https://pagehelper.github.io/)



# 8、使用注解开发

使用mybatis大多数使用配置文件，而是用其他的是使用注解的方式

## 8.1、面向接口编程

面向接口编程的根本原因就是为了**解耦**，是定义与实现的分离。

## 8.2、使用注解开发

使用注解对于简单的可以去写，但是对于有些繁杂的还是需要进行xml文件配置。

1. 注解在接口上的实现

```java
//注解就是简化开发的作用
@Select("select * from user")
public List<User> getUserList();
```

2. 需要在核心配置文件中绑定

```xml
<!--之前是绑定配置文件，这里是进行绑定接口-->
<mappers>
<mapper class="com.lgy.dao.userDao"/>
</mappers>
```

3. 测试



实现本质：反射

底层：动态代理



## 8.3、基于注解的CRUD

1. 可以设置自动提交事务(可不做)

```java
//true代表着自动提交事务
    public static SqlSession getSqlSession(){
        return sqlSessionFactory.openSession(true);
    }
}
```

2. 编写接口

```java
public interface userDao {

    //注解就是简化开发的作用

    @Select("select * from user")
    public List<User> getUserList();

    //这里本应该就一个参数id，但是由多个参数的时候一定要使用 @Param 注解，@Param 里面的id对应于sql语句里面的#{id}
    @Select("select *from user where id = #{id}")
    public User getUserById(@Param("id") int id,@Param("String") String name);

    //插入数据
    @Insert("insert into user (id,name,pwd) values (#{id},#{name},#{password})")
    public int insertUser(User user);

}
```

3. 编写测试类



# 9、Lombok

Project Lombok is a java library that automatically plugs into your editor and build tools, spicing up your java.
Never write another getter or equals method again, with one annotation your class has a fully featured builder, Automate your logging variables, and much more.

翻译：Lombok项目是一个Java库，它会自动插入您的编辑器和构建工具中，从而使您的Java更加生动有趣。永远不要再写另一个getter或equals方法，带有一个注释的您的类有一个全功能的生成器，自动化您的记录变量，等等。

说白了就是写bean更方便了。

1. 首先需要在idea里面进行插件的安装

   preferences -->plugins,进行搜索Lombok插件，然后选择进行安装。

2. 在项目中导入Lombok的包，如果使用maven直接在maven仓库里面进行搜索。

```xml
<!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.12</version>
    <scope>provided</scope>
</dependency>
```

3. 可以加注解进行使用

可以使用的注解

```
@Getter and @Setter
@FieldNameConstants
@ToString
@EqualsAndHashCode
@AllArgsConstructor, @RequiredArgsConstructor and @NoArgsConstructor
@Log, @Log4j, @Log4j2, @Slf4j, @XSlf4j, @CommonsLog, @JBossLog, @Flogger, @CustomLog
@Data
@Builder
@SuperBuilder
@Singular
@Delegate
@Value
@Accessors
@Wither
@With
@SneakyThrows
@val
@var
experimental @var
@UtilityClass
Lombok config system
Code inspections
Refactoring actions (lombok and delombok)
```

@Data : 生成无参构造，get、set、toString、hashcode、equals。

4. 举例子

```java
@Data
@AllArgsConstructor 
@NoArgsConstructor
public class Student {

    private int id;
    private String name;
    private int Grage;
    private boolean sex;
    private double height;
}
```



























