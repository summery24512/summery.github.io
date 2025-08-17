---
layout:      post
title:       "第一次博客尝试"
author:      "summery"
header-style:  text
catalog：      true
tags:
  - web
  - JavaScipt
---
关于系统架构
C/S即为用户下载下来的软件，B/S即为用户输入网址访问的网页
C/S结构
优点:
1.速度快(大量的数据都是集成在客户端软件当中，所以服务器只需要传送很少的数据量)
2.服务器压力小(大量的数据都是集成在客户端软件当中，所以服务器只需要传送很少的数据量)
3.安全(大量的数据都是集成在客户端软件当中,数据在多个客户端上有缓存)
缺点:
升级维护比较差劲(每一个客户端都需要升级)
B/S架构
优点:
升级维护方便，成本比较低。（只需要升级服务器端即可。）
不需要安装特定的客户端软件,只需要打开浏览器，输入网址即可。
缺点:
速度慢(所有的数据都是在服务器上，用户发送的每一个请求都需要服务器来响应数据)
不安全(更改服务器数据后所有用户访问的数据都会更改)
B/S结构的系统通信原理
域名
https://www.baidu.com/(网站)，www.baidu.com 是一个域名
在浏览器地址栏上输入域名，回车之后，域名解析器会将域名解析出来一个具体的IP地址和端口号等。
解析结果也许是：http://110.242.68.3:80/index.html

IP地址:  一台主机的身份证号
端口号:  一个软件
Web系统的通信原理
● 第一步：用户输入网址（URL）
● 域名解析器进行域名解析：110.242.68.3:80/index.html
● 浏览器软件在网络中搜索并找到110.242.68.3这一台主机
● 该台主机定位到80端口对应的服务器软件
● 80端口对应的服务器软件得知浏览器想要的资源名是：index.html
● 服务器软件找到index.html文件，并且将index.html文件中的内容直接输出响应到浏览器上。
● 浏览器接收并执行到来自服务器的代码（HTML CSS JS）
各部分起到的作用

SUN公司负责制定Servlet规范(通过创建接口的方式)
各大webapp的开发团队实现SUN公司发布的接口，创建类去实现该接口
Tomcat负责根据用户不同的请求路径，来寻找对应的XXXservlet，根据反射机制来创建对应的对象
这个配置文件的文件名不能乱来。固定的。
这个配置文件的存放路径不能乱来。固定的。
servlet规范中规定了：
● 一个合格的webapp应该是一个怎样的目录结构。
● 一个合格的webapp应该有一个怎样的配置文件。
● 一个合格的webapp配置文件路径放在哪里。
● 一个合格的webapp中java程序放在哪里。
● 这些都是Servlet规范中规定的。
● Tomcat服务器要遵循Servlet规范。JavaWEB程序员也要遵循这个Servlet规范。这样Tomcat服务器和webapp才能解耦合。
使用IDEA开发一个Servlet的web
第一步：基础搭建

添加模块
双击Shift	---->Add Framework Support..(添加框架支持)------>选择Web Application

导入依赖
<dependency>
    <groupId>jakarta.servlet</groupId>
    <artifactId>jakarta.servlet-api</artifactId>
    <version>6.0.0</version>
    <scope>provided</scope>
</dependency>
第二步：编写Servlet
实现jakarta.servlet.Servlet接口中的5个方法。

第三步:在web.xml文件中完成StudentServlet类的注册
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">


    <servlet>
        <servlet-name>studentServlet</servlet-name>
        <servlet-class>com.bjpowernode.javaweb.servlet.StudentServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>studentServlet</servlet-name>
        <url-pattern>/servlet/student</url-pattern>
    </servlet-mapping>
</web-app>
第四步:给一个html页面，在HTML页面中编写一个超链接
● student.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<!--这里的项目名是 /xmm ，无法动态获取，先写死-->
<a href="/xmm/servlet/student">student list</a>
</body>
</html>
第五步：让IDEA工具去关联Tomcat服务器。
1.Add Configuration
2.左上角加号，点击Tomcat Server --> local

3.Deployment（点击这个用来部署webapp），继续点击加号，部署即可。修改 Application context为：/xmm

第六步:启动tom服务器，浏览器输入地址
打开浏览器，在浏览器地址栏上输入：http://localhost:8080/xmm/student.html

注意:前端发送请求要加项目名

三.Http协议
HTTP协议：是W3C制定的一种超文本传输协议。（通信协议：发送消息的模板提前被制定好。)
● HTTP协议包括： 
  ○ 请求协议 
    ■ 浏览器  向   WEB服务器发送数据的时候，这个发送的数据需要遵循一套标准，这套标准中规定了发送的数据具体格式。
  ○ 响应协议 
    ■ WEB服务器  向  浏览器发送数据的时候，这个发送的数据需要遵循一套标准，这套标准中规定了发送的数据具体格式。

 1.HTTP的请求协议（B --> S） 
  ○  HTTP的请求协议包括：
    ■ 请求行
    ■ 请求头
    ■ 空白行
    ■ 请求体
  ○  HTTP请求协议的具体报文：GET请求 
GET /servlet05/getServlet?username=lucy&userpwd=1111 HTTP/1.1                       请求行
Host: localhost:8080                                                                请求头
Connection: keep-alive
sec-ch-ua: "Google Chrome";v="95", "Chromium";v="95", ";Not A Brand";v="99"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.54 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: http://localhost:8080/servlet05/index.html
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
                                                                                    空白行
                                                                                    请求体
HTTP请求协议的具体报文：POST请求 


POST /servlet05/postServlet HTTP/1.1                                              请求行
Host: localhost:8080                                                              请求头
Connection: keep-alive
Content-Length: 25
Cache-Control: max-age=0
sec-ch-ua: "Google Chrome";v="95", "Chromium";v="95", ";Not A Brand";v="99"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
Origin: http://localhost:8080
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/95.0.4638.54 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: http://localhost:8080/servlet05/index.html
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
                                                                                  空白行
username=lisi&userpwd=123                                                         请求体
  ○  请求行 
    ■ 包括三部分： 
      ● 第一部分：请求方式（7种） 
        ○ get（常用的）
        ○ post（常用的）
        ○ delete
        ○ put
        ○ head
        ○ options
        ○ trace
      ● 第二部分：URI 
        ○ 什么是URI？ 统一资源标识符。代表网络中某个资源的名字。但是通过URI是无法定位资源的。
        ○ 什么是URL？统一资源定位符。代表网络中某个资源，同时，通过URL是可以定位到该资源的。
        ○ URI和URL什么关系，有什么区别？ 
          ■ URL包括URI
          ■ http://localhost:8080/servlet05/index.html 这是URL。
          ■ /servlet05/index.html 这是URI。
      ● 第三部分：HTTP协议版本号
  ○  请求头 
    ■ 请求的主机
    ■ 主机的端口
    ■ 浏览器信息
    ■ 平台信息
    ■ cookie等信息
    ■ ....
  ○  空白行 
    ■ 空白行是用来区分“请求头”和“请求体”
  ○  请求体 
    ■ 向服务器发送的具体数据。
2. HTTP的响应协议（S --> B） 
  ○  HTTP的响应协议包括：4部分 
    ■ 状态行
    ■ 响应头
    ■ 空白行
    ■ 响应体
  ○  HTTP响应协议的具体报文： 
HTTP/1.1 200 ok                                     状态行
Content-Type: text/html;charset=UTF-8               响应头
Content-Length: 160
Date: Mon, 08 Nov 2021 13:19:32 GMT
Keep-Alive: timeout=20
Connection: keep-alive
                                                    空白行
<!doctype html>                                     响应体
<html>
    <head>
        <title>from get servlet</title>
    </head>
    <body>
        <h1>from get servlet</h1>
    </body>
</html>
● 状态行:
● 三部分组成 
    ■ 第一部分：协议版本号（HTTP/1.1）
    ■ 第二部分：状态码（HTTP协议中规定的响应状态号。不同的响应结果对应不同的号码。） 
      ● 2.分类：
● **1xx: 信息响应：**这类响应结果不是很常见
  ○ 100 Continue: 服务器已接收请求头，客户端应继续发送请求主体。
  ○ 101 Switching Protocols: 服务器同意切换协议。
● **2xx: 成功：**这类状态码基本都是请求成功。
  ○ 200 OK: 请求成功，服务器已返回请求的数据。
  ○ 201 Created: 请求已成功，并且服务器创建了新的资源。
  ○ 202 Accepted: 服务器已接受请求，但尚未处理。
  ○ 204 No Content: 请求成功但无返回内容。
● **3xx: 重定向：**这类状态码一般是用于告诉浏览器请求的站点已经被移动到其他地址了，需要更换到新的地址。
  ○ 301 Moved Permanently: 请求的资源已被永久移动到新URL。
  ○ 302 Found: 请求的资源临时被移动到新URL。
  ○ 304 Not Modified: 资源未被修改，可以使用缓存的版本。
● **4xx: 客户端错误：**这类状态码在我们后续学习中会经常碰到，基本都是由于浏览器发送的请求少携带了什么数据或是请求有问题之类的。
  ○ 400 Bad Request: 服务器无法理解请求的格式。
  ○ 401 Unauthorized: 请求需要用户认证。
  ○ 403 Forbidden: 服务器拒绝请求。
  ○ 404 Not Found: 服务器找不到请求的资源。
  ○ 405 Method Not Allowed: 请求方法被禁用。
  ○ 429 Too Many Requests: 客户端在给定的时间内发送了太多请求。
● **5xx: 服务器错误：**这类状态码也会在外面后续学习中经常碰到，基本都是由于服务端出现错误导致的。
  ○ 500 Internal Server Error: 服务器内部错误。
  ○ 501 Not Implemented: 服务器不支持请求的功能。
  ○ 502 Bad Gateway: 网关或代理服务器收到无效响应。
  ○ 503 Service Unavailable: 服务器暂时无法处理请求（超负载或维护）。
  ○ 504 Gateway Timeout: 网关或代理服务器未及时收到上游服务器的响应。
● 响应头： 
    ■ 响应的内容类型
    ■ 响应的内容长度
    ■ 响应的时间
    ■ ....
● 空白行： 
    ■ 用来分隔“响应头”和“响应体”的。
● 响应体： 		
    ■ 响应体就是响应的正文，这些内容是一个长的字符串，这个字符串被浏览器渲染，解释并执行，最终展示出效果。
●  怎么向服务器发送GET请求，怎么向服务器发送POST请求？ 
  ○ 到目前为止，只有一种情况可以发送POST请求：使用form表单，并且form标签中的method属性值为：method="post"。
3.GET和POST有什么区别?
● 怎么向服务器发送GET请求，怎么向服务器发送POST请求？ 
  ○ 到目前为止，只有一种情况可以发送POST请求：使用form表单，并且form标签中的method属性值为：method="post"。
● GET请求和POST请求有什么区别？   
● （get请求在“请求行”上发送数据） get请求发送数据的时候，数据会挂在URI的后面，并且在URI后面添加一个“?”，"?"后面是数据。这样会导致发送的数据显示浏览器的地址栏上。
  ○ http://localhost:8080/servlet05/getServlet?username=zhangsan&userpwd=1111
● （post请求在“请求体”当中发送数据）post请求发送数据时在请求体中发送，不会回显到浏览器的地址栏上
● 发送内容上的区别
  ○ get请求只能发送普通的字符串。并且发送的字符串长度有限制，不同的浏览器限制不同。
  ○ get请求无法发送大数据量。
  ○ post请求可以发送任何类型的数据，包括普通字符串，流媒体等信息：视频、声音、图片。
  ○ post请求可以发送大数据量，理论上没有长度限制。
● 适用情况的区别
  ○ get请求在W3C中是这样说的：get请求比较适合从服务器端获取数据。
  ○ post请求在W3C中是这样说的：post请求比较适合向服务器端传送数据。
● 数据安全性（正确使用的前提下）
  ○ get请求是安全的。get请求是绝对安全的。为什么？因为get请求只是为了从服务器上获取数据。不会对服务器造成威胁。
  ○ post请求是危险的。为什么？因为post请求是向服务器提交数据，如果这些数据通过后门的方式进入到服务器当中，服务器是很危险的。另外post是为了提交数据，所以一般情况下拦截请求的时候，大部分会选择拦截（监听）post请求。
● 是否支持缓存
  ○ get请求支持缓存。 
    ■ 实际上，你只要发送get请求，浏览器做的第一件事都是先从本地浏览器缓存中找，找不到的时候才会去服务器上获取。这种缓存机制目的是为了提高用户的体验。
  ○ post请求不支持缓存。（POST是用来修改服务器端的资源的.)
● Get请求和POST请求如何选择？
  ○ 如果想从服务器获取资源，建议使用GET请求，如果这个请求是为了向服务器提交数据，建议使用POST请求
  ○ 大部分的form表单提交都是post方式，因为form表单中要填写大量的数据，这些数据时手机用户信息，一般需要传给服务器，服务器将数据保存/修改
  ○ 如果表单有敏感信息，建议使用post请求，因为get请求会回显信息到地址栏上（如：密码信息）
  ○ 做文件上传时一定是post请求，因为传输的数据不是普通文本
  ○ 其他情况都可以使用GET请求
