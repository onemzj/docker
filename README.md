# docker-compose-nginx-php-mysql
docker-compose+nginx+php+mysql+redis
# 版本
php:5.6.x
php:7.x

mysql:5.6.x
mysql:5.7.x

nginx:latest


# 更新说明
 * 2018-3-11 
   * 更新 docker-compose 版本为3.5版本
   * 去除 elasticsearch 容器 (稍后放出 elk容器集群)
   * 更新 网络名称为`lnmp`,不使用默认网络，方便其他容器或容器集群加入到`lnmp`网络中
   * 更新 nginx default.conf配置文件,调用php容器默认别名

# elasticsearch logtsash kibana
如果你要使用搜索引擎
https://github.com/foxiswho/docker-elk

# nginx docker内配置文件位置
配置文件位置：/etc/nginx/nginx.conf

来源：官方源 

# php docker内配置文件位置
来源：官方源 

配置文件及目录位置

/usr/local/etc/php-fpm.conf

/usr/local/etc/php-fpm.d/www.conf

/usr/local/etc/php-fpm.d  目录

## php.ini 默认加载目录位置
/usr/local/etc/php/conf.d/  目录
## 扩展目录位置
/usr/local/lib/php/extensions/

# redis
来源：官方源 

# elasticsearch
来源：官方源 

# Mac系统 docker php71 安装案例
## Mac系统 安装方式

https://www.docker.com/docker-mac

下载该软件,安装略

**开始设置目录**

菜单->Preferences->File Sharing,点 + 号,选择 跟目录下的 `Volumes` 文件夹，点击 `Apply & Restart` 按钮

**设置阿里云源**
菜单->Preferences->Daemon ,Basic 选项卡 ,Registry mirrors 下,点 + 号,把你的阿里云镜像加速地址加入进去。

阿里云镜像加速地址类似于这种格式`https://******.mirror.aliyuncs.com`,

**如果设置自己的阿里云镜像加速地址**
到阿里云控制台找到属于自己的 镜像加速地址：https://cr.console.aliyun.com/#/accelerator

加速地址设置教程-> https://yq.aliyun.com/articles/29941



### 0.首先MAC系统硬盘设置
mac 系统默认硬盘默认 `不区分大小写`，

如果需要区分请 按 [http://blog.csdn.net/fenglailea/article/details/53083785](http://blog.csdn.net/fenglailea/article/details/53083785) 此链接中教程 重新分区。

`建议分区，我这里是分区的`

建立 一个 `10G` 卷名为`work`的分区，格式化为`区分大小写`格式。
> 注意也可以不分区，`/Volumes/`目录下建立一个软连接文件夹也可以

### 1.选择要安装的系统和版本

例如：mac系统 php7.1版本,进入`mac-php71`目录
```shell
cd mac-php71
```

### 2.docker-compose.yml配置更改

选择你需要的功能，不需要的用#号注释掉

### 3.建立目录和文件
新建目录
```shell
/Volumes/work/wwwroot/
```
Volumes: MAC系统 卷 硬盘名称都会显示在里面,`work`单独的分区

work：分区名称

wwwroot:自定义目录,默认目录

nginx/vhost：nginx 站点配置文件

在当前 `nginx/vhost` 目录下，配置你的 nginx站点，可以根据 `default.conf`进行修改

在 `/Volumes/work/wwwroot/` 目录下
新建 `index.php`
```php
<?php
phpinfo();
```

>注意 如果你是自定义本地站点如`test.com`，那么就要在 `/etc/hosts` 加入本地host指向，编辑时需要`root`权限的哦

```SHELL
127.0.0.1 test.com
```

### 4.生成镜像

这个时候 一定不能更换目录。

`注意` 如果你以前已经配置过一样的容器那么会自动覆盖容器
```
docker-compose up
```
时间比较长， 更新源都在国外，最好早晨拉取


完成后，在浏览器里面输入`localhost`回车，即可看到`phpinfo`输出信息

## 安装完成后 一定要配置PHP，主要启用PHP扩展
基本PHP 扩展已经启用，这里无须再启用

macphp71_1 容器名字可能生成的不一样

# Windows 版 docker php71 安装案例

下载地址

https://www.docker.com/docker-windows

或

https://store.docker.com/editions/community/docker-ce-desktop-windows

下载该软件,安装略

**开始设置目录**

菜单->Preferences->File Sharing,点 + 号,选择 跟目录下的 `Volumes` 文件夹，点击 `Apply & Restart` 按钮

**设置阿里云源**
菜单->Preferences->Daemon ,Basic 选项卡 ,Registry mirrors 下,点 + 号,把你的阿里云镜像加速地址加入进去。

阿里云镜像加速地址类似于这种格式`https://******.mirror.aliyuncs.com`,

**如果设置自己的阿里云镜像加速地址**
到阿里云控制台找到属于自己的 镜像加速地址：https://cr.console.aliyun.com/#/accelerator

加速地址设置教程-> https://yq.aliyun.com/articles/29941


### 2.docker-compose.yml配置更改

选择你需要的功能，不需要的用#号注释掉

### 3.建立目录和文件
在`E`盘根目录下建立目录`www`和`work`目录，

在`www`目录下建立 `wwwroot`子目录

然后用户 sourceTree git客户端拉取本项目`docker-compose-nginx-php-mysql`
到 `work/docker-compose-nginx-php-mysql`目录下

### 1.选择要安装的系统和版本

例如：win系统 php7.1版本,进入`win-php71-swoole`目录
在命令行里进入该目录
```shell
cd e:/work/docker-compose-nginx-php-mysql/win-php71-swoole
```

wwwroot:自定义目录,默认目录

nginx/vhost：nginx 站点配置文件

在当前 `nginx/vhost` 目录下，配置你的 nginx站点，可以根据 `default.conf`进行修改

在 `E:/www/wwwroot/` 目录下
新建 `index.php`
```php
<?php
phpinfo();
```

>注意 如果你是自定义本地站点如`test.com`，那么就要在 `/etc/hosts` 加入本地host指向，编辑时需要`root`权限的哦

```SHELL
127.0.0.1 test.com
```

### 4.生成镜像
在命令行里进入该目录
```shell
cd e:/work/docker-compose-nginx-php-mysql/win-php71-swoole
```

这个时候 一定不能更换目录。

`注意` 如果你以前已经配置过一样的容器那么会自动覆盖容器
```
docker-compose up
```
时间比较长， 更新源都在国外，最好早晨拉取


完成后，在浏览器里面输入`localhost`回车，即可看到`phpinfo`输出信息

## 安装完成后 一定要配置PHP，主要启用PHP扩展
基本PHP 扩展已经启用，这里无须再启用

macphp71_1 容器名字可能生成的不一样


# X.问题
## X.1 权限问题
设置 可读写执行权限
```
chmod -R 777 /Volumes/work/wwwroot
```

### 更改下载镜像名称
下载镜像和容器前缀名称是根据当前项目目录名设置的。
例如当前项目目录为`mac-php71`，那么镜像和容器的前缀名为 `macphp71`

=============================================================
=============================================================
# 以下为 手动配置 从空白的 docker 如何集成 开发套件的简单步骤
## nginx 配置
本配置 nginx 默认启动时已经自动配置了，
以下是手动配置方法

进入nginx容器
```
docker exec -it compose_nginx_1 bash
```
`compose_nginx_1` 容器名字可能不一样
配置nginx.conf
```
vim /etc/nginx/nginx.conf
```
找到如下配置
```
include /etc/nginx/conf.d/*.conf;
```
修改为：（根据你自己分区名称置修改）
```
include /Volumes/work/vhost/*.conf; 
```
保存和退出容器

## php 配置
略 

跟nginx类似

# mysql 配置说明
```angular2html
docker exec -it mac-php71-swoole_mysql_1 bash

echo "sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES" >> /etc/mysql/mysql.conf.d/mysqld.cnf

```
