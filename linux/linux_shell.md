# 系统信息
## 查看Linux内核版本
cat /proc/version
## 查看Linux系统版本
lsb_release -a
## 查看磁盘剩余空间
df -h
## 查看剩余内存
free -m
## 查看目录大小
du -bs /Directory
## 查看大文件
find . -size +100M

# mysql数据库操作
## mysql安装
### 安装目录
安装文件下载目录：/data/software
Mysql目录安装位置：/usr/local/mysql
数据库保存位置：/data/mysql
日志保存位置：/data/log/mysql
## mysql卸载
### 查看安装情况
rpm -qa|grep -i mysql
### 卸载
rpm -ev MySQL-client-5.5.25a-1.rhel5
### 解决卸载依赖包报错
rpm -ev MySQL-client-5.5.25a-1.rhel5 --nodeps
### 解决卸载退出报错
rpm -e --noscripts MySQL-client-5.5.25a-1.rhel5 
### 清空mysql缓存
rm -rf /var/lib/mysql
rm -rf /var/lib/mysql
rm -rf /usr/lib64/mysql
rm -rf /etc/my.cnf 
## mysql远程连接设置
### 授权操作mysql>
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'admin' WITH GRANT OPTION;
### 重载授权表mysql>
FLUSH PRIVILEGES;
## 操作数据库
### 连接本地数据库
mysql -h host -uroot -ppassword
### 导出数据库 
mysqldump -hhost -uroot -ppassword db > db_bak.sql
### 导入数据库
mysql -uroot -ppassword db < db_bak.sql
### 显示数据库列表
show databases;
### 显示库中的数据表
use mysql； 
show tables;
### 显示数据表的结构
describe 表名;
### 查询表中的记录
select * from 表名;
### 建库
create database 库名;
GBK: create database test2 DEFAULT CHARACTER SET gbk COLLATE gbk_chinese_ci;
UTF8: CREATE DATABASE `test2` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
### 建表
use 库名；
create table 表名(字段设定列表)；
### 删库和删表
drop database 库名;
drop table 表名；
### 将表中记录清空
delete from table;
truncate table table;
## 修改数据库登录密码
mysqladmin -u用户名 -p旧密码 password 新密码
mysql>SET PASSWORD FOR root=PASSWORD("root");
## 新增用户
grant select on 数据库.* to 用户名@登录主机 identified by "密码"
如增加一个用户test密码为123，让他可以在任何主机上登录， 并对所有数据库有查询、插入、修改、删除的权限。首先用以root用户连入mysql，然后键入以下命令：
grant select,insert,update,delete on *.* to " Identified by "123";

* [Tomcat](#1)
* [查看项目日志](#1.1)
# Tomcat
## 查看项目日志
tail -f /usr/local/src/apache-tomcat-8.5.15/logs/catalina.out
## 运行停止项目
cd /usr/local/src/apache-tomcat-8.5.15/bin/
./shutdown.sh
./startup.sh

split命令专门用来将一个大文件分割成很多个小文件，我把split命令的选项做一个简要说明

选项	含义
-b	分割后的文档大小，单位是byte
-C	分割后的文档，单行最大byte数
-d	使用数字作为后缀，同时使用-a length指定后缀长度
-l	分割后文档的行数
为了尽量保证日志的可读性，我们按行分割大日志文件，并且指定分割后的文件的前缀和后缀

#后缀是数字，占两位，前缀是test.log
split -l 1000000 test.log -d -a 2 test.log
# 按照指定配置运行jar包
java -Xms4G -Xmx8G -jar /usr/local/allinone-testcase-collect-service-0.1-SNAPSHOT.jar --spring.profiles.active=pro > /usr/local/allinone/testcasecollect/log/allinone-testcase-collect-service.log
