# mysql重新回顾

### 安装步骤

安装完成后，在Mysql文件夹里找到my.ini进行配置（C:\ProgramData\MySQL\MySQL Server 5.7\my.ini）

1.[mysqld]里面的port可以修改端口号

basedir是安装目录

default-storage-engine存储引擎

2.然后在计算机启动项管理中找到服务，刚刚起名字叫MYSQL57，就找这个

cmd停止mysql

cmd:net stop mysql57（注意必须是管理员身份）



#### 进入mysql

1.开始菜单进入mysql 5.7 command line client程序

输入密码即可

退出输入exit或者ctrl+c

不推荐这个方法，因为只能root用户用

2.cmd：mysql -h localhost  -P 3306 -u root -p回车 输入密码（h代表host，p代表端口号，u代表user）

mysql -h localhost  -P 3306 -u root -proot 直接回车也可以 最后一个p代表password

如果连接本机，主机名和端口号这两个参数可以省略