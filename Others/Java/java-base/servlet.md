

用Java编写的服务器端程序，
主要功能是交互式的浏览和修改数据，动态生成web内容。
运行在支持Java的应用服务器中。

HttpServlet 重写doGet doPost方法

生命周期？
加载、实例化、初始化、处理请求、服务结束
javax.servlet.Servlet接口的init service destrory方法表达

加载Servlet的class ==> 实例化Servlet ==> 调用init完成初始化 ==> 响应请求 ==> 容器关闭Servlet的destroy方法。
