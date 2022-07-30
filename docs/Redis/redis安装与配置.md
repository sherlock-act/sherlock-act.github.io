# Linux安装

## 安装gcc依赖

由于 redis 是用 C 语言开发，安装之前必先确认是否安装 gcc 环境

```shell
gcc -v
```

如果没有安装，执行以下命令进行安装（因为这一步没有做导致我执行安装命令一直报错）

```shell
yum install -y gcc
```



## 下载

从Redis官网下载选择对应版本下载

`https://download.redis.io/releases/`

也可以在终端中使用命令进行下载

>  `wget http://download.redis.io/releases/xxxxxxxxxxxxxx `

## 解压

> tar -zxvf redis-6.2.6.tar.gz

## 进⼊redis⽬录

> cd redis-6.3.6/

## 生成

> sudo make

## 测试

- 这段运⾏时间会较⻓

> sudo make test

- 如果test发生错误`You need tcl 8.5or newer in order to run the Redis test`
  - 下载tcl:
  - ` https://sourceforge.net/projects/tcl/ `
  - 解压tcl
  - 将解压后的tcl文件移动到`/usr/local`目录下
  - cd 到`/usr/local/tcl8.6.1/unix/`目录下
  - 执行命令`sudo  ./configure`
  - 安装tcl`sudo make install`

## 安装

- 将redis的命令安装到指定路径/usr/local/redis/⽬录

> `make install PREFIX=/usr/local/redis`

- 安装完成后，我们进入目录/usr/local/redis/bin中查看

  > cd /usr/local/redis/bin
  > ls -al

  ```shell
  drwxr-xr-x 2 root root    4096 7月  30 18:07 .
  drwxr-xr-x 3 root root    4096 7月  30 18:03 ..
  -rwxr-xr-x 1 root root 4829488 7月  30 18:03 redis-benchmark												redis性能测试工具
  lrwxrwxrwx 1 root root      12 7月  30 18:03 redis-check-aof -> redis-server				AOF文件修复工具
  lrwxrwxrwx 1 root root      12 7月  30 18:03 redis-check-rdb -> redis-server				RDB文件检索工具
  -rwxr-xr-x 1 root root 5003768 7月  30 18:03 redis-cli															redis命令行客户端					
  lrwxrwxrwx 1 root root      12 7月  30 18:03 redis-sentinel -> redis-server
  -rwxr-xr-x 1 root root 9518896 7月  30 18:03 redis-server													redis服务器
  ```

# 配置redis

## 复制配置文件

- redis下载目录下有`redis.conf`配置文件,将配置文件复制到移动到安装目录(`/usr/local/redis/bin`)下

- > `cp ~/redis-6.3.6/redis.conf /usr/local/redis/bin`

- 绑定ip：如果需要远程访问，可将此⾏注释，或绑定⼀个真实ip

  > bind 127.0.0.1

- 端⼝，默认为6379

  > port 6379

- 是否以守护进程运⾏

  - 如果以守护进程运⾏，则不会在命令⾏阻塞，类似于服务
  - 如果以⾮守护进程运⾏，则当前终端被阻塞
  - 设置为yes表示守护进程，设置为no表示⾮守护进程
  - 推荐设置为yes

  > daemonize yes

- 数据⽂件

  > dbfilename dump.rdb

- 数据⽂件存储路径

  > dir /var/lib/redis

- ⽇志⽂件

  > logfile /var/log/redis/redis-server.log

- 数据库，默认有16个

  > database 16

- 主从复制，类似于双机备份。

  > slaveof

## 启动服务

- 使用守护进程启动redis
  - 需要将配置文件中的`daemonize`设置为yes

```shell
# 启动服务
./redis-server redis.conf
# 查看进程
ps -ef |grep redis
```

## 设置开机启动

- 修改系统配置文件

```shell
cd /lib/systemd/system/
# 新建文件
vim redis.service
```

- 在文件中添加如下内容

```shell
[Unit]
Description=redis-server
After=network.target

[Service]
Type=forking
# ExecStart需要按照实际情况修改成自己的地址
ExecStart=/usr/local/redis/bin/redis-server /usr/local/redis/bin/redis.conf
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```

- 执行系统配置命令

```shell
# 开机自动启动
systemctl enable redis.service

# 以下为redis的服务其他命令
# 启动redis服务
systemctl start redis.service
# 查看服务状态
systemctl status redis.service
# 停止服务
systemctl stop redis.service
# 取消开机自动启动(卸载服务)
systemctl disabled redis.service
```

## 远程连接redis

- 如果需要远程连接redis的话需要关闭服务器防火墙

```shell
# 检查防火墙状态 看到active(running)就意味着防火墙打开了
sudo systemctl status firewalld
# 关闭防火墙
sudo systemctl stop firewalld
# 开启防火墙
sudo systemctl start firewalld
# 上面的命令是临时的，重启后就失效了
# 彻底关闭防火墙
sudo systemctl disable firewalld
```

- 并且开放端口

```shell
 # 开放redis端口
 firewall-cmd --zone=public --add-port=6379/tcp --permanent
 # 应用
 firewall-cmd --reload
```

