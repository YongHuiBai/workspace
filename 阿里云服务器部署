# 阿里云服务器 (Flask+uwsgi+Nginx+Ubuntu部署) 

一、
1. 购买完服务器更改服务器密码 。 控制台-重置密码（root密码）
2. 控制台远程连接 login root password 刚才的密码
3. 开放端口21 以及阿里云安全组开放21（防火墙开启端口 ufw allow 21) 或者（关闭防火墙ufw enable）
4. 使用终端ssh 连接服务器
5.创建新用户 命令 adduser (username) 
6.为该用户添加sudo功能 命令 vim /etc/sudoers ， 
在root ALL=ALL=(ALL:ALL) ALL下添加一行 
username ALL=ALL=(ALL:ALL) ALL 用wq!保存后 就可以用sshusername@xx.xx:xx:xx:xx登录
7.安装mysql 数据库 sudo apt-get install mysql-server
8.为mysql 设置远程访问权限
安装完用mysql -u root -p登录修改远程访问权限
GRANT ALL PRIVILEGES ON *.* TO'用户名'@'%' IDENTIFIED BY '密码' WITH GRANT OPTION;
flush privileges; 更新权限
进入/etc/mysql/my.cnf  注释掉 bind_address=127.0.0.1
开放端口3306 以及阿里云安全组开放3306    -- (防火墙关闭忽略)
最后用workbench连接 完成
9.安装pip
sudo apt-get install python-pip
10.安装flask
pip install flask
11.安装nginx
sudo apt-get install nginx  安装启动 service nginx start 如果遇到端口被占用kill 掉80端口，从新执行命令
成功后可以在浏览器输入ip地址看到welcome to nginx!

二、
1. 配置falsk项目。 
2. 在项目中加uwsgi.ini配置文件 大致配置如下
[uwsgi]
socket = 127.0.0.1:5051 // 指定项目执行的端口号
processes = 4  // 开启的进程数量（这里是开启4个进程）
threads = 2 // 开启的线程数量（这里是开启2个进程）
master = true // 允许主线程存在（true）
pythonpath = /root/workspace/Flask_demo //指明当前应用程序的项目路径
module = hello // 程序的入口文件名
callable = app //应用程序中指明的uwsgi需要调用的应用程序
memory-report = true //开启内存报告
3.修改nginx 文件 命令 vi /etc/nginx/sites-available/default   修改内容如下：
server_name  xx.xx.xx.xx;
location  中添加两行
include uwsgi_params;
uwsgi_pass  127.0.0.1:5051;
配置完成后 
重启nginx  命令 service nginx restart
cd到项目中 开启uwsgi  命令 uwsgi --ini uwsgi.ini 
完成如果遇到 浏览器显示Internal Server Error 因为uwsgi 与nginx 通信失败
执行命令killall -9 uwsgi 后再次执行命令 uwsgi --ini uwsgi.ini 


