# 一、Maven

## 1、是什么

是一款基于 Java 平台的项目管理和整合工具，它将项目的开发和管理过程抽象成一个项目对象模型（POM）。开发人员只需要做一些简单的配置，Maven 就可以自动完成项目的编译、测试、打包、发布以及部署等工作。

Maven 是使用 Java 语言编写的，因此它和 Java 一样具有跨平台性，这意味着无论是在 Windows ，还是在 Linux 或者 Mac OS 上，都可以使用相同的命令进行操作。

## 2、Maven目标

-   一个可重复使用，可维护且易于理解的项目综合模型
-   与此模型进行交互的工具和插件

## 3、Maven特点

1.  设置简单。
2.  所有项目的用法**一致**。
3.  可以管理和自动进行更新依赖。
4.  庞大且不断增长的**资源库**。
5.  可扩展，使用 Java 或脚本语言可以轻松的编写插件。
6.  几乎无需额外配置，即可立即访问新功能。
7.  基于模型的构建：Maven 能够将任意数量的项目构建为预定义的输出类型，例如 JAR，WAR。
8.  项目信息采取集中式的元数据管理：使用与构建过程相同的元数据，Maven 能够生成一个网站（site）和一个包含完整文档的 PDF。
9.  发布管理和发行发布：Maven 可以与源代码控制系统（例如 Git、SVN）集成并管理项目的发布。
10.  向后兼容性：您可以轻松地将项目从旧版本的 Maven 移植到更高版本的 Maven 中。
11.  并行构建：它能够分析项目依赖关系，并行构建工作，使用此功能，可以将性能提高 20%-50％。
12.  更好的错误和完整性报告：Maven 使用了较为完善的错误报告机制，它提供了指向 Maven Wiki 页面的链接，您将在其中获得有关错误的完整描述。

## 4、安装配置

### 1）Java环境配置

### 2）下载Maven

地址：[小精灵 – 下载阿帕奇小精灵 (apache.org)](https://maven.apache.org/download.cgi)

### 3）配置Maven环境变量

![](Typora图片\Maven配置环境1.png)

![Maven配置环境1](Typora图片\Maven配置环境.png)

### 4）验证Maven安装结果

![Maven安装验证](Typora图片\Maven安装验证.png)

### 5）修改本地仓库位置

在解压后的maven的conf文件中的settings.xml

添加属性

`<localRepository>E:/maven/repository</localRepository>`

### 6）修改maven下载文件中央资源库地址

在解压后的maven的conf文件中的settings.xml

添加属性

><mirrors>
>
>  <!-- mirror
>
>  <mirror>
>
>   <id>mirrorId</id>
>
>   <mirrorOf>repositoryId</mirrorOf>
>
>   <name>Human Readable Name for this Mirror.</name>
>
>   <url>http://my.repository.com/repo/path</url>
>
>  </mirror>
>
>   -->
>
>​	<mirror>
>
>​    <id>nexus-aliyun</id>
>
>​    <mirrorOf>*</mirrorOf>
>
>​    <name>Nexus aliyun</name>
>
>​    <url>http://maven.aliyun.com/nexus/content/groups/public</url>
>
>  </mirror>
>
> </mirrors>

### 7）

## 5、idea中配置本地Maven

Build, Execu tion, Deployment > Build Tools > Maven中配置路径

![idea配置Maven路径](Typora图片\idea配置Maven路径.png)

## 6、创建Maven项目

Maven 提供了大量不同类型的 Archetype 模板，通过它们可以帮助用户快速的创建 Java 项目，其中最简单的模板就是 maven-archetype-quickstart，它只需要用户提供项目最基本的信息，就能生成项目的基本结构及 POM 文件。

![](Typora图片\Maven的模板.png)

通过maven-archetype-quickstart模型，创建最原生的Maven项目

## 7、Maven的构建和测试

### 1）项目的构建

项目构建完成后，在该项目根目录中生成了一个名为 target 的目录

<img src="Typora图片\Maven构建.png" style="zoom:75%;" />

说明：

-   Maven 命令中包含了两个命令：**clean**和**package**，其中 clean 负责清理 target 目录，package 负责将项目构建并打包输出为 jar 文件。
-   classes：源代码编译后存放在该目录中。
-   test-classes：测试源代码编译后并存放在该目录中。
-   surefire-reports：Maven 运行测试用例生成的测试报告存放在该目录中。
-   helloMaven-1.0-SNAPSHOT.jar：Maven 对项目进行打包生成的 jar 文件。

### 2）项目的测试

项目依赖junit后就可以在AppTest中进行代码的测试，使用`@test`注解实现各自方法的独立运行。

```xml
<!--依赖：-->
<dependencies>
  <dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.11</version>
    <scope>test</scope>
  </dependency>
</dependencies>
```

```java
package org.example;

import static org.junit.Assert.assertTrue;

import org.junit.Test;

/**
 * Unit test for simple App.
 */
public class AppTest {
    /**
     * Rigorous Test :-)
     */
    
    //@Test注解
    @Test
    public void shouldAnswerWithTrue() {
        System.out.println("这是一个测试方法");
    }
}
```

<img src="C:\Users\Administrator\Desktop\xsjx\Typora图片\Maven测试.png" style="zoom:67%;" />



## 8、Maven坐标

Maven 坐标一套规则，它规定：世界上任何一个构件都可以使用 Maven 坐标并作为其唯一标识，Maven 坐标包括 **groupId**、**artifactId**、**version**、**packaging** 等元素，只要用户提供了正确的坐标元素，Maven 就能找到对应的构件。

==任何一个构件都必须明确定义自己的坐标==，这是 Maven 的强制要求，任何构件都不能例外。我们在开发 Maven 项目时，也需要为其定义合适的坐标，只有定义了坐标，其他项目才能引用该项目生成的构件。

```xml
<!--
这是依赖junit完成测试的包，具体的坐标参数为：

	groupId：项目组 ID，
		定义当前 Maven 项目隶属的组织或公司，通常是唯一的。它的取值一般是项目所属公司或组织的网址或 URL 的反写，例如 com.xszx

	artifactId：项目 ID，
		通常是项目的名称

	version：版本

	packaging：项目的打包方式
		默认值为 jar
-->
<groupId>com.xszx</groupId>
<artifactId>mavenDemo</artifactId>
<version>1.0-SNAPSHOT</version>
<packaging>jar</packaging>
```



## 9、Maven依赖

通俗的说，如果一个 Maven 构建所产生的构件（例如 jar 文件）被其他项目引用，那么该构件就是其他项目的依赖。

### 1）依赖声明

Maven 坐标是依赖的前提，**所有 Maven 项目必须明确定义自己的坐标**，只有这样，它们才可能成为其他项目的依赖。当一个项目的构件成为其他项目的依赖时，该项目的坐标才能体现出它的价值。

当 Maven 项目需要声明某一个依赖时，通常只需要在其 POM 中配置该依赖的坐标信息，Maven 会根据坐标自动将依赖下载到项目中。

```xml
<dependency>
  <groupId>junit</groupId>
  <artifactId>junit</artifactId>
  <version>4.11</version>
  <scope>test</scope>
</dependency>
```

-   groupId： 项目组 ID，定义当前 Maven 项目隶属的组织或公司，通常是唯一的。它的取值一般是项目所属公司或组织的网址或 URL 的反写，例如 com.xszx。
-   artifactId： 项目 ID，通常是项目的名称。
-   version：版本。
-   scope: 标签就是用来指定被依赖资源的依赖范围，可选配置有 compile、test、provided、runtime、system、import，若不指定则默认 compile。

### 2）获取依赖坐标

通常情况下，绝大部分依赖的 Maven 坐标都能在 [仓库服务 (aliyun.com)](https://developer.aliyun.com/mvn/search) 中获取。

选择合适的版本，在依赖详情页的最下方就是该版本依赖的 Maven 坐标，我们可以直接将其复制到项目的 pom.xml 中使用

<img src="Typora图片\aliyun仓库.png" style="zoom:80%;" />

## 10、Maven仓库

### 1）分类

![](Typora图片\Maven仓库分类.png)

### 2）Maven 依赖搜索顺序

当通过 Maven 构建项目时，Maven 按照如下顺序查找依赖的构件。

1.  从本地仓库查找构件，如果没有找到，跳到第 2 步，否则继续执行其他处理。
2.  从中央仓库查找构件，如果没有找到，并且已经设置其他远程仓库，然后移动到第 4 步；如果找到，那么将构件下载到本地仓库中使用。
3.  如果没有设置其他远程仓库，Maven 则会停止处理并抛出错误。
4.  在远程仓库查找构件，如果找到，则会下载到本地仓库并使用，否则 Maven 停止处理并抛出错误。
5.  当遇到一些在所有远程仓库中都不存在的构建，则程序员就需要手动的将需要依赖的构建添加到本地仓库

## 11、Maven插件（plugin）

Maven 实际上是一个依赖插件执行的框架，它执行的每个任务实际上都由插件完成的。<u>Maven 的核心发布包中并不包含任何 Maven 插件</u>，它们以独立构件的形式存在， 只有在 Maven 需要使用某个插件时，才会去仓库中下载。

### 1）插件目标

对于 Maven 插件而言，为了**提高代码的复用性**，通常一个 Maven 插件能够实现多个功能，每一个功能都是一个插件目标，即 Maven 插件是插件目标的集合。我们可以把插件理解为一个类，而插件目标是类中的方法，调用插件目标就能实现对应的功能。

![](C:\Users\Administrator\Desktop\xsjx\Typora图片\Maven插件类型.png)

### 2）

## 12、Maven导入本地jar包

Maven 是通过仓库对依赖进行管理的，当 Maven 项目需要某个依赖时，只要其 POM 中声明了依赖的坐标信息，Maven 就会自动从仓库中去下载该构件使用。

但在实际的开发过程中，经常会遇到一种情况：某一个项目需要依赖于存储在本地的某个 jar 包，该 jar 包无法从任何仓库中下载的，这种依赖被称为外部依赖或本地依赖。

那么这种依赖是如何声明的呢？

将本地的jar文件向本地仓库安装：

要想安装jar文件到本地则需要使用maven命令完成操作：

`mvn install:install-file -Dfile=D:\showData.jar -DgroupId=com.Mar -DartifactId=showData -Dversion=1.0.1 -Dpackaging=jar`

![](Typora图片\Maven导入本地jar.png)

执行了上面的命令后就会发现在本地的仓库中已经存在了一个依赖的构建

![](Typora图片\Maven导入本地jar2.png)

在本地的项目上就可以使用maven依赖完成操作：

```xml
<dependencies>
    <dependency>
      <groupId>com.Mar</groupId>
      <artifactId>showData</artifactId>
      <version>1.0.1</version>
    </dependency>
</dependencies>
```

<img src="Typora图片\Maven导入本地jar3.png" style="zoom:80%;" />

## 13、14、15、





# 二、MyBatis

## 1、是什么

MyBatis 是一款优秀的持久层（<u>持久层就是系统中专注于实现数据持久化的相对独立的层面</u>）框架，

它支持定制化 SQL、存储过程以及高级映射。

MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。

MyBatis 可以使用简单的 XML 或注解来配置和映射原生信息，将接口和 Java 的 POJOs(Plain Ordinary Java Object,普通的 Java对象)映射成数据库中的记录。

**常见的持久层框架：**

Hibernate、MyBatis、TopLink、Spring Data

## 2、JDBC

1）加载驱动（com.mysql.jdbc.Driver）

2）获取connection数据库连接对象

3）获取能执行sql语句数据库操作对象

4）执行sql语句（更新，查询）

5）事务的提交

6）关闭数据库连接

## 3、MyBatis的使用

### 1）引入MyBatis

要使用 MyBatis， 只需将 [mybatis-x.x.x.jar](https://github.com/mybatis/mybatis-3/releases) 文件置于类路径（classpath）中即可。

如果使用 Maven 来构建项目，则需将下面的依赖代码置于 pom.xml 文件中：

```xml
<dependency>
  <groupId>org.mybatis</groupId>
  <artifactId>mybatis</artifactId>
  <version>x.x.x</version><!--版本号-->
</dependency>
```

### 2）创建MyBatis的配置文件

在项目中创建一个XML配置文件存储相关的Mybatis的配置信息

XML 配置文件中包含了对 MyBatis 系统的核心设置，

包括获取数据库连接实例的数据源（DataSource）以及决定事务作用域和控制方式的事务管理器（TransactionManager）

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
  <environments default="development">
    <environment id="development">
      <transactionManager type="JDBC"/>
      <dataSource type="POOLED">
        <property name="driver" value="${driver}"/>
        <property name="url" value="${url}"/>
        <property name="username" value="${username}"/>
        <property name="password" value="${password}"/>
      </dataSource>
    </environment>
  </environments>
</configuration>
```

以上就是 Mybatis的配置文件，在文件中配置了连接数据库的数据源，数据源中包含数据库驱动、数据库访问地址、数据库用户名、数据库密码

### 3）从xml中创建SqlSessionFactory

每个基于 MyBatis 的应用都是以一个 SqlSessionFactory 的实例为核心的

SqlSessionFactory 的实例可以通过 SqlSessionFactoryBuilder 获得。

而 SqlSessionFactoryBuilder 则可以从 XML 配置文件或一个预先配置的 Configuration 实例来构建出 SqlSessionFactory 实例。

从 XML 文件中构建 SqlSessionFactory 的实例非常简单，建议使用类路径下的资源文件进行配置。 但也可以使用任意的输入流（InputStream）实例，比如用文件路径字符串或 file:// URL 构造的输入流。MyBatis 包含一个名叫 Resources 的工具类，它包含一些实用方法，使得从类路径或其它位置加载资源文件更加容易。

```java
@Test
public void getSqlSessionFactory() throws Exception {
    String resource = "mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
}
```

通过以上的代码获取到了SqlSessionFactory对象，此对象是Mybatis执行一切操作的基础

### 4）从SqlSessionFactory中获取SqlSession

在操作数据库是一定是以session会话来完成独立的操作，所以在MyBatis中也一样

既然有了 SqlSessionFactory，顾名思义，我们可以从中获得 SqlSession 的实例。

SqlSession 提供了在数据库执行 SQL 命令所需的所有方法。可以通过 SqlSession 实例来直接执行已映射的 SQL 语句。

```java
@Test
public void getSqlSession() throws Exception {
    //读取resources文件夹中的mybatis-config.xml文件
    String resource = "mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
    System.out.println(sqlSessionFactory);
    //获取数据库会话对象
    SqlSession sqlSession = sqlSessionFactory.openSession();
    System.out.println(sqlSession);
}
```

### 5）使用SqlSession对象执行sql

在对象射文件（PersonMapper.xml）创建根据主建查询单条数据的方法，供 SqISession对象去调用执行

```xml

<mapper namespace="com.Mar.mapper.PersonMapper">
<!--    编写sql语句-->
<!--    查询语句-->
    <select id="getOneById" >
        select * from person where id = #{id};
    </select>
</mapper>
```

上面在xml文件中定义了一个id属性为getOneById的查询语句



向mybatis核心配置文件中添加对象映射文件(xml):

```xml
<!--指定写入mapper-->
<mappers>
    <mapper resource="com/Mar/mapper/xml/PersonMapper.xml"></mapper>
</mappers>
```

![](Typora图片\mybatis_mapper.png)

方法一：

```java
Person person1 = (Person) sqlSession.selectOne("com.xszx.mybatis.mapper.PersonMapper.getOneById", 1);
```

方法二：

```java
//反射获取接口类
PersonMapper mapper = sqlSession.getMapper(PersonMapper.class);
//调用方法
Person person = mapper.getOneById(1);
```

但是在实际的开发中，其实咱们随着业务的增多，对应的实体映射文件(xml)还是会有很多，所以直接将XXX.xml文件存放在和mybatis核心配置文件同级的目录下还是比较容易出现很多意想不到的问题，所以在实际的开发中建议大家还是将实体映射文件和实体+实体的对应接口文件+实体文件存放在相同的目录中。

只需要在项目的pom.xml文件中添加指定资源文件来源的操作即可：

```xml
<build>
  <resources>
    <resource>
      <directory>src/main/java</directory>
      <includes>
        <include>**/*.xml</include>
      </includes>
    </resource>
    <resource>
      <directory>src/main/resources</directory>
    </resource>
  </resources>
</build>
```

添加后执行：

```java
@Test
public void getSqlSession() throws Exception{
    //读取resources文件夹中的mybatis-config.xml文件
    String resource = "mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
    //获取数据库会话对象
    SqlSession sqlSession = sqlSessionFactory.openSession();
    //执行sql语句
    PersonMapper mapper = sqlSession.getMapper(PersonMapper.class);
    //调用方法传递参数查询数据
    Person person = mapper.getOneById(2);
    System.out.println(person);
}
```

### 6）Log4j

使用log4j完成执行sql或者结果的展示，上面进行了数据库的查询操作，查出了部分的数据，但是在控制台没有发现任何的sql语句。

因为mybatis输出sql语句是依靠log4j来实现，所以在试用mybatis的时候如果想看sql语句的执行的话则需要使用log4j来完成语句的输出。

要想使用log4j咱们需要在resources目录下添加log4j的配置文件，配置文件的后缀log4j.properties

```properties
# Output pattern : date [thread] priority category - message   FATAL 0  ERROR 3  WARN 4  INFO 6  DEBUG 7
log4j.rootLogger=WARN, Console, RollingFile

#Console
log4j.appender.Console=org.apache.log4j.ConsoleAppender
log4j.appender.Console.layout=org.apache.log4j.PatternLayout
log4j.appender.Console.layout.ConversionPattern=%d %-5p [%c{5}] - %m%n

#RollingFile
log4j.appender.RollingFile=org.apache.log4j.DailyRollingFileAppender
log4j.appender.RollingFile.File=../logs/MyBatisDemo02/MyBatisDemo02.log
log4j.appender.RollingFile.layout=org.apache.log4j.PatternLayout
log4j.appender.RollingFile.layout.ConversionPattern=%d [%t] %-5p [%c] - %m%n

#log4j.logger.java.sql=DEBUG

#Springframework level
#log4j.logger.org.springframework=ERROR

#Hibernate level
#log4j.logger.org.hibernate=ERROR
#log4j.logger.org.hibernate.cache.ehcache.AbstractEhcacheRegionFactory=ERROR
#log4j.logger.org.hibernate.search.impl.ConfigContext=ERROR
#log4j.logger.net.sf.ehcache.config.CacheConfiguration=ERROR

#Project defalult level
#log4j.logger.org.activiti.engine.impl.persistence=DEBUG
#log4j.logger.org.apache.shiro=DEBUG
#OFF FATAL ERROR WARN INFO DEBUG TRACE ALL

#com.Mar为路径
log4j.logger.com.Mar=DEBUG
```

```java
Logger logger = Logger.getLogger(AppTest.class);
@Test
public void getSqlSession() throws Exception{
    //读取resources文件夹中的mybatis-config.xml文件
    String resource = "mybatis-config.xml";
    InputStream inputStream = Resources.getResourceAsStream(resource);
    SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
    //获取数据库会话对象
    SqlSession sqlSession = sqlSessionFactory.openSession();
    //执行sql语句
    PersonMapper mapper = sqlSession.getMapper(PersonMapper.class);
    //调用方法传递参数查询数据
    Person person = mapper.getOneById(2);
    System.out.println(person);
    logger.info(person);
}
```

![](Typora图片\Log4j.png)

![](Typora图片\Log4j_2.png)

### 7）

## 4、命名空间

在之前版本的 MyBatis 中，命名空间（Namespaces）的作用并不大，是可选的。 但现在，随着命名空间越发重要，你必须指定命名空间。

命名空间的作用有两个，一个是利用更长的全限定名来将不同的语句隔离开来，同时也实现了你上面见到的接口绑定。就算你觉得暂时用不到接口绑定，你也应该遵循这里的规定，以防哪天你改变了主意。 长远来看，只要将命名空间置于合适的 Java 包命名空间之中，你的代码会变得更加整洁，也有利于你更方便地使用 MyBatis。

在使用Mybtais的时候在遇到一些命名的时候最好使用全限定名。

## 5、注解的使用

对于像 PersonMapper这样的映射器类来说，还有另一种方法来完成语句映射。 它们映射的语句可以不用 XML 来配置，而可以使用 Java 注解来配置。比如，上面的 XML 示例可以被替使用注解来映射简单语句会使代码显得更加简洁，但对于稍微复杂一点的语句，Java 注解不仅力不从心，还会让你本就复杂的 SQL 语句更加混乱不堪。 因此，如果你需要做一些很复杂的操作，最好用 XML 来映射语句。

选择何种方式来配置映射，以及认为是否应该要统一映射语句定义的形式，完全取决于你和你的团队。 换句话说，永远不要拘泥于一种方式，你可以很轻松的在基于注解和 XML 的语句映射方式间自由移植和切换换成如下的配置：

```java
public interface PersonMapper {
    @Select("select * from person where id = #{id}")
    public Person getOneById(int id);
    @Delete("delete from person where id = #{id}")
    public void deleteById(int id);
}
```

使用注解来映射简单语句会使代码显得更加简洁，但对于稍微复杂一点的语句，Java 注解不仅力不从心，还会让你本就复杂的 SQL 语句更加混乱不堪。 因此，如果你需要做一些很复杂的操作，最好用 XML 来映射语句。

选择何种方式来配置映射，以及认为是否应该要统一映射语句定义的形式，完全取决于你和你的团队。 换句话说，永远不要拘泥于一种方式，你可以很轻松的在基于注解和 XML 的语句映射方式间自由移植和切换

## 6、7、8、9

## 三、四、五、六