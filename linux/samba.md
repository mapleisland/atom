# ubuntu下配置Samba实现文件夹共享

一. samba的安装:
```
sudo apt-get insall samba
sudo apt-get install smbfs
```
二. 创建共享目录:
```
mkdir /home/username/share
sudo chmod 777 /home/username/share
```
三. 创建Samba配置文件:

1. 保存现有的配置文件
```
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.bak
```
2. 修改现配置文件
```
sudo gedit /etc/samba/smb.conf
```
在smb.conf最后添加
```
[share]
  path = /path/to/sharefolder
  available = yes
  browsealbe = yes
  public = yes
  writable = yes
```
四. 创建samba帐户
```
sudo touch /etc/samba/smbpasswd
sudo smbpasswd -a username
```
然后会要求你输入samba帐户的密码

 ［如果没有第四步，当你登录时会提示 session setup failed: NT_STATUS_LOGON_FAILURE］

 五. 重启samba服务器
```
sudo /etc/init.d/samba restart
```
六. 测试
```
smbclient -L //localhost/share
```
七，使用
```
可以到windows下输入ip使用了，在文件夹处输入 "\\" + "Ubuntu机器的ip或主机名" + "\\" + "share"
```