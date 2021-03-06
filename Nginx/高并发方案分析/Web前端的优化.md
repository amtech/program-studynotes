### 一 减少Http请求
> 一个页面的请求，%80 的时间花在了 资源的加载上，剩下的才是 html的接收时间

##### 1.  HTTP连接产生的开销
- 域名解析-TCP连接-发送请求-等待-下载资源-解析时间
- http1.0协议是串行请求，按照顺序进行发送
- dns的解析也是要花时间的

##### 2. 方法
- css，js,图片合并等方法

### 二. HTTP缓存机制
##### 1. 缓存分类
HTTP缓存模型中，如果请求成功会有三种情况：
```bash
200 from cache：直接从本地缓存中获取响应，最快速，最省流量，因为没有向服务器发送请求

304 ： 协商缓存，浏览器发送请求头服务器验证，如果服务器没有改变从浏览器本地获取内容

200 ： 从服务器获取内容，没有说那个缓存
```
nginx.conf 中配置
expires time； 通知浏览器过期时长

### 三. 脚本代码压缩

使用压缩工具对代码进行格式化压缩

使用 nginx 模块 gzip 开启压缩传输
```bash
gzip on | off ; #是否开启gzip
gzip_buffers 32 4k |16 8k ;#在内存中缓冲多少块，每块多大
gzip_comp_level [1-9] #推荐6（级别越高，压得越小，越浪费cpu计算资源）
gzip_comp_level [1-9] #推荐6（级别越高，压得越小，越浪费cpu计算资源）
gzip_comp_level [1-9] #推荐6（级别越高，压得越小，越浪费cpu计算资源）
gzip_comp_level [1-9] #推荐6（级别越高，压得越小，越浪费cpu计算资源）
gzip_disable          #正则匹配UA 什么样的uri不进行gzip
gzip_min_length 200;  #开始压缩的最小长度
gzip_http_version 1.0|1.1; #开始压缩的http协议版本
gzip_proxied;             #设置请求者代理服务器该如何缓存内容
```

### 四. 独立的资源服务器
- 分担web服务器的 I/O资源，提高服务器的性能稳定性
- 服务器不需要很强的CPU计算资源
- 需要高转速的硬盘和磁盘阵列
- 可以提高网站的可扩展性
- 尽量采用独立域名
