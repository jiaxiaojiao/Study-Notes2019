[extjs 中文网站](http://extjs.org.cn/)

[Ext4.1.0 api](http://extjs-doc-cn.github.io/ext4api/)

[ExtJs csdn 整理](https://blog.csdn.net/qq_17505335/article/category/6302431)

[ExtJs csdn整理2](https://blog.csdn.net/suyu_yuan/article/category/6455028)

[ExtJs cnblogs 整理](https://www.cnblogs.com/niejunchan/category/757717.html)

[ExtJs cnblogs 整理2](https://www.cnblogs.com/knowledgesea/category/509956.html)

[extjs w3cschool](https://www.w3cschool.cn/extjs/extjs_overview.html)

```text
什么是Ext Js？
流行的JavaScript框架。
基本用于创建桌面应用程序。

历史版本
Ext JS 1.1
2006
Ext JS 2.0
2007 功能有限。
Ext JS 3.0
2009 速度差。
Ext JS 4.0
2011 基于MVC架构。
Ext JS 5.0
2014 基于MVVM机构。
Ext JS 6.0
2016 合并了Ext Js(用于桌面应用程序) sencha touch(用于移动应用程序) 框架。

特征
这些是Ext JS的突出特性
可定制的UI小部件与丰富的UI集合，如网格，枢轴网格，表单，图表，树木。
新版本与旧版本的代码兼容性。
灵活的布局管理器有助于组织跨多个浏览器，设备和屏幕大小的数据和内容显示。
高级数据包将UI小部件与数据层分离。 数据包允许客户端使用高度功能的模型收集数据，这些模型支持排序和过滤等功能。
它是协议不可知的，并且可以从任何后端源访问数据。
可定制的主题Ext JS窗口小部件提供了跨平台一致的多个现成主题。
好处
Sencha Ext JS是业务级Web应用程序开发的领先标准。 Ext JS提供了为桌面和平板电脑构建强大应用程序所需的工具。
简化针对现代和传统浏览器的跨平台开发，跨桌面，平板电脑和智能手机。
通过IDE插件集成到企业开发环境中，提高开发团队的生产力。
降低Web应用程序开发的成本。
授权团队创建具有吸引力的用户体验的应用程序。
它有一组小部件使UI强大和容易。
它遵循MVC架构这样高度可读的代码。
限制
库的大小大约500 KB，这使得初始加载时间更多，并使应用程序缓慢。
HTML已满
标签使其复杂和难以调试。
根据一般公共许可政策，它是免费的开源应用程序，但支付商业应用程序。
有些时候加载甚至简单的东西需要很少的代码行，这在简单的html或Jquery更简单。
需要相当经验的开发人员开发Ext JS应用程序。
工具
这些是sencha提供的用于Ext JS应用程序开发的工具，主要用于生产级别。
Sencha Cmd
Sencha CMD是一个提供Ext JS代码缩小，脚手架，生产构建生成功能的工具。
Sencha IDE Plugins
Sencha IDE插件，它将Sencha框架集成到IntelliJ，WebStorm IDE中。 这有助于通过提供代码完成，代码检查，代码导航，代码生成，代码重构，模板创建和拼写检查等功能来提高开发人员的生产力。
Sencha Inspector
Sencha Inspector是一个调试工具，帮助调试器调试任何问题，同时开发。
```

###### 1. 类的命名规范
类名仅可包含字母、数字。数字大多数情况下不推荐使用，除非是在一些技术术语中。不要使用中划线、下划线等非字符。
```
MyCompany.useful_util.Debug_Toolbar //不要使用下划线 
MyCompany.util.Base64 //技术术语可以包含数字 
```

类应该通过正确命名的“包（Packages）”来组织。最小包情况时，类名应该紧随最顶层的“名字空间（Namespace）”：
```
MyCompany.data.CoolProxy //“包”通过“.”来组织 
MyCompany.Application //最小包情况
```

最顶层的“名字空间（Namespaces）”和“类名（ClassNames）”应该使用“驼峰命名法（CamelCased）”，其他都是用小写字母：

```
MyCompany.form.action.AutoLoad
```

非Sencha官方发布的类，不要使用“Ext”作为最顶层名字空间。
缩写词也要遵守“驼峰命名法（CamelCased）” ：

```
Ext.data.JSONProxy 替换为Ext.data.JsonProxy
MyCompary.parser.HTMLParser 替换为 MyCompany.util.HtmlParser
MyCompany.server.HTTP 替换为MyCompany.server.Http
```



###### 2. 源文件的命名规则
类名直接映射到文件存储路径，每个类一个文件：
```
Ext.util.Observable 存储在 path/to/src/Ext/util/Observable.js 
Ext.form.action.Submit 存储在 path/to/src/Ext/form/action/Submit.js 
MyOrg.chart.axis.Numeric 存储在 path/to/src/MyOrg/chart/axis/Numeric.js
```

###### 3. 方法和变量的命名规则

方法和变量命名同类一样，仅可包含字母、数字。数字大多数情况下不推荐使用，除非是在一些技术术语中。不要使用中划线、下划线等非字符； 
方法和变量命名应该使用“驼峰命名法（CamelCased）”，缩写词也一样；
```
encodeUsingMd5() //技术术语可以包含数字 
getHTML()  //替换为getHtml() 
getJSONResponse()   //替换为getJsonResponse()  
parseXMLContent()   //替换为parseXmlContent()
var isGoodName
var base64Encoder //技术术语可以包含数字
var xmlReader 
var httpServer 
```

###### 4. 属性的命名规则
```
非静态的类属性命名规则同上；
静态的类属性命名全部使用大写字母：
```
