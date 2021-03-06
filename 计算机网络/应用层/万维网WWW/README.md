# 万维网WWW

## 万维网概述
World Wide Web万维网。是一个分布式的超媒体hypermedia, 他是超文本(hyperText)系统的扩充。
所谓的hypertext就是包含指向其他其他文档的连接的文本，一个超文本由多个信息源链接成。
也就是说，利用一个连接可以使用户找到另一个文档，以此类推，也可以找到别的文档。
几个问题：
* 怎么标志分布在整个因特网上的万维网文档。
```
使用统一资源定位符URL
```
* 用什么协议来实现万维网上各种链接。
```
超文本传送协议HTTP
```
* 创作不同风格的万维网文档
```
超文本标记语言HTML
```

## URL

### URL格式
URL相当于一个文件名在网络范围的扩展。可以类化成一个指针。
一般分为四个部分：
```JavaScript
<协议>://<主机>:<端口>/<路径>
```
* 协议
```
指出用什么协议来获取该万维网文档
```
* 主机
```
域名
```
* 端口
```
有时可省略
```
* 路径

## 超文本传送协议HTTP

### 超文本传送协议HTTP的操作过程
HTTP协议定义了浏览器(即WWW客户进程)怎么向万维网服务器请求万维网文档，以及服务器怎么把文档传送给浏览器。
从层次上看，HTTP是面向事务的(transaction-oriented)应用层协议。所谓事务，是指一系列的信息交换，而且这一系列的信息交换是一个不可分割的整体。
```
每个万维网网点都有一个服务器进程。它不断监听TCP的端口80。
一旦监听到连接建立请求并建立了TCP连接。
浏览器就向万维网服务器发出请求，服务器返回所请求的页面作为响应。
最后TCP被释放。
```
HTTP使用了面相连接的TCP作为运输层协议，保证数据的可靠传输。
* `HTTP本身是无连接的`。通信的双方在交换HTTP报文之前不需要先建立HTTP连接。
* `HTTP是无状态的`。服务器不会记得曾经访问过的客户。->简化了HTTP的设计。
```
HTTP／1.1解决了HTTP／1.0一些连接耗时的问题，使用了`持续连接`，因为每次请求资源都需要花费很多时间在TCP连接上。
所以HTTP／1.1使用了持续连接，在服务器发送响应后，仍然在一段时间内保持这条连接。
```
### HTTP/1.1
HTTP／1.1的持续连接有两种工作方式。
* 非流水线方式(without pipeling)
```
特点：客户在受到前一个响应后，才能发出下一个请求。
虽然节省了一个TCP的连接时间，但是每次访问一次对象都要等一个往返时间。
```
* 流水线方式
```
特点：客户在收到响应之前，还可以持续发送。
```
### 代理服务器
代理服务器(proxy server)是一种网络实体，又称为万维网高速缓存(web cache)。
代理服务器吧最近的一些请求和响应暂存在本地磁盘中。当新请求到达，如果这个与暂存的相同，就返回暂存的响应。不用每次都按URL地址去访问资源。

### HTTP报文结构
两类报文：
* 请求报文
* 响应报文
因为HTTP是面向文本的，因此报文中每一个字段都是一些ASCII码串，因此长度不确定。
分三部分组成：
* 开始行
```
请求报文：请求行：包括方法，URL，HTTP版本
响应报文：状态行：包括HTTP版本，状态码，解析状态码的简单短语。
```
* 首部行

* 实体主体

### 在服务器上存放用户的信息
由于HTTP是无状态的，如果希望万维网能识别用户，可以在HTTP上使用cookie。
cookie的工作流程：
```
当某个用户浏览某个使用cookie的网站时，该网站的服务器就为该用户产生一个唯一的识别码。
接着给该用户的响应报文中添加一个set-cookie的首部行。例如set-cookie: 123456,这就是唯一的识别码。
当用户收到这个响应报文后，其浏览器就在它管理的特定cookie文件中添加一行，其中包括:服务器的主机名和set-cookie后面给出的识别码。
当该用户继续浏览这个网站时，每发送一个HTTP请求报文，其浏览器就会从其cookie文件中取出这个网站的识别码，并放到HTTP请求报文的cookie首部行中：
例如 Cookie: 123456
那么服务器就会知道用户的浏览信息。
```
