首先安装samba服务器
```
[root@localhost ~]# yum install samba-common,samba
```
查看samba服务的启动情况
```
[root@localhost ~]# service smb status
//如果显示
smbd is stopped
```
执行
```
[root@localhost ~]# service smb start
Starting SMB services:                                     [  OK  ]
```
在任务列表中应该可以看到smb的守护进程
```
[root@localhost ~]# ps aux | grep smb
root      1552  0.3  0.1 213520  3756 ?        Ss   11:03   0:00 smbd -D
root      1554  0.0  0.1 214036  2032 ?        S    11:03   0:00 smbd -D
root      1557  0.0  0.0 103304   880 pts/0    S+   11:04   0:00 grep smb
```
为了samba可以开机启动,在chkconfig中添加运行级别3和5自动启动
```
[root@localhost ~]# chkconfig --level 35 smb on
[root@localhost ~]# chkconfig | grep smb
smb       0:off   1:off   2:off   3:on    4:off   5:on    6:off
```
这样samba服务算是启动了,但是没有配置共享的信息  
编辑`/etc/samba/smb.conf`配置文件  
配置smb服务  
```
[global]
workgroup = WORKGROUP
security = SHARE

[public]
comment = a comment
path = /path/to/your/share/folder
public = yes
writeable = yes
browseable = yes
guest ok = yes
```
编辑完之后需要关闭防火墙和selinux才能正常访问
1.关闭selinux  
编辑selinux配置文件/etc/selinux/config
```
[root@localhost ~]# vi /etc/selinux/config
```
将SELINUX字段改成disabled
```
SELINUX=disabled
```
2.关闭防火墙
```
[root@localhost ~]# service iptables stop
```
