



## 1：Docker 

https://docs.docker.com/engine/install/centos/

docker 厂库 docker.hub.com 

2: <img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210419213329388.png" alt="image-20210419213329388" style="zoom:50%;" />

虚拟机技术的缺点：

1. 资源占用十分多

2. 冗余步骤多

3. 启动慢

4. <img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210419213543700.png" alt="image-20210419213543700" style="zoom:50%;" />

   

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210419213736359.png" alt="image-20210419213736359" style="zoom:67%;" />

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210419214145679.png" alt="image-20210419214145679" style="zoom:80%;" />

## 1: docker 的安装

centos7 

1 uname -r   查看系统版本

2： cat /etc/os-release

 yum makecache fast  # 更新索引

systemctl start docker  

docker version

docker run hello-world

docker images 

```
1 : 卸载旧的docker  在官网上看安装步骤

```

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210419215447579.png" alt="image-20210419215447579" style="zoom: 80%;" />

### d**ocker 是什么工作的？**

Docker是一个client-server 结构的系统，Docker的守护进程运行在主机上，通过Socker从客服端访问！

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210419220213341.png" alt="image-20210419220213341" style="zoom: 50%;" />



DockerServer 接受到Docker-client的指令，就会执行命令

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210419220054515.png" alt="image-20210419220054515" style="zoom:50%;" />



Docker 为什么比VM快？

1. docker 比VM更少的抽象层
2. docker利用的是宿主机的内核。VM需要Guest OS

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210419220329985.png" alt="image-20210419220329985" style="zoom:50%;" />

新建一个容器的时候，docker不需要像虚拟机一样重新加载一个操作系统，避免引导，虚拟机加载的是Guest OS， 分钟级别的， 而docker是利用宿主机的操作系统，秒级。

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210419220403683.png" alt="image-20210419220403683" style="zoom:80%;" />



**docker 常用 commend：**

docker version

 docker  info

## 2： **镜像命令**

##### docker images   --help   查看本地的主机镜像

![image-20210323144726792](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210323144726792.png)

- Repository : 镜像的仓库源  Tag 镜像的标签 版本  
- docker images -a    
- docker images -q   
-  docker images -aq      # 可选项

##### **docker search  搜索镜像**

 docker search mysql  	

dokcer search -help

可选项   --filter  

![image-20210323145458897](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210323145458897.png)

##### **docker pull 下载**

docker pull mysql

docker pull mysql:5.7  指定版本

![image-20210323150409099](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210323150409099.png)

![image-20210323150517387](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210323150517387.png)

分层下载  节约内存

##### docker rmi  删除镜像

docker rmi -f id1 ,id2

全部删除镜像

docker rmi  -f $(docker images -aq)

![image-20210323150927108](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210323150927108.png)

## 3：**容器命令**

有了镜像才可以创建容器，  linux ， 下载一个centos 镜像

### docker pull centos

### 新建容器并启动

### docker run [可选参数]  image

参数说明

![image-20210323151632276](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210323151632276.png)

![image-20210323151848250](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210323151848250.png)

![image-20210323152116466](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210323152116466.png)

### **停止容器**：

exit

ctrl + P +Q 容器不停止

### 删除容器

![image-20210323152900051](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210323152900051.png)

![image-20210324153544782](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210324153544782.png)

### 查看容器进程ps

![image-20210324154045209](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210324154045209.png)

### docker inspect 

### 进入正在运行的容器

![image-20210324154756359](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210324154756359.png)

![image-20210324154826359](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210324154826359.png)

### 从容器中复制到物理机

![image-20210324160130683](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210324160130683.png)

![image-20210324160426547](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210324160426547.png)

## 4： docker 部署nginx

![image-20210420202958471](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210420202958471.png)

![image-20210420203042487](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210420203042487.png)

### 端口暴露的概念：

<img src="C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210420203128919.png" alt="image-20210420203128919" style="zoom:50%;" />

### docker 部署tomcat

![image-20210420204852179](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210420204852179.png)

### docker stats id 查看占用资源



## 5： portainer 

docker run -d -p 8088:9000 --restart=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer

curl localhost:8088

启动： sudo systemctl restart docker

## 6： Docker 镜像讲解

镜像是一种轻量级，可执行独立软件包，用来打包软件运行环境和基于运行环境开发的软件，它包含运行某个软件所需的所有内容，包括代码，运行时，库，环境变量和配置文件。

所有的应用，直接打包docker镜像，可以直接运行

如何得到镜像：

1. 从远程厂库下载
2. 朋友拷贝
3. 自己制作一个dockerFile镜像

![image-20210505195354255](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210505195354255.png)

![image-20210505195420085](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210505195420085.png)

![image-20210505195532227](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210505195532227.png)

![image-20210505195551625](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210505195551625.png)

![image-20210505195631618](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210505195631618.png)

#### Commit 镜像：

![image-20210505200940681](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210505200940681.png)

![image-20210505200958213](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210505200958213.png)

## 7： 容器数据卷

![image-20210507202431585](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210507202431585.png)

### 容器的持久化和同步操作！ 容器间也是可以数据共享的

![image-20210507203316431](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210507203316431.png)

![image-20210507203609014](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210507203609014.png)

```bash
docker run -d -p 3310:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql -e  MYSQL_ROOT_PASSWORD=123456 --name mysql01 mysql:5.7

```

![image-20210507205732601](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210507205732601.png)

![image-20210507210104966](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210507210104966.png)

### 2： 具名和匿名挂载：

![image-20210507210556614](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210507210556614.png)

![image-20210507210810671](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210507210810671.png)

## 8: Dockerfile:

![image-20210519203211691](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210519203211691.png)

这里的每个命令，就是镜像的一层

### ![image-20210519203924294](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210519203924294.png)

### 数据卷容器：

--volumes-from 

![image-20210519205733012](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210519205733012.png)



![image-20210519211522108](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210519211522108.png)

![image-20210519211456302](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210519211456302.png)

docker01 02 数据共享

![image-20210519211616027](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210519211616027.png)

![image-20210519211644914](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210519211644914.png)

![image-20210519211722915](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210519211722915.png)

![image-20210519211753858](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210519211753858.png)

## DockerFile介绍

![image-20210519212055916](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210519212055916.png)

## DockerFile构建过程



![image-20210519212425063](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210519212425063.png)

![image-20210519212510917](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210519212510917.png)



## DockerFile 指令

![image-20210519213026591](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210519213026591.png)

WorkDIR: 切换目录

copy:  不解压 ，只拷贝

copy  本地文件【可以多个】  容器路径 [/home] 

copy 指令 能保留原文件的元数据， 权限，访问时间

ADD :  

1. 原文件是一个url  docker 会下载，如果原文件是一个url，且是压缩包，不会自动解压，也得单独使用RUN 指令
2. 源文件是一个压缩文件， gzip tar , xz  ADD 会自动解压文件到目标路径

CMD： 默认参数

![image-20220603103142182](../../../Users/Mrwang/Desktop/Note/pic/image-20220603103142182.png)

entroypoint :  可以追加 参数  CMD 不行 

ENV 和ARG

区别： ENV 无论是在镜像构建的时候，还是容器运行的时候，该变量都可以使用

ENV  环境变量 Var_name 调用 $Var_name

ARG :  只是用于构建镜像需要的设置，容器运行时就消失

VOLUME： 容器运行时，应该保证在存储层不写入任何数据，运行在容器内产生的数据，推荐写到宿主机，进行维护

~~~python
VOLUME  ["/data1","/data2"]  # 将容器内的 /data文件夹
~~~

USER root



#创建一个自己的centos 

### 1: 编写DockeFile 文件

![image-20210520211005218](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210520211005218.png)

![image-20210520211057107](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210520211057107.png)

![image-20210520212023637](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210520212023637.png)

![image-20210520212034554](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210520212034554.png)

docker history 

![image-20210520212253182](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210520212253182.png)

![image-20210520212339242](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210520212339242.png)

![image-20210520212608357](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210520212608357.png)

![image-20210520212732314](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210520212732314.png)

![image-20210520212751431](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210520212751431.png)

### 实战： Tomcat 镜像

![image-20210520212900414](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210520212900414.png)

![image-20210520213439697](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210520213439697.png)

![image-20210520213346282](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210520213346282.png)

![image-20210520214142874](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210520214142874.png)

![image-20210520214222377](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210520214222377.png)

![image-20210520214301881](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210520214301881.png)

### 发布自己的镜像：

![image-20210520214359931](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210520214359931.png)

![image-20210520214420251](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210520214420251.png)

![image-20210520214607336](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210520214607336.png)

## 小结：

![image-20210520214942843](C:\Users\Mrwang\AppData\Roaming\Typora\typora-user-images\image-20210520214942843.png)

