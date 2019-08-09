## Nginx

Nginx是一款高性能的http服务器/反向代理服务器及电子邮件（IMAP/POP3）代理服务器。

#### 应用场景

1. HTTP服务器。用作静态网页服务器。

2. 反向代理服务器。通过配置将服务器的IP和指定域名进行映射。

3. 负载均衡。

#### Linux上安装Nginx

#### Nginx实现负载均衡

#### Nginx日志

Nginx日志主要有两种：访问日志和错误日志。

访问日志主要记录客户端访问nginx的每一个请求，格式可以自定义。

错误日志主要记录客户端访问nginx出错时的日志，格式不支持自定义。

两种日志都可以选择性关闭。

通过访问日志，你可以得到用户地域来源、跳转来源、使用终端、某个URL访问量等相关信息；通过错误日志，你可以得到系统某个服务或server的性能瓶颈等。

##### 访问日志[Access.log]

<table>
    <tr><th>变量名称</th><th>变量描述</th><th>举例说明</th></tr>
    <tr><td>$remote_addr</td><td>客户端地址</td><td>113.140.15.90</td></tr>
    <tr><td>$remote_user</td><td>客户端用户名称</td><td>–</td></tr>
    <tr><td>$time_local</td><td>访问时间和时区</td><td>18/Jul/2012:17:00:01 +0800</td></tr>
    <tr><td>$request</td><td>请求的URI和HTTP协议</td><td>“GET /pa/img/home/logo-alipay-t.png HTTP/1.1″</td></tr>
    <tr><td>$http_host</td><td>请求地址，即浏览器中你输入的地址（IP或域名）</td><td>img.alipay.com10.253.70.103</td></tr>
    <tr><td>$status</td><td>HTTP请求状态</td><td>200</td></tr>
    <tr><td>$upstream_status</td><td>upstream状态</td><td>200</td></tr>
    <tr><td>$body_bytes_sent</td><td>发送给客户端文件内容大小</td><td>547</td></tr>
    <tr><td>$http_referer</td><td>跳转来源</td><td> “https://cashier.alipay.com…/”</td></tr>
    <tr><td>$http_user_agent</td><td>用户终端代理</td><td>“Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 5.1; Trident/4.0; SV1; GTB7.0; .NET4.0C;</td></tr>
    <tr><td>$ssl_protocol</td><td>SSL协议版本</td><td>TLSv1</td></tr>
    <tr><td>$ssl_cipher</td><td>交换数据中的算法</td><td>RC4-SHA</td></tr>
    <tr><td>$upstream_addr</td><td>后台upstream的地址，即真正提供服务的主机地址</td><td>10.228.35.247:80</td></tr>
    <tr><td>$request_time</td><td>整个请求的总时间</td><td>0.205</td></tr>
    <tr><td>$upstream_response_time</td><td>请求过程中，upstream响应时间</td><td>0.002</td></tr>
</table>

##### 错误日志[Error.log]

<table>
    <tr><th>错误信息</th><th>错误说明</th></tr>
    <tr><td>“upstream prematurely（过早的） closed connection”</td><td>请求uri的时候出现的异常，是由于upstream还未返回应答给用户时用户断掉连接造成的，对系统没有影响，可以忽略</td></tr>
    <tr><td>“recv() failed (104: Connection reset by peer)”</td><td>（1）服务器的并发连接数超过了其承载量，服务器会将其中一些连接Down掉； （2）客户关掉了浏览器，而服务器还在给客户端发送数据； （3）浏览器端按了Stop</td></tr>
    <tr><td>“(111: Connection refused) while connecting to upstream”</td><td>用户在连接时，若遇到后端upstream挂掉或者不通，会收到该错误</td></tr>
    <tr><td>“(111: Connection refused) while reading response header from upstream”</td><td>用户在连接成功后读取数据时，若遇到后端upstream挂掉或者不通，会收到该错误</td></tr>
    <tr><td>“(111: Connection refused) while sending request to upstream”</td><td>Nginx和upstream连接成功后发送数据时，若遇到后端upstream挂掉或者不通，会收到该错误</td></tr>
    <tr><td>“(110: Connection timed out) while connecting to upstream”</td><td>nginx连接后面的upstream时超时</td></tr>
    <tr><td>“(110: Connection timed out) while reading upstream”</td><td>nginx读取来自upstream的响应时超时</td></tr>
    <tr><td>“(110: Connection timed out) while reading response header from upstream”</td><td>nginx读取来自upstream的响应头时超时</td></tr>
    <tr><td>“(110: Connection timed out) while reading upstream”</td><td>nginx读取来自upstream的响应时超时</td></tr>
    <tr><td>“(104: Connection reset by peer) while connecting to upstream”</td><td>upstream发送了RST，将连接重置</td></tr>
    <tr><td>“upstream sent invalid header while reading response header from upstream”</td><td>upstream发送的响应头无效</td></tr>
    <tr><td>“upstream sent no valid HTTP/1.0 header while reading response header from upstream”</td><td>upstream发送的响应头无效</td></tr>
    <tr><td>“client intended to send too large body”</td><td>用于设置允许接受的客户端请求内容的最大值，默认值是1M，client发送的body超过了设置值</td></tr>
    <tr><td>“reopening logs”</td><td>用户发送kill  -USR1命令</td></tr>
    <tr><td>“gracefully shutting down”,</td><td>用户发送kill  -WINCH命令</td></tr>
    <tr><td>“no servers are inside upstream”</td><td>upstream下未配置server</td></tr>
    <tr><td>“no live upstreams while connecting to upstream”</td><td>upstream下的server全都挂了</td></tr>
    <tr><td>“SSL_do_handshake() failed”</td><td>SSL握手失败</td></tr>
    <tr><td>“SSL_write() failed (SSL:) while sending to client”</td><td> </td></tr>
    <tr><td>“(13: Permission denied) while reading upstream”</td><td> </td></tr>
    <tr><td>“(98: Address already in use) while connecting to upstream”</td><td> </td></tr>
    <tr><td>“(99: Cannot assign requested address) while connecting to upstream”</td><td> </td></tr>
    <tr><td>“ngx_slab_alloc() failed: no memory in SSL session shared cache”</td><td>ssl_session_cache大小不够等原因造成</td></tr>
    <tr><td>“could not add new SSL session to the session cache while SSL handshaking”</td><td>ssl_session_cache大小不够等原因造成</td></tr>
    <tr><td>“send() failed (111: Connection refused)”</td><td></td></tr>
</table>



