## 1. nginx 配置反向代理下载 MP4 文件，在 Chrome 报网络错误

> 1.查看 nginx 日志

```
open()failed (13: Permission denied) while reading upstream
```

> 2.nginx

```
ps -ef|grep nginx 查看worker线程的用户(nobody)
ls -al /usr/local/nginx/proxy_temp 查看权限

chown -R nobody:nobody /usr/local/nginx/proxy_temp 为文件夹添加owner
```

> 3.原因

```
分析下failed (13: Permission denied) while reading upstream问题的原因

首先看一下nginx 反向代理参数说明

proxy_connect_timeout 600; #nginx跟后端服务器连接超时时间(代理连接超时)
proxy_read_timeout 600; #连接成功后，后端服务器响应时间(代理接收超时)
proxy_send_timeout 600; #后端服务器数据回传时间(代理发送超时)
proxy_buffer_size 32k; #设置代理服务器（nginx）保存用户头信息的缓冲区大小
proxy_buffers 4 32k; #proxy_buffers缓冲区，网页平均在32k以下的话，这样设置
proxy_busy_buffers_size 64k; #高负荷下缓冲大小（proxy_buffers*2）
proxy_temp_file_write_size 64k; #设定缓存文件夹大小，大于这个值，将从upstream服务器传

问题就出在proxy_temp_file_write_size上，当你的文件超过该参数设置的大小时，nginx会先将文件写入临时目录(缺省为nginx安装目下/proxy_temp目录),

如果nginx对prxoy_temp没有权限就会写不进去，结果就是只显示部分页面。

我遇到这个案例用工具查看了一下，post-new.php这个页面大小事94，超过了64k就要符合我们上面的分析。
```

> 4.reference

[referer1](https://blog.csdn.net/xiangguiwang/article/details/78662528)
[referer2](http://www.nginx.cn/695.html)
