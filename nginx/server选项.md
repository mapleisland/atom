
```
server {
	#监听端口
	listen 8080;

	#服务器名字,配置域名
	server_name  domain.com www.domain.com;

	#打开索引功能
	autoindex on;

	#人性化方式显示大小
	autoindex_exact_size on/off;

	#显示服务器时间
	autoindex_localtime on;
}

```
Gzip
```
gzip on;
gzip_min_length 1k;
gzip_buffers 4 16k;
#gzip_http_version 1.0;
gzip_comp_level 2;
gzip_types text/plain application/x-javascript text/css application/xml text/javascript application/x-httpd-php image/jpeg image/gif image/png;
gzip_vary off;
gzip_disable "MSIE [1-6]\.";
```


```
events{
	#epoll模型是Linux 2.6以上版本内核中的高性能网络I/O模型
	use epoll;

	#单个worker进程最大连接数
	#nginx最大连接数 = worker连接数 * worker进程数
	worker_connections 1024;
}
```
