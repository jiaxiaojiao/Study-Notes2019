## JSP的四大作用域对象

域对象 | 数据类型 | 描述
---|---|---
pageContext | PageContext | 当前JSP作用域对象
request | HttpServletRequest | 当前请求对象
session | HttpSession | 当前会话对象 必须设置JSP: Session=true
application | ServletContext | 当前应用对象

## JSP 9大内置对象
在JSP中预先定义好的，可以直接拿来使用的对象

内置对象 | 数据类型 | 描述
---|---|---
pageContext | PageContext | 当前JSP作用域对象
request | HttpServletRequest | 请求对象
session | HttpSession | 会话对象 必须设置JSP  session=true
application | ServletContext | 当前应用对象
response | HttpServletResponce | 响应对象
config | ServletConfig | 当前JSP的配置对象
out | JspWriter | 输出流对象
page | Object | 当前JSP/Servlet对象，没有实际意义
exception | Throwble | 异常对象 必须设置当前JSP isErrorPage=true

#### JSP/Servlet



#### 传值
- [页面向后端传值](./java/byval.md)