# Centos 7 FTP（vsftp）服务安装及配置

标签（空格分隔）： FTP VSFTP

---
## 一、安装和配置

1.vsftp 安装
```
yum install vsftpd
```
- 输入上面的安装代码后，不久会有类似is this ok[y/N]:直接输入Y继续就可以了。
vsftp 配置

2.FTP配置文件相关配置
```
vi /etc/vsftpd/vsftpd.conf
```
定位到
```
anonymous_enable=YES
```
- 按下键盘i盘进入编辑模式 把YES改成NO
```
anonymous_enable=NO
```
- 这样就可以了。这里的anonymous_enable=NO意思是不允许匿名登录FTP

- 设置完以后，按下 Esc 退出编辑模式，再按下`:wq`保存退出。
### 启动和停止
- 启用vsftp服务
```
systemctl start vsftpd.service
```
- 停止 vsftp 服务
```
systemctl stop vsftpd.service
```
- 重启 vsftp 服务
```
systemctl restart vsftpd.service
```
- 开机自动启动
```
systemctl enable vsftpd.service
```
- 取消随服务器启动
```
systemctl disable vsftpd.service
```
## 二、创建访问用户
1.接下来我们就要以创建一个用户，并给这个用户指定一个目录。
```
useradd -d /var/www/html/yunkus.com -s /sbin/nologin yunkus
```
> -s：禁止此用户登录SSH的权限 
> /sbin/nologin：不允许此用户登录系统，但可以登录FTP

2.设置用户密码
- 用户创建好后，我们还得给他设置一个登录密码
```
passwd yunkus
```
- 回车，输入密码即可（需输入两次）
- 这样就完成了服务器端的FTP服务的配置




