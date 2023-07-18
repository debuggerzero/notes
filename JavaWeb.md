# JavaWeb

## 1. 基本概念

### 1.1. 前言

- **Web 开发：**
  - Web：网页	
  - 静态 Web
    - HTML、CSS
    - 提供给所有人看的数据始终不会发生改变
  - 动态 Web
    - 提供给所有人看的数据会发生变化，不同的时间、不同的地点看到的信息各不相同
    - 技术栈：Servlet / JSP、ASP、PHP
- 在 Java 中，动态 Web 资源开发的技术统称为 JavaWeb

### 1.2. Web 应用程序

- Web 应用程序：可以提供浏览器访问的程序；
  - 能访问到的任何一个页面或者资源，都存在于这个世界的某一个角落的计算机上
  - URL
  - 这个统一的 Web 资源会被放在同一个文件夹下，Web 应用程序 --> Tomcat：服务器
  - 一个 Web 应用有多个部分组成（静态 Web，动态 Web）
    - HTML，CSS，Js
    - jsp，Servlet
    - Java 程序
    - jar 包
    - 配置文件 (properties)
- Web 应用程序编写完毕后，若想提供给外界访问：需要一个服务器来统一管理；

### 1.3. 静态 Web

- *.htm, *html，这些都是网页的后缀
- 静态 Web 存在的缺点
  - Web 页面无法动态更新，所有用户能看到都是同一个页面
    - 轮播图，点击效果：伪动态
    - JavaScript [实际开发中，他用的最多]
    - VBScript
  - 他无法和数据库交互（数据无法持久化，用户无法交互）

### 1.4. 动态 Web

- 页面会动态展示："Web 的页面展示的效果因人而异"
- 缺点
  - 加入服务器的动态 Web 资源出现了错误，我们需要重新编写我们的**后台程序**，重新发布
    - 停机维护
- 优点
  - 静态 Web 存在的缺点
    - Web 页面可以动态更新，所有用户能看到不是同一个页面
    - 他可以和数据库交互

## 2、HTTP

1. HTTP 称之为 **超文本传输协议**

2. HTTP 是**无状态**的

3. HTTP 请求响应包含**两个**部分：**请求和响应**

   - **请求：**

     请求包含三个部分：1. 请求行；2. 请求信息头；3. 请求主体；

     - 请求行包含是三个信息：

     1. 请求的方式；
     2. 请求的URL；
     3. 请求的协议（一般都是 HTTP1.1）

     - 请求消息头中包含了很多客户端需要告诉服务器的信息，比如：我的浏览器型号、版本、我能接收的内容的类型、我给你发的内容的类型、内容的长度等等..
     - 请求体，三种情况：

     1. get 方法，没有请求体，但是有一个 queryString
     2. post 方法，有请求体，form data
     3. json 格式，有请求体，request payload 

   - **响应：**

     响应也包含三部分：1. 响应行；2. 响应头；3. 响应体

     - 响应行包含三个信息：1. 协议；2. 响应状态码；3. 响应状态
     - 响应头：包含了服务器的信息；服务器发送给浏览器的信息（内容的媒体类型、编码、内容长度等）
     - 响应体：响应的实际内容；比如: 请求 add.html 页面时，响应的内容就是```<html><head><body><form>...``` 

### 2.1. 两个时代

- HTTP/1.0：客户端可以与 Web 服务器连接后，只能获得一个 Web 资源，断开连接
- HTTP/1.1：客户端可以与 Web 服务器连接后，可以获得多个 Web 资源

### 2.2. Http 请求

- 客户端 --- 发请求 (Request) --- 服务器

```java
Request URL: https://www.baidu.com/			//请求地址
Request Method: GET						   //get 方法/ post 方法
Status Code: 200 OK						   //状态码：200
Remote Address: 180.101.49.11:443
```

```java
Accept:text/html
Accept-Encoding: gzip, deflate, br
Accept-Language: en,zh-CN;q=0.9,zh;q=0.8
Connection: keep-alive
```

1.	**请求行**
   - 请求行中的请求方式：GET
   - 请求方式：GET，POST.....
     - get：请求能够携带的参数比较少，大小有显示，会在浏览器的 URL 地址栏显示数据内容，不安全，但高效。
     - POST：请求能够携带的参数没有限制，大小没有显示，不会在浏览器的 URL 地址栏显示数据内容，安全，但不高效。
       2.**消息头**

```java
Accept：告诉浏览器，它所支持的数据类型
Accept-Encoding：支持哪种编码格式 GBK UTF-8 GB2312 ISO8859-1
Accept-Language：告诉浏览器，它的语言环境
Cache-Control：缓存控制
Connection：告诉浏览器，请求完成是断开还是保持连接
Host：主机...../.
```

### 2.3. Http 响应

- 服务器 --- 响应 --- 客户端

```java
Cache-Control: private										//缓存控制
Connection: keep-alive										//连接
Content-Encoding: gzip										//编码
Content-Type: text/html;charset=utf-8						 //类型
```

1. 响应体

```java
Accept：告诉浏览器，它所支持的数据类型
Accept-Encoding：支持哪种编码格式 GBK UTF-8 GB2312 ISO8859-1
Accept-Language：告诉浏览器，它的语言环境
Cache-Control：缓存控制
Connection：告诉浏览器，请求完成是断开还是保持连接
Host：主机...../.
Refrush：告诉客户端，多久刷新一次
Location：让网页重新定位
```

2. 响应状态码
   - 200：请求响应成功
   - 3xx：请求重定向  
     - 重定向：你重新到我给你新位置去
   - 4xx：找不到资源  404
     - 资源不存在
   - 5xx：服务器代码错误  500  502：网关错误

## 3、Maven

**为什么要学习这个技术？**

1. 在 JavaWeb 开发中，需要使用大量的 jar 包，我们手动去导入；
2. 如何能够让一个东西自动帮我导入和配置这个 jar 包

### 3.1. Maven 项目架构管理工具

Maven 核心思想：约定大于配置

- 有约束，不要去违反

Maven 会规定好你如何去编写 Java 代码，必须要按照规范来；

### 3.2. 配置环境变量

- M2-HOME	maven 目录下的 bin
- MAVEN_HOME     maven 的目录
- 在系统的 path 中配置

### 3.3. 阿里云镜像

```java
<mirror>
    <id>alimaven</id>
    <name>aliyun maven</name>
    <url>https://maven.aliyun.com/repository/public/</url>
    <mirrorOf>central</mirrorOf>
</mirror>
```

### 3.4. 本地仓库

在本地的仓库，远程仓库；

建立一个本地仓库 localRepository

```java
<localRepository>E:\Instrument\apache-maven-3.6.3\maven-repo</localRepository>
```

### 3.5. pom 文件

- pom.xml 是 Maven 的核心配置文件

```xml
<!-- Maven 版本和头文件 -->
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
<modelVersion>4.0.0</modelVersion>
```

```xml
<groupId>com.zero</groupId>
<artifactId>javaweb-01-maven</artifactId>
<version>1.0.0.0</version>
<!-- 
    Package：项目的打包方式 
    jar：Java 应用
    war：JavaWeb 应用
-->
<packaging>war</packaging>
```

```xml
<!-- 配置 -->
<properties>
  <!-- 项目的默认构建编码 -->
  <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  <!-- 编码版本 -->
  <maven.compiler.source>1.8</maven.compiler.source>
  <maven.compiler.target>1.8</maven.compiler.target>
</properties>
```

### 3.6. Maven 仓库的使用

> 地址：https://mvnrepository.com/

## 4、Servlet

### 4.1. Servlet 简介

- Servlet 就是 sun 公司开发动态 web 的一门技术
- Sun 公司在这些 API 中提供了一个接口叫做：Servlet 程序，只需要完成两个小步骤：
  - 编写一个类，实现 Servlet 接口
  - 把开发好的 Java 类部署到 web 服务器中

**把实现了 Servlet 接口的 Java 程序叫做 Servlet**

### 4.2. Servlet 生命周期

1. **生命周期**

   - 从出生到死亡的过程就是生命周期。对应 Servlet 中的三个方法：init(), service(), destroy()
2. **默认情况下：**

   - 第一次接受请求时，这个 Servlet 会进行实例化（调用构造方法）、初始化（调用 init()）、然后服务（调用 service()）
   - 第二次接受请求开示，每一次都是服务
   - 当容器关闭时，期中的所有的 servlet 实例就会被销毁，调用销毁方法。
3. **通过某个案例我们发现**

   - Servlet 实例 Tomcat 只会创建一个，所有的请求都是这个实例去响应。
   - 默认情况下，第一次请求时，Tomcat 才会去实例化，初始化，然后在服务。这样的好处是什么？提高系统的启动速度。
   - 因此得出结论：如果需要提高系统的启动速度，当前默认情况就是这样。如果需要提要响应速度，我们应该设置 Servlet 的初始化时机。
4. **Servlet 的初始化时机**

   - 默认是第一次接受请求时，实例化，初始化
   - 我们可以通过 ```<load-on-startup>``` 来设置启动的顺序， 数字越小，启动越靠前，最小值 0。

```
  <servlet>
      <load-on-startup>1</load-on-startup>
  </servlet>
```

5. **Servlet 在容器中是<u>单例</u>的、<u>线程不安全</u>的**
   - 单例：所有的请求都是同一个实例去响应
   - 线程不安全：一个线程需要根据这个实例中的某个成员变量值去做逻辑判断。但是在中间某个时机，另一个线程改变了这个变量的值，从而导致第一个线程的执行路径发生变化。
   - 启发：尽量不要在 servlet 中定义成员变量。

### 4.3. HelloServlet

Servlet 结构 Sun 公司有两个默认的实现类：HttpServlet，GenericServlet

1. 构建一个普通的 Maven 项目，删掉里面的 src 目录；这个空工程就是 Maven 主工程

2. 关于 Mave 父子工程的理解：

   父项目中会有：

   ```xml
   <modules>
   	<module>servlet-01</module>
   </modules>
   ```

   子项目中会有：

   ```xml
   <parent>
       <artifactId>javaweb-02-servlet</artifactId>
       <groupId>com.zero</groupId>
       <version>1.0.0.0</version>
   </parent>
   ```

   父项目中的 Java 子项目可以直接使用

   ```java
   son extends father
   ```

3. Maven 环境优化

   1. 修改 web.xml 为最新的
   2. 将 Maven 的结构搭建完整

### 4.4. Mapping 问题

1. 一个 Servlet 可以指定一个映射路径

   ```xml
   <servlet-mapping>
       <servlet-name>xxx</servlet-name>
       <url-pattern>/xxx</url-pattern>
   </servlet-mapping>
   ```

2. 一个 Servlet 可以指定多个映射路径

3. 一个 Servlet 可以指定通用映射路径

4. 指定一些后缀或者前缀等等

5. 优先级问题

   - 制定了固有的映射路径优先级最高，如果找不到就会走默认的处理请求。

### 4.5. ServletContext

- web 容器在启动的时候，他会为每个 web 程序都创建一个对应的 ServletContext 对象，他代表了当前的 Web 应用。
- 共享数据
  - 我在这个 Servlet 中保存的数据，可以在另一个 Servlet 中拿到；
- 请求转发

```java
ServletContext servletContext = this.getServletContext();
servletContext.getRequestDispatcher("/getc").forward(req, resp);
```

- 读取资源文件

  - Properties

    - 在 java 目录下新建 properties
    - 在 resources 目录下新建 properties

    发现：都被打包到了同一个路径下：classes，俗称为 classpath

  ```java
  InputStream resourceAsStream = this.getServletContext().getResourceAsStream("/WEB-INF/classes/db.properties");
  Properties properties = new Properties();
  properties.load(resourceAsStream);
  String username = properties.getProperty("username");
  String password = properties.getProperty("password");
  response.getWriter().println(username + " " + password);
  ```

### 4.6. HttpServletResponse

​	web 服务器接收到客户端的 http 请求，针对这个请求，分别创建一个代表请求的 HttpServletRequest 对象，代表响应的一个 HttpServletResponse;

- 如果要获取客户端请求过来的参数：HttpServletRequest
- 如果要给客户端响应一些信息：HttpServletResponse

#### 1. 简单分类

- 负责向浏览器发送数据的方法


```java
ServletOutputStream getOutputStream() throws IOException;
PrintWriter getWriter() throws IOException;
```

- 负责向浏览器发送响应头的方法

```java
void setCharacterEncoding(String var1);
void setContentLength(int var1);
void setContentLengthLong(long var1);
void setContentType(String var1);
void setDateHeader(String var1, long var2);
void addDateHeader(String var1, long var2);
void setHeader(String var1, String var2);
void addHeader(String var1, String var2);
void setIntHeader(String var1, int var2);
void addIntHeader(String var1, int var2);
```

#### 2. 常见应用

1. 向浏览器输出消息

2. 下载文件

   1. 获取下载文件的路径
   2. 获取下载的文件名
   3. 设置让浏览器支持下载
   4. 获取下载文件的输出流
   5. 创建缓冲区
   6. 获取 OutputStream 对象
   7. 将 FileOutPutStream 流写入到缓冲区
   8. 将 OutputStream 将缓冲区中的数据输入到客户端

   ```java
   String realPath = "D:\\Hodgepodge\\source\\Java\\JavaWeb\\javaweb-02-servlet\\response\\target\\classes\\img.png";
   String fileName = realPath.substring(realPath.lastIndexOf("\\") + 1);
   response.setHeader("Content-Disposition", "attachment;filename=" + URLEncoder.encode(fileName, "UTF-8"));
   FileInputStream fileInputStream = new FileInputStream(realPath);
   int len = 0;
   byte[] bytes = new byte[1024];
   ServletOutputStream outputStream = response.getOutputStream();
   while ((len = fileInputStream.read(bytes)) > 0) {
     	outputStream.write(bytes, 0, len);
   }
   fileInputStream.close();
   outputStream.close();
   ```

#### 3. 验证码功能

```java
//让浏览器 3 秒自动刷新一次
response.setHeader("refresh", "3");
//在内存中创建一个图片
BufferedImage bufferedImage = new BufferedImage(80, 20, BufferedImage.TYPE_INT_BGR);
Graphics2D graphics = (Graphics2D) bufferedImage.getGraphics();
graphics.setColor(Color.WHITE);
graphics.fillRect(0, 0, 80, 20);
//给图片写数据
graphics.setColor(Color.blue);
graphics.setFont(new Font(null, Font.BOLD, 20));
graphics.drawString(makeNum(), 0, 20);
//告诉浏览器，这个请求用图片的方式打开
response.setContentType("image/jpeg");
//网站存在缓存，不让浏览器缓存
response.setDateHeader("expires", -1);
response.setHeader("Cache-Control", "no-cache");
response.setHeader("Pragma", "no-cache");
ImageIO.write(bufferedImage, "jpeg", response.getOutputStream());
```

#### 4. 实现重定向

```java
/*
response.setHeader("Location", "/response_war_exploded/image");
response.setStatus(302);
*/
response.sendRedirect("/response_war_exploded/image");
```

- 重定向与转发的区别
- 相同点
  - 页面都会实现跳转
- 不同点
  - 请求转发的时候，URL 不会发生变化
  - 重定向时候，URL 地址栏会发生变化

### 4.7. HttpServletRequest

#### 1. 获取前端传递的参数

#### 2. 请求转发

## 5、Cookie、Session

### 5.1. 会话

- **会话**：用户打开一个浏览器，点击了很多超链接，访问多个 Web 资源，关闭浏览器，该过程称之为会话
- **有状态会话**

### 5.2. 保存会话的两种技术

**cookie**

- 客户端技术（响应，请求）

session

- 服务器技术，利用这个技术，可以保存用户的回话信息？我们可以把信息或者数据放在 Session 中

### 5.3. Cookie

1. 从请求中拿到 Cookie 信息
2. 服务器响应给客户端 Cookie

```java
Cookie[] cookies = request.getCookies();  			//获得 Cookie
cookies.getName(); 								  //获得 cookie 中的 key
cookies.getValue();								  //获得 cookie 中的 value
```

- cookie：一般保存在本地的用户目录下 APPData 中

### 5.3. Session

1. HTTP 是**无状态**的
   - HTTP 无状态：服务器无法判断这两次请求是同一个客户端发过来的，还是不同的客户端发过来的。
   - 无状态带来的显示问题：第一次请求时添加商品到购物车，第二次请求是结账；如果这两次请求服务器无法区分是同一个用户的，那么就会导致混乱。
   - 通过回话跟踪技术来解决无状态的问题。
2. **回话跟踪技术**
   - 客户端第一次发请求给服务器，服务器获取 session，获取不到，则创建新的，然后响应给客户端。
   - 下次客户端给服务器发请求时，会把 sessionID 带给服务器，那么服务器就能获取到，那么服务器就判断这次请求和上次请求是同一个客户端，从而能够区分开客户端。
   - 常用的 API ：
     - request.getSession() -> 获取当前的会话，没有则创建一个新的会话
     - request.getSession(true) -> 效果同上
     - request.getSession(false) -> 回去当前会话，没有则返回 null ，不会创建新的
     - session.getId() -> 获取 sessionID
     - session.isNew() -> 判断当前 session 是否是新的
     - session.getMaxInactiveInterval() -> session 的非激活间隔时长，默认1800s
     - session.setMaxInactiveInterval()
     - session.invalidate() -> 强制性让会话立即失效
     - ....
3. session **保存作用域**
   - session 保存作用域是和具体的某一个 session 对应的
   - 常用的 API ：
     - void session.setAttribute(k, v);
     - Object session.getAttribute(k);
     - void removeAttribute(k);

## 6、什么是业务层

1. Model1 和 Model2

   - 视图层：用于做数据展示以及和用户交互的一个界面。
     控制层：能够接受客户端的请求，具体的业务功能还是需要借助于模型组件来完成。
     模型层：模型分为很多种：有比较简单的 pojo/vo(value object)，有业务模型组件，有数据访问层组件。

     ```
     1) pojo/vo : 值对象
     2) DAO ： 数据访问对象
     3) BO ： 业务对象
     ```

2. 区分业务对象和数据访问对象

   - DAO 中的方法都是单精度方法或者称之为细粒度方法。什么叫单精度？一个方法只考虑一个操作，比如添加，那就是insert操作、查询那就是select操作....
   - BO 中的方法属于业务方法，也实际的业务是比较复杂的，因此业务方法的粒度是比较粗的注册这个功能属于业务功能，也就是说注册这个方法属于业务方法。
   - 那么这个业务方法中包含了多个 DAO 方法。也就是说注册这个业务功能需要通过多个 DAO 方法的组合调用，从而完成注册功能的开发。
     - 注册：
       1. 检查用户名是否已经被注册 - DAO 中的 select 操作。
       2. 向用户表新增一条新用户记录 - DAO 中的 insert 操作。
       3. 向用户积分表新增一条记录（新用户默认初始化积分100分） - DAO 中的 insert 操作。
       4. 向系统消息表新增一条记录（某某某新用户注册了，需要根据通讯录信息向他的联系人推送消息） - DAO 中的 insert 操作。
       5. 向系统日志表新增一条记录（某用户在某IP在某年某月某日某时某分某秒某毫秒注册） - DAO 中的 insert 操作。
       6. .......

3. 在库存系统中添加业务层组件。

## 7、MVC

- V : view 视图；C：Controller 控制器；M：Model 模型
- 数据访问模型（DAO）、业务逻辑模型（BO）、值对象模型（POJO）、数据传输模型（DTO）

## 8、IOC

1. 耦合/依赖
   - 依赖指的是某某某离不开某某某
   - 在软件系统中，层与层之间是存在依赖的。我们也称之为耦合。  
   - 我们系统架构或者是设计的一个原则是： 高内聚低耦合。
   - 层内部的组成应该是高度聚合的，而层与层之间的关系应该是低耦合的，最理想的情况0耦合（就是没有耦合）
2. IOC - 控制反转 / DI - 依赖注入.
   - 控制反转：控制权从程序员到 BeanFactory。
   - 依赖注入：从主动获取到配置文件解析容器获取

## 9、过滤器 Filter

1. Filter也属于Servlet规范
2. Filter开发步骤：新建类实现 Filter 接口，然后实现其中的三个方法：init、doFilter、destroy 配置 Filter，可以用注解 @WebFilter，也可以使用 xml 文件 <filter><filter-mapping>
3. Filter 在配置时，和 servlet 一样，也可以配置通配符，例如 @WebFilter("*.do") 表示拦截所有以 .do 结尾的请求
4. 过滤器链
   1. 执行的顺序依次是： A B C demo03 C2 B2 A2
   2. 如果采取的是注解的方式进行配置，那么过滤器链的拦截顺序是按照全类名的先后顺序排序的
   3. 如果采取的是 xml 的方式进行配置，那么按照配置的先后顺序进行排序

## 10、监听器

1. ServletContextListener - 监听ServletContext对象的创建和销毁的过程
2. HttpSessionListener - 监听HttpSession对象的创建和销毁的过程
3. ServletRequestListener - 监听ServletRequest对象的创建和销毁的过程
4. ServletContextAttributeListener - 监听ServletContext的保存作用域的改动(add,remove,replace)
5. HttpSessionAttributeListener - 监听HttpSession的保存作用域的改动(add,remove,replace)
6. ServletRequestAttributeListener - 监听ServletRequest的保存作用域的改动(add,remove,replace)
7. HttpSessionBindingListener - 监听某个对象在Session域中的创建与移除
8. HttpSessionActivationListener - 监听某个对象在Session域中的序列化和反序列化

## 11、XML

1. XML 包含三个部分

   - XML 声明，而且声明这一行代码必须在 XML 文件的第一行

     - ```<?xml version="1.0" encoding="utf-8"?>```

   - DTD 文档类型定义

   - XML 正文

     ```xml
       <beans>
         <!-- 这个 bean 标签的作用是将来 servletpath 中涉及的名字对应的是fruit -->
         <!-- 那么就要 FruitController -->
       	<bean id="fruit" class="com.....FruitController"/>
       </beans>
     ```
