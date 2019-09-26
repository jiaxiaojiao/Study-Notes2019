# Servlet

## 什么是Servlet
> Servlet是采用Java语言编写的服务器端程序，它运行于Web服务器中的Servlet容器中，主要的功能是提供请求/响应的Web服务模式，可以生成动态的Web内容。

优点：
1. 较好的移植性。Java语言跨平台。
2. 执行效率高。针对每个请求创建一个线程来执行。
3. 功能强大。与Web服务器交互。
4. 使用方便。提供了接口来读取或设置HTTP头消息，处理Cookie和跟踪回话状态等。
5. 可扩展性强。Java面向对象。

## Servlet处理客户端请求的步骤。
1. 用户通过一个连接来向Servlet发起请求。
2. Web服务器收到请求后，会把请求交给响应的容器来处理，当容器发现这是对Servlet发起的请求后，容器此时会创建两个对象：HttpServletResponse，HttpServletRequest。
3. 容器根据请求消息中的URL消息找到对应的Servlet，然后针对该请求创建一个单独的线程。
4. 容器调用Servlet的service()方法来完成对用户请求的响应。service()方法会调用doPost() doGet来完成具体的响应任务。同时把生成的动态页面返回给容器。
    1. 当HTTP请求中的method属性为get时，调用doGet()方法。
    2. 当method属性为post时，调用doPost()方法
5. 容器把响应消息组装成HTTP格式返回给客户端。线程结束，删除对象HttpServletResponse，HttpServletRequest。

## Servlet生命周期。
Servlet运行在容器中，整个生命周期都是由容器来控制的。
1. 加载。 类加载器使用Servlet类对应的文件来加载Servlet。
2. 创建。调用Servlet构造函数创建Servlet实例。
3. 初始化。init()。 只会被调用一次
4. 处理客户请求。doGet() doPost()
5. 卸载。destroy()

## Servlet中的forward和redirect
forward 服务器内部重定向。

redirect 客户端的重定向。跳转。