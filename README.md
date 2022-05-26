# linux常用命令

- ls - list
- cd - change directory
- rm - remove (删除)
- touch - 创建file
- mkdir - 创建dir
- ps -ef - 查看进程
- top
- ll |grep "abc" - 过滤除了"abc"的file和dir
- cat - 在terminal显示
- yum install - yum 安装
- pwd - 查看当前path
- wget https://dev.mysql.com/get/mysql80-community-release-el8-4.noarch.rpm 
- rpm -qa | grep mysql - 查看是否安装 mysql
- find / -name mysql - 查找mysql 文件夹

## Centos-8 无法连接yum

```
cd yum.repos.d/
mkdir bk
mv * bk/

wget https://mirrors.aliyun.com/repo/Centos-vault-8.5.2111.repo -O /etc/yum.repos.d/Centos-vault-8.5.2111.repo
wget https://mirrors.aliyun.com/repo/epel-archive-8.repo -O /etc/yum.repos.d/epel-archive-8.repo

yum install -y mysql-server
systemctl start mysqld
systemctl enable mysqld
service mysqld status

```

### 查看MySQL 是否启动

```
ps -ef |grep mysql
mysqladmin --version
```

### 相关安装目录

```
cd /usr/bin/
fin my*
```

### 相关路劲

```
cd /usr/share/mysql
ls -lh
```

### 相关文件存放目录

```
cd /var/lib/mysql
ls -lh
```

```
/etc/my.cnf.d //mysql的启动配置文件
* client.cnf //mysql客户端配置文件
* mysql-server.cnf //mysql守护进程配置文件
* mysql-default-authentication-plugin.cnf //默认权限授权配置文件
备注：
可复制一份到/etc下，修改成my.cnf
```

### 更改root密码

```
alter user 'root'@'localhost' identified with mysql_native_password by 'root密码';
flush privileges;
```



### 设置远程登录账号

```
use mysql
select user,host from user;
create user 'oct'@'%' identified by '密码';
grant all privileges on *.* to 'oct'@'%';//开放权限
alter user 'oct'@'%' identified with mysql_native_password by '你的密码';
flush privileges;
```

### 开启防火墙端口

```
systemctl start firewalld
查看防火墙某个端口是否开放
firewall-cmd --query-port=80/tcp

开放防火墙端口80
firewall-cmd --zone=public --add-port=80/tcp --permanent

关闭80端口

firewall-cmd --zone=public --remove-port=80/tcp --permanent

配置立即生效
firewall-cmd --reload
查看防火墙状态
systemctl status firewalld

https://10.8.11.99/

关闭防火墙
systemctl stop firewalld

打开防火墙
systemctl start firewalld

开放一段端口
firewall-cmd --zone=public --add-port=8121-8124/tcp --permanent

查看开放的端口列表
firewall-cmd --zone=public --list-ports

```

