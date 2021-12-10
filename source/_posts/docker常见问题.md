---
title: docker常见问题
date: 2021-11-25 11:37:12
author: waper97
tags: #标签
 - docker常见问题
 - docker常用命令
layout : post #公开文章 
comments: true #是否开启评论
categories: docker #分类
keywords: 常用命令 #文章关键字
---






### docker常用命令
```
 docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

```
[docker run 官方文档地址 ]( https://docs.docker.com/engine/reference/commandline/run/)

<!--more-->
**常用的Options**

| Name, shorthand名称、缩写 | Default | Description                                                  |
| -------------------------- | ------- | ------------------------------------------------------------ |
| `--detach` , `-d`          |         | Run container in background and print container ID :在后台运行容器并打印容器 ID |
| `--env` , `-e`             |         | Set environment variables : 设置环境变量                     |
| `--publish` , `-p`         |         | Publish a container's port(s) to the host:  将容器的端口发布到主机 |
| `--tty` , `-t`             |         | Allocate a pseudo-TTY :分配一个伪 TTY，即分配一个终端        |
| `-- name`                  |         | Assign a name to the container: 为容器指定名称               |
| `--volume` , `-v`          |         | Bind mount a volume :绑定挂载卷                              |
| `--interactive` , `-i`     |         | Keep STDIN open even if not attached ：即使未连接，也要保持 STDIN 打开   STDIN即（standard input：标准输入），还有STDOUT(standard out:标准输出)，STDEER( standard error :标准错误输出) |


docker 在容器运行时，可以通过ctrl+p 


**example:**

```
$ docker run -d -p 80:80 docker/getting-started
```

- -d    \- run the container in detached mode (in the background)   ：以分离模式运行容器（在后台）

- -p    - `80:80` - map port 80 of the host to port 80 in the container :   将主机的 80 端口映射到容器中的 80 端口





**![]()Tip** 可以缩写为

 ```	 
 $ docker run -dp 80:80 docker/getting-started
 
 ```








### docker容器中无法使用vim的问题
```java
- 1.输入apt-get update
- 2.输入apg-get install vim
    然后就ojbk了
```

### dockerfile参数

|    命令    |                             含义                             |
| :--------: | :----------------------------------------------------------: |
|    FROM    |                        基于什么构镜像                        |
| MAINTAINER |                            维护者                            |
|   EXPOST   |                          暴露的端口                          |
| ENTRYPOINT |                          追加的命令                          |
|    RUN     |                         要执行的命令                         |
|  WORKDIR   |                   为任何 RUN 设置工作目录                    |
|    ADD     |                          复制新文件  采用可识别压缩格式（identity、gzip、bzip2 或 xz）的本地 tar 存档，则将其解压缩为目录                         |
|    ENV     |                         设置环境变量                         |
|   VOLUME   |               指令创建一个具有指定名称的挂载点               |
|    COPY    | 指令从 <src> 复制新的文件或目录，并将它们添加到容器的文件系统中的路径 |

### docker 构建镜像命令
docker build -f xxxx -t xxxxx2 .

|    命令    |                             含义                             |
| :--------: | :----------------------------------------------------------: |
|   -f   |                        dockerfile文件           |
|   -t |                       tag 构建成镜像的名称       |

**这个点"." 别忘记**



### 创建自己的镜像
 

#### 1.DockerFile创建

{% codeblock lang:linux %}
[rectangle setX: 10 y: 10 width: 20 height: 20];

FROM centos
MAINTAINER waper97<563667426@qq.com> 维护人
COPY readMe.md /usr/local/readeMe.md 复制文件到指定路径
ADD jdk-8u311-linux-x64.tar.gz /usr/local/ 解压到指定路径下
ADD apache-tomcat-10.0.13.tar.gz /usr/local/ 解压到指定路径下

RUN yum -y install vim 执行命令
ENV MYPATH /usr/local
WORKDIR $MYPATH

ENV JAVA_HOME /usr/local/jdk1.8.0_311
ENV CLASSPATH_HOME $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
ENV CATALINA_HOME /usr/local/apache-tomcat-10.0.13
ENV CATALINA_BASH /usr/apache-tomcat-10.0.13
ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/lib:$CATALINA_HOME/bin 

EXPOSE 8080 暴露端口

CMD /usr/local/apache-tomcat-10.0.13/bin/startup.sh && tail -F /usr/local/apache-tomcat-10.0.13/logs/catalina.out




{% endcodeblock %}
#### 2.构建镜像
{% codeblock lang:linux %}

docker build -t mydockerimages(既自定义镜像的名称) .
**注意：** 最后面有个 "."这个别忘记了

{% endcodeblock %}

#### 3.启动容器
{% codeblock lang:linux %}
	docker run -d -p 9090:8080 --name wapertomcat \ 
	-v /home/test/tomcat/test:/usr/local/apache-tomcat-10.0.13/webapps/test \
	-v /home/test/tomcat/logs/:/usr/local/apache-tomcat-10.0.13/logs 42c9a5d678c0
{% endcodeblock %}

### docker启动出现 Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?

### Docker网络
#### docker 容器内部无法使用ip addr 

![在这里插入图片描述](https://img-blog.csdnimg.cn/ebde78c6a3ea485789d6a402577d1906.png)

可以使用

{% codeblock lang:linux %}
apt update && apt install -y iproute2
{% endcodeblock %}

![在这里插入图片描述](https://img-blog.csdnimg.cn/ae345c17e39b4b6881875536ecffd864.png)
#### linux内部可以ping通docker内的容器

原理:

{% codeblock lang:linux %}

{% endcodeblock %}

172.17.0.5
{% codeblock lang:linux %}
apt-get update && apt install iputils-ping &&  apt install net-tools 
{% endcodeblock %}
#### docker容器互链

#### --link 

容器之间的互联 ： 容器内部的host映射关系

#### 自定义网络

{% codeblock lang:linux %}

bridge: 桥接 （default）

none: 不配置网络

host: 合宿主机共享网络

container：容器

自定义网络会帮我们维护好了对应的关系
{% endcodeblock %}


#### 网络联通

{% codeblock lang:linux %}
[root@localhost ~]# docker network --help

Usage:  docker network COMMAND

Manage networks

Commands:
  connect     Connect a container to a network
  create      Create a network
  disconnect  Disconnect a container from a network
  inspect     Display detailed information on one or more networks
  ls          List networks
  prune       Remove all unused networks
  rm          Remove one or more networks


  connect     Connect a container to a network 链接一个容器到一个网络

{% endcodeblock %}
