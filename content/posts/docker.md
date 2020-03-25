+++
title = "Docker学习笔记"
author = ["jirex"]
lastmod = 2020-03-25T14:05:41+08:00
draft = false
+++

## 概念 {#概念}


### 镜像 （image) {#镜像-image}

-   相当于启动盘，系统盘
-   分层存储，有点像git，类似指针的概念

    {{< figure src="https://raw.githubusercontent.com/jirex/static-center/master/img/20200325133640.png" width="50%" >}}


### 容器 （container) {#容器-container}

-   从镜像启动，类 和 实例的关系
-   会在镜像基础上，添加一层存储层，但容器被删除时，存储层的改变也会被删除，所以不要在里面写入任何数据，用数据卷


### 仓库 （Repository） {#仓库-repository}

-   镜像的仓库


## 安装 {#安装}


### centos {#centos}

-   删除旧版本

    ```bash
    sudo yum remove docker \
               docker-client \
               docker-client-latest \
               docker-common \
               docker-latest \
               docker-latest-logrotate \
               docker-logrotate \
               docker-selinux \
               docker-engine-selinux \
               docker-engine
    ```
-   使用yum安装

    ```bash
    # step 1: 安装必要的一些系统工具
    sudo yum install -y yum-utils device-mapper-persistent-data lvm2
    # Step 2: 添加软件源信息
    sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
    # Step 3: 更新并安装 Docker-CE
    sudo yum makecache fast
    sudo yum -y install docker-ce
    # Step 4: 开启Docker服务
    sudo service docker start
    ```
-   建立docker用户组，不用sudo来启动docker

    ```bash
    #建立docker用户组
    sudo groupadd docker
    #将当前用户加入用户组
    sudo usermod -aG docker $USER
    ```
-   测试安装

    ```bash
    docker version
    ```
-   镜像加速 (如果服务器在国内)
    编辑 `/etc/docker/daemon.json`, 然后重启docker

    ```json
    {
       "registry-mirrors": [
           "https://dockerhub.azk8s.cn",
           "https://hub-mirror.c.163.com"
       ]
    }
    ```


## 理念 {#理念}


### 一个容器只跑一个程序, 容器间通过网络交互 {#一个容器只跑一个程序-容器间通过网络交互}


### 分层存储， 容器间相互隔离，但他们的底层是共享的 {#分层存储-容器间相互隔离-但他们的底层是共享的}


## Dockerfile {#dockerfile}


### 常用命令 {#常用命令}


#### FROM {#from}

`FROM ubuntu:latest`
指定基础镜像


#### RUN {#run}

`RUN ls -al`
运行命令


#### COPY {#copy}

`COPY . /var/www/`
复制文件到容器内部
`COPY [--chown=<user>:<group>] <源路径>... <目标路径>`


#### CMD {#cmd}

`CMD ["node","test.js"]`
容器启动命令，保持容器启动，需要程序不以daemon形式运行


#### ENTRYPOINT {#entrypoint}

`ENTRYPOINT ["docker-entrypoint.sh"]`
容器运行前准备工作入口点，在CMD前执行，不常用


#### ENV {#env}

ENV Host="local" IsTest=true
环境变量, php、python都有获取环境变量的方法


#### WORKDIR {#workdir}

`WORKDIR /usr/share/nginx/html/`
切换工作目录，接下去的命令都会在这个目录下执行
不要用RUN cd ...


### 指令区分 {#指令区分}


#### RUN、CMD、ENTRYPOINT {#run-cmd-entrypoint}

-   RUN 指令是在容器被构建时运行的命令
-   CMD 、 ENTRYPOINT 是启动容器时执行 shell 命令
-   ENTRYPOINT在CMD前


#### ADD、COPY {#add-copy}

-   复制文件都用COPY
-   ADD可以解压缩文件


## docker-compose {#docker-compose}


### 目的 {#目的}

像web这种需要多种程序一起运作，比如php、redis等，需要把多个容器组成一个项目，单独用Dockfile不好管理，
还需要容器之间交互, docker-compose比较简单，还有k8s比较流行


### 安装 {#安装}

-   mac自带
-   linux

<!--listend-->

```bash
curl -L https://github.com/docker/compose/releases/download/1.25.4/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```


### docker-compose.yml文件常用命令 {#docker-compose-dot-yml文件常用命令}


#### image {#image}

指定镜像，可以不用写dockerfile


#### build {#build}

指定Dockerfile文件路径，可以是相对路径

```yaml
version: '3'
services:

    webapp:
        build: ./dir
```

也可以指定Dockerfile名字

```yaml
version: '3'
services:

    webapp:
        build:
            context: ./dir
            dockerfile: Dockerfile-alternate
```


#### command {#command}

容器启动后执行的命令，和Dockerfile中的CMD是一样的


#### container\_name {#container-name}

容器名字，挺有用的，以后看log的时候方便


#### depends\_on {#depends-on}

容器依赖的其他容器，可以在其他容器启动后再启动

```yaml
version: '3'

services:
    web:
        build: .
        depends_on:
        - db
        - redis

    redis:
        image: redis

    db:
        image: postgres
```


#### environment {#environment}

指定环境变量

```yaml
environment:
    - IsTest='true'
    - Host=local
```


#### ports {#ports}

暴露端口信息，可以让宿主机用

```yaml
ports:
  - "3000"
  - "8000:8000"
  - "49100:22"
  - "127.0.0.1:8001:8001"
```


#### volumes {#volumes}

挂载宿主机路径到容器，可读可写，可以用于开发环境，不用重启容器

```yaml
volumes:
    - /var/lib/mysql
    - cache/:/tmp/cache
    - ~/configs:/etc/configs/:ro
```


#### restart {#restart}

如果容器出错停止，是否重启，可以不用守护程序了，比如forever

```yaml
restart: always
```


#### env\_file {#env-file}

环境变量文件, docker-compose默认会读取系统和当前文件夹下.env文件

```yaml
env_file:
  - ./common.env
  - ./apps/web.env
  - /opt/secrets.env
```


## 常用命令 {#常用命令}


### docker-compose up --build -d {#docker-compose-up-build-d}

启动整个项目
`--build` 代表重新构建容器
`-d` 代表以daemon运行


### docker-compose stop {#docker-compose-stop}

停止整个项目


### docker-compose ps {#docker-compose-ps}

查看项目运行状态


### docker image ls -a {#docker-image-ls-a}

列出所有下载的镜像


### docker container ls -a {#docker-container-ls-a}

列出所有容器，包括停止的


### docker image prune {#docker-image-prune}

清除无用的镜像，没被现存容器用到的，加 `-a` 是清除所有


### docker container prune {#docker-container-prune}

清除所有容器


### docker exec -it <contaner id> bash {#docker-exec-it-contaner-id-bash}

运行命令，进入容器


### docker-compose logs --tail 10 -f {#docker-compose-logs-tail-10-f}

查看log
`--tail 10` 代表读出最后10条
`-f` 代表以daemon运行的项目读log时候不退出，不停打印最新的log


## node项目样例 {#node项目样例}


### Dockfile {#dockfile}

```yaml
FROM node:latest

#npm换源
RUN npm config set registry https://registry.npm.taobao.org

COPY ./package.json /home/node/package.json

WORKDIR /home/node

RUN npm install

COPY ./ /home/node

```


### docker-compose.yml {#docker-compose-dot-yml}

```yaml
 version: "3"
 services:

 node:
     container_name: node
     build: .
     volumes:
         - ./:/home/node
     command: "node test.js"
#tail -f /dev/null 用来保存容器运行状态
```
