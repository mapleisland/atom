# mount挂载命令

查询系统中已经挂载的设备
```
[root@localhost ~]# mount
```

依据配置文件/etc/fstab的内容,自动挂载
```
[root@localhost ~]# mount -a
```

完整格式
```
[root@localhost ~]# mount [-t 文件系统] [-o 特殊选项] 设备文件名 挂载点
```

卸载
```
[root@localhost ~]# umount 设备文件名或挂载点
```