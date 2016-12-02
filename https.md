# 使用 OpenSSL 生成 SSL Key 和 CSR
由于只有浏览器或者系统信赖的 CA 才可以让所有的访问者通畅的访问你的加密网站，而不是出现证书错误的提示。所以我们跳过自签证书的步骤，直接开始签署第三方可信任的 SSL 证书吧。

OpenSSL 在 Linux、OS X 等常规的系统下默认都安装了，因为一些安全问题，一般现在的第三方 SSL 证书签发机构都要求起码 2048 位的 RSA 加密的私钥。

同时，普通的 SSL 证书认证分两种形式，一种是 DV（Domain Validated），还有一种是 OV （Organization Validated），前者只需要验证域名，后者需要验证你的组织或公司，在安全性方面，肯定是后者要好。

无论你用 DV 还是 OV 生成私钥，都需要填写一些基本信息，这里我们假设如下：
- 域名，也称为 Common Name，因为特殊的证书不一定是域名：example.com
- 组织或公司名字（Organization）：Example, Inc.
- 部门（Department）：可以不填写，这里我们写Web Security
- 城市（City）：Beijing
- 省份（State / Province）：Beijing
- 国家（Country）：CN
- 加密强度：2048 位，如果你的机器性能强劲，也可以选择 4096 位
按照以上信息，使用 OpenSSL 生成 key 和 csr 的命令如下:
```
openssl req -new -newkey rsa:2048 -sha256 -nodes -out example_com.csr -keyout example_com.key -subj "/C=CN/ST=Beijing/L=Beijing/O=Example Inc./OU=Web Security/CN=example.com"
```
PS：如果是泛域名证书，则应该填写*.example.com

你可以在系统的任何地方运行这个命令，会自动在当前目录生成example_com.csr和example_com.key这两个文件

接下来你可以查看一下example_com.csr，得到类似这么一长串的文字
```
-----BEGIN CERTIFICATE REQUEST-----
MIICujCCAaICAQAwdTELMAkGA1UEBhMCQ04xEDAOBgNVBAgTB0JlaWppbmcxEDAO  
BgNVBAcTB0JlaWppbmcxFTATBgNVBAoTDEV4YW1wbGUgSW5jLjEVMBMGA1UECxMM  
V2ViIFNlY3VyaXR5MRQwEgYDVQQDEwtleGFtcGxlLmNvbTCCASIwDQYJKoZIhvcN  
AQEBBQADggEPADCCAQoCggEBAPME+nvVCdGN9VWn+vp7JkMoOdpOurYMPvclIbsI  
iD7mGN982Ocl22O9wCV/4tL6DpTcXfNX+eWd7CNEKT4i+JYGqllqP3/CojhkemiY  
SF3jwncvP6VoST/HsZeMyNB71XwYnxFCGqSyE3QjxmQ9ae38H2LIpCllfd1l7iVp  
AX4i2+HvGTHFzb0XnmMLzq4HyVuEIMoYwiZX8hq+kwEAhKpBdfawkOcIRkbOlFew  
SEjLyHY+nruXutmQx1d7lzZCxut5Sm5At9al0bf5FOaaJylTEwNEpFkP3L29GtoU  
qg1t9Q8WufIfK9vXqQqwg8J1muK7kksnbYcoPnNgPx36kZsCAwEAAaAAMA0GCSqG  
SIb3DQEBBQUAA4IBAQCHgIuhpcgrsNwDuW6731/DeVwq2x3ZRqRBuj9/M8oONQen  
1QIacBifEMr+Ma+C+wIpt3bHvtXEF8cCAJAR9sQ4Svy7M0w25DwrwaWIjxcf/J8U  
audL/029CkAuewFCdBILTRAAeDqxsAsUyiBIGTIT+uqi+EpGG4OlyKK/MF13FxDj  
/oKyrSJDtp1Xr9R7iqGCs/Zl5qWmDaLN7/qxBK6vX2R/HLhOK0aKi1ZQ4cZeP7Mr
8EzjDIAko87Nb/aIsFyKrt6Ze3jOF0/vnnpw7pMvhq+folWdTVXddjd9Dpr2x1nc  
y5hnop4k6kVRXDjQ4OTduQq4P+SzU4hb41GIQEz4  
-----END CERTIFICATE REQUEST-----
```
这个 CSR 文件就是你需要提交给 SSL 认证机构的，当你的域名或组织通过验证后，认证机构就会颁发给你一个example_com.crt

而example_com.key是需要用在 Nginx 配置里和example_com.crt配合使用的，需要好好保管，千万别泄露给任何第三方。

# Nginx 配置 HTTPS 网站以及增加安全的配置
前面已经提到，你需要提交 CSR 文件给第三方 SSL 认证机构，通过认证后，他们会颁发给你一个 CRT 文件，我们命名为example_com.crt

同时，为了统一，你可以把这三个文件都移动到/etc/ssl/private/目录。

然后可以修改 Nginx 配置文件:
```
server {  
    listen 80;
    listen [::]:80 ssl;
    listen 443 ssl;
    listen [::]:443 ssln;
    server_name example.com;

    ssl on;
    ssl_certificate /etc/ssl/private/example_com.crt;
    ssl_certificate_key /etc/ssl/private/example_com.key;
}
```
检测配置文件没问题后重新读取 Nginx 即可
```
nginx -t && nginx -s reload
```
但是这么做并不安全，默认是 SHA-1 形式，而现在主流的方案应该都避免 SHA-1，为了确保更强的安全性，我们可以采取迪菲－赫尔曼密钥交换
首先，进入`/etc/ssl/certs`目录并生成一个`dhparam.pem`
```
openssl dhparam -out dhparam.pem 2048 # 如果你的机器性能足够强大，可以用 4096 位加密
```
生成完毕后，在 Nginx 的 SSL 配置后面加入
```
ssl_prefer_server_ciphers on;
ssl_dhparam /etc/ssl/certs/dhparam.pem;
ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
ssl_ciphers "EECDH+ECDSA+AESGCM EECDH+aRSA+AESGCM EECDH+ECDSA+SHA384 EECDH+ECDSA+SHA256 EECDH+aRSA+SHA384 EECDH+aRSA+SHA256 EECDH+aRSA+RC4 EECDH EDH+aRSA !aNULL !eNULL !LOW !3DES !MD5 !EXP !PSK !SRP !DSS !RC4";
keepalive_timeout 70;
ssl_session_cache shared:SSL:10m;
ssl_session_timeout 10m;
```
同时，如果是全站 HTTPS 并且不考虑 HTTP 的话，可以加入 HSTS 告诉你的浏览器本网站全站加密，并且强制用 HTTPS 访问
```
add_header Strict-Transport-Security max-age=63072000;
add_header X-Frame-Options DENY;
add_header X-Content-Type-Options nosniff;
```
同时也可以单独开一个 Nginx 配置，把 HTTP 的访问请求都用 301 跳转到 HTTPS
```
server {
  return 301 https://example.com$request_uri;
}
```
