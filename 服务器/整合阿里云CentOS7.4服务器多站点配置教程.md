# 整合阿里云CentOS7.4服务器多站点配置教程

标签（空格分隔）： 多站点 虚拟主机

---
> httpd 配置文件路径: `/etc/httpd/conf/httpd.conf`
> 说明:现在有`bolg.geekln.cn`和`hello.geekln.cn`两个域名，现在要配置两个站点。

- bolg.geekln.cn 的站点路径为 `/var/www/heml/bolg`
- hello.geekln.cn 的站点路径为 `/var/www/heml/hello`

## 一 、增加站点配置文件
- 创建目录
```
cd /etc/httpd
//创建一个虚拟主机目录
sudo mkdir vhost-conf.d
```
- 创建`bolg.geekln.cn` 站点对应文件:  `bolg-geekln.conf`
```
<VirtualHost *:80>
    #Created by Geekln on 2018-09-12
    Serveradmin 1373518279@qq.com
    ServerName bolg.geekln.cn
    DocumentRoot /var/www/heml/bolg

    <Directory "/var/www/heml/bolg">
          Options FollowSymLinks
          AllowOverride All
          #Require all denied
          Require all granted
    </Directory>
</VirtualHost>
```

- 创建`hello.geekln.cn` 站点对应文件:  `hello-geekln.conf`
```
<VirtualHost *:80>
    #Created by Geekln on 2018-09-12
    Serveradmin 1373518279@qq.com
    ServerName hello.geekln.cn
    DocumentRoot /var/www/heml/hello

    <Directory "/var/www/heml/hello">
          Options FollowSymLinks
          AllowOverride All
          #Require all denied
          Require all granted
    </Directory>
</VirtualHost>
```
## 二、修改httpd配置文件
```
sudo vim /etc/httpd/conf/httpd.conf
```
- 在配置httpd配置文件末尾添加虚拟主机路径
```
Include vhost-conf.d/*.conf
```
## 三、修改hosts文件
```
sudo vim /etc/hosts
```
- 在末尾添加
```
127.0.0.1 bolg.geekln.cn
127.0.0.1 hello.geekln.cn
```
## 四、重启Apahce服务器
```
sudo systemctl restart httpd.service
```
- 自此多站点配置完毕

> 注意：前提是你的两个域名必须在域名解析里面将域名解析到你的IP


