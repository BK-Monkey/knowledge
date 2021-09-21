# shell 常用命令

# 所有命令均可加 --help 参数查看帮助信息

示例：

```
ps --help
```

# 管道符

管道符就是竖线 “|”，用于将前一个命令的输出传递给后一个命令。

示例：将ps -ef 输出的信息传递给grep 命令，用于过滤出含有nginx 字符的行。

```shell
ps -ef | grep nginx
```



# 命令执行

系统命令在任何路径下都可执行，例如 ps、ifconfig、kill 等命令

自己编译的二进制文件或者 shell 脚本，有两种执行方式

1. cd 到对应目录，使用 ./xxxx  或者 ./xxxx.sh 执行，例如 ./install.sh 
2. 使用绝对路径执行，例如  /data/znbase/install.sh 

 

# 进程

## 查看进程ID:    

```shell
ps -aux | grep  {进程独有的关键字}
后者 ps -ef | grep  {进程独有的关键字}
```

示例,第二列为进行ID

```shell
root@ecs-20210414092352:/data/zapfortest# ps -aux | grep nginx
root      1603  0.0  0.0 141356  7072 ?        Ss   Jun16   0:00 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;

root@ecs-20210414092352:/data/zapfortest# ps -ef | grep nginx
root      1603     1  0 Jun16 ?        00:00:00 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;

```

## 杀死进程：     

```shell
kill -9   {进程ID}
```

示例

```shell
kill -9 1603
```

## 批量杀进程

```
ps -ef | grep {进程独有的关键字} | grep -v grep | awk '{print $1}' | xargs kill -9
```

示例：

```
ps -ef | grep nginx | grep -v grep | awk '{print $1}' | xargs kill -9
```



## 后台运行:   

```shell
nohup {command} &  
```

注： 需要使用exit退出终端，否则也无法后台运行    

示例：

```shell
nohup java -jar xxxxx.jar &
```



# 网络

## 查看ip

```shell
ifconfig 或者 ip addr
```



# 文件操作 

## 查看文件全部内容：  

```shell
cat {文件路径}
```

示例：

```shell
root@ecs-20210414092352:/data/zapfortest/logs# cat test.txtaaaaaaaaaaaaaaa
```

## 查看文件最后几行 ： 

```
cat {文件路径} | tail -n {要显示的行数}
```

示例，显示文件最后5 行

```shell
root@ecs-20210414092352:/data/zapfortest/logs# cat monitorauth.log.2021-08-25.log | tail -n 5        at org.eclipse.jetty.io.FillInterest.fillable(FillInterest.java:103)        at org.eclipse.jetty.io.ChannelEndPoint$1.run(ChannelEndPoint.java:104)        at org.eclipse.jetty.util.thread.QueuedThreadPool.runJob(QueuedThreadPool.java:806)        at org.eclipse.jetty.util.thread.QueuedThreadPool$Runner.run(QueuedThreadPool.java:938)        at java.lang.Thread.run(Thread.java:748)
```

## 分页显示文件：

```
cat {文件路径} | more
```

示例：按回车会向后翻页

```shell
root@ecs-20210414092352:/data/zapfortest/logs# cat monitorauth.log.2021-08-25.log | more2021-08-25 09:52:58.054 [main] INFO  com.inspur.monitor.MonitorApplication - Starting MonitorApplication v1.0-SNAPSHOT on ecs-20210414092352 with PID 25914 (/data/zapfortest/MonitorAlertCenter-1.0-SNAPSHOT.jar started by root in /data/zapfortest)2021-08-25 09:52:58.056 [main] INFO  com.inspur.monitor.MonitorApplication - The following profiles are active: dev2021-08-25 09:52:58.743 [main] INFO  o.s.d.r.config.RepositoryConfigurationDelegate - Bootstrapping Spring Data JPA repositories in DEFERRED mode.2021-08-25 09:52:58.851 [main] INFO  o.s.d.r.config.RepositoryConfigurationDelegate - Finished Spring Data repository scanning in 96ms. Found 7 JPA repository interfaces.2021-08-25 09:52:59.283 [main] INFO  org.eclipse.jetty.util.log - Logging initialized @2161ms to org.eclipse.jetty.util.log.Slf4jLog2021-08-25 09:52:59.431 [main] INFO  o.s.b.w.e.jetty.JettyServletWebServerFactory - Server initialized with port: 80812021-08-25 09:52:59.434 [main] INFO  org.eclipse.jetty.server.Server - jetty-9.4.30.v20200611; built: 2020-06-11T12:34:51.929Z; git: 271836e4c1f4612f12b7bb13ef5a92a927634b0d; jvm 1.8.0_282-8u282-b08-0ubuntu1~18.04-b08
```



## 编辑文件

```shell
vim 或者 vi
```

按i 或者a 进入编辑模式，
esc 退出编辑模式，
shift + : ,  输入 wq 保存退出，
shift + : ,  q! 不保存退出。

示例：

```shell
vim test1.txt
```

有这个文件就是直接打开，没有则新建

此时是浏览模式，按 i 或者 a,进入编辑模式，随便输入内容。

然后按 esc 退出编辑模式。

在继续按 shift + :,此时屏幕最下方会出现：，

输入 wq 按enter ，会保存文件，并且退出。

输入 q! ,按enter，会不保存退出。



## 创建文件夹：  

```shell
mkdir
```

示例:   -p 参数会建立多级路径，如果没有test1, 如果不加-p ，命令会失败，如果加上-p，则会成功执行，test1 test2  test3 均会建立。

```shell
mkdir -p /data/test1/test2/test3
```



## 复制文件

```shell
cp {source} {dist}
```

示例：将text.txt 复制一份，命名为text1.txt

```shell
cp test.txt  text1.txtcp /data/text.txt  /data/text1.txt
```



## 移动或者重命名文件

```shell
mv {source} {dist}
```

示例： 将 test.text 重命名为text1.txt

```shell
mv test.txt  text1.txtmv /data/test.txt  /data/text1.txt
```

## 删除文件或者文件夹

```
rm 
```

示例: -r 递归删除，-f 不提示 强制删除，（**慎用**），使用的话，一定保证指定的文件或者文件夹存在。

```
rm -rf /data/logs/
```



## 查看文件列表

```
ls
```

示例： 查看隐藏文件和

```shell
root@ecs-20210414092352:/data/zapfortest# ls -altotal 488drwxr-xr-x  6 root root   4096 Aug 25 14:34 .drwxr-xr-x 14 root root   4096 Aug  9 16:55 ..drwxr-xr-x  2 root root  12288 Aug 25 14:34 libdrwxr-xr-x  2 root root   4096 Aug 26 09:47 logs-rw-r--r--  1 root root 110897 Aug 25 14:03 MonitorAlertCenter-1.0-SNAPSHOT.jar-rw-r--r--  1 root root  70409 Aug 17 10:26 MonitorAlertCenter-1.0-SNAPSHOT.jar.bak-rw-------  1 root root 270941 Aug 26 09:19 nohup.outdrwxr-xr-x  3 root root   4096 Aug  5 10:11 resourcesdrwxr-xr-x  2 root root   4096 Aug 23 18:11 Template
```

drwxr-xr-x  6 root root   4096 Aug 25 14:34 .

drwxr-xr-x  ： 

第一位 d 标识为文件夹

二三四位  rwx 标识拥有者的全新啊，为 r 可读，w 可写， x 可执行

五六七位  r-x 标识 用户组的权限，r 为可读，- 不可写，x 可执行

八九十 位  r-x  标识 其他用户的权限，r 为可读，- 不可写，x 可执行

第一个 root 标识这个文件的拥有者是root

第二个 root 标识这个root 所在的用户组为root。



## 文件权限管理

```shell
chmod
```

示例：

```shell
chmod 751 install.sh  给全部用户赋予chmod +x install.sh，给文件服务可执行权限。
```

文件有三种权限，读 写 可执行，读：4  写：2 ： 可执行：1

文件调用权限分为三级 : 文件所有者（Owner）、用户组（Group）、其它用户（Other Users）

 751  三位数字，

第一个7 代表 所有者权限， 7 = 4+2+1 ,说明 所有者有这个文件的读写和可执行权限。

第二个5 代表 用户组权限， 5 = 4+1 ,说明 所有者有这个文件的读 和可执行权限。

第三个1 代表 其他用户权限， 1=1 ,说明 其他用户有这个文件的可执行权限。

***


# 环境变量

查看环境变量

```shell
export
```

示例：

```
root@ecs-20210414092352:/data/zapfortest/logs# exportdeclare -x GOPATH="/usr/local/go"declare -x HISTFILE="/root/.history."declare -x HISTTIMEFORMAT="[%Y-%m-%d %H:%M:%S] [] [root] "declare -x HOME="/root"declare -x LANG="en_US"declare -x LAST_CMD=""declare -x LESSCLOSE="/usr/bin/lesspipe %s %s"declare -x LESSOPEN="| /usr/bin/lesspipe %s"declare -x LOGNAME="root"
```

修改环境变量：

```
export http_proxy="http://[user]:[pass]@host:port/" 
```

删除环境变量

```
export -n http_proxy
```



#  在线软件管理命令

## debian  ubuntu

```shell
apt-get
```

示例：安装nginx 和 docker

```shell
apt-get install nginx docker 
```

## rehat centos 

```shell
yum
```

示例：安装nginx 和 docker

```shell
yum install nginx docker
```



***

# 服务管理命令

## systemctl 

从新加载服务列表

```shell
systemctl daemon-reload
```

设定服务开机启动

```shell
systemctl enable ${servicefile}
```

示例

```shell
systemctl enable nginx
```

服务启动

```shell
systemctl start ${servicefile}
```

示例

```shell
systemctl start nginx
```

停止服务

```shell
systemctl stop ${servicefile}
```

示例

```shell
systemctl stop nginx
```

禁止服务开机启动

```shell
systemctl disable ${servicefile}
```

示例：

```shell
systemctl disable nginx
```



## 服务文件位置

### ubuntu

```shell
/etc/systemd/system
```

### centos

```shell
/usr/lib/systemd/system
```



### 服务文件内容示例：

```shell
[Unit]Description=prometheus project[Service]Type=simpleExecStart=${basePath}/start.sh ${basePath}Restart=alwaysRestartSec=5PrivateTmp=true[Install]WantedBy=multi-user.target
```



# 重启系统

```shell
reboot
```



# 远程操作命令

远程连接

```shell
ssh 
```

示例：远程连接到172.31.0.31 ，172.31.0.31使用的ssh 端口为 29

```shell
ssh -p 29 root@172.31.0.31 
```



远程复制文件

``` shell
scp
```

示例： 将当前目录下的 test.txt 文件复制到172.31.0.31 的tmp 目录下，172.31.0.31使用的ssh 端口为 29

```shell
scp -P 29 test.txt root@172.31.0.31:/tmp/
```


