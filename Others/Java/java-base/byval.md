# 页面传值

## SringMVC接收复杂集合参数
Spring MVC在接收集合请求参数时，需要在Controller方法的集合参数里前添加@RequestBody，而@RequestBody默认接收的enctype (MIME编码)是application/json，因此发送POST请求时需要设置请求报文头信息，否则Spring MVC在解析集合请求参数时不会自动的转换成JSON数据再解析成相应的集合。以下列举接收List<String>、List<User>、List<Map<String,Object>>、User[]、User(bean里面包含List)几种较为复杂的集合参数示例：
### 接收List<String>集合参数：

页面js代码
```jsp
var idList = new Array();  
idList.push(“1”);   
idList.push(“2”);   
idList.push(“3”);  
var isBatch = false;  
$.ajax({  
    type: "POST",  
    url: "<%=path%>/catalog.do?fn=deleteCatalogSchemes",  
    dataType: 'json',  
    data: {"idList":idList,"isBatch":isBatch},  
    success: function(data){  
        …  
    },  
    error: function(res){  
        …  
    }  
});
```
Controller方法：
```text
@Controller
@RequestMapping("/catalog.do")
public class CatalogController {
  
    @RequestMapping(params = "fn=deleteCatalogSchemes")
    @ResponseBody
    public AjaxJson deleteCatalogSchemes(@RequestParam("idList[]") List<String> idList,Boolean isBatch) {
            …
    }
}
```

### 接收List<User>、User[]集合参数：

User实体类：
```text
public class User {
    private String name;
    private String pwd;
    //省略getter/setter
}
```

页面js代码
```jsp
var userList = new Array();  
userList.push({name: "李四",pwd: "123"});   
userList.push({name: "张三",pwd: "332"});   
$.ajax({  
    type: "POST",  
    url: "<%=path%>/catalog.do?fn=saveUsers",  
    data: JSON.stringify(userList),//将对象序列化成JSON字符串  
    dataType:"json",  
    contentType : 'application/json;charset=utf-8', //设置请求头信息  
    success: function(data){  
        …  
    },  
    error: function(res){
        …
    }
});
```

Controller方法：
```text
@Controller  
@RequestMapping("/catalog.do")  
public class CatalogController {  
  
    @RequestMapping(params = "fn=saveUsers")
    @ResponseBody
    public AjaxJson saveUsers(@RequestBody List<User> userList) {
        …
    }
}
```
如果想要接收User[]数组，只需要把saveUsers的参数类型改为@RequestBody User[] userArray就行了。

### 接收List<Map<String,Object>>集合参数

页面js代码（不需要User对象了）
```jsp
var userList = new Array();  
userList.push({name: "李四",pwd: "123"});   
userList.push({name: "张三",pwd: "332"});   
$.ajax({  
    type: "POST",  
    url: "<%=path%>/catalog.do?fn=saveUsers",  
    data: JSON.stringify(userList),//将对象序列化成JSON字符串  
    dataType:"json",  
    contentType : 'application/json;charset=utf-8', //设置请求头信息  
    success: function(data){  
        …  
    },  
    error: function(res){  
        …  
    }  
});
```
Controller方法
```text
@Controller  
@RequestMapping("/catalog.do")  
public class CatalogController {  
  
    @RequestMapping(params = "fn=saveUsers")  
    @ResponseBody  
    public AjaxJson saveUsers(@RequestBody List<Map<String,Object>> listMap) {  
        …  
    }  
}
```

### 接收User(bean里面包含List)集合参数

User实体类
```text
public class User {  
    private String name;   
    private String pwd;  
    private List<User> customers;//属于用户的客户群  
    //省略getter/setter  
}
```
页面js代码
```jsp
var customerArray = new Array();  
customerArray.push({name: "李四",pwd: "123"});   
customerArray.push({name: "张三",pwd: "332"});   
var user = {};  
user.name = "李刚";  
user.pwd = "888";  
user. customers = customerArray;  
$.ajax({  
    type: "POST",  
    url: "<%=path%>/catalog.do?fn=saveUsers",  
    data: JSON.stringify(user),//将对象序列化成JSON字符串  
    dataType:"json",  
    contentType : 'application/json;charset=utf-8', //设置请求头信息  
    success: function(data){  
        …  
    },  
    error: function(res){  
        …  
    }  
});
```

Controller方法
```jsp
@Controller  
@RequestMapping("/catalog.do")  
public class CatalogController {  
  
    @RequestMapping(params = "fn=saveUsers")  
    @ResponseBody  
    public AjaxJson saveUsers(@RequestBody User user) {  
        List<User> customers = user.getCustomers();  
        …  
    }  
}
```

## 参考
- [ajax传参数组,spring boot 接收](https://www.jianshu.com/p/85251b746058)
- [SpringMVC接收复杂集合参数](https://jxd-zxf.iteye.com/blog/2072300)