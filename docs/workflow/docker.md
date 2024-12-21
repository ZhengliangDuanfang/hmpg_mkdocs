!!! info "写在开头"
    对于Docker到底是做什么用的，我还没有找到过一个比较通俗的回答。我的看法是Docker可以用来复制并迅速环境，比方说你想模拟一下一个古早版本的Ubuntu，还要用到古早版本的Python之类，你就可以用Docker来快速搭建，而不用折腾你的WSL了。另外它也轻量很多，比方说你可以直接运行Python，而无需安装基础的Ubuntu环境。

## 用Dockerfile创建镜像

通过编写Dockerfile文件，可以指明建立Docker镜像需要的资源。

下面是一个例子，是写BS大作业时候用过的。
```dockerfile
# Description: Dockerfile for Java 17, Maven, MySQL

# 进入docker后，运行以下命令启动mysql
# bash /docker-entrypoint-init.d/start.sh

# 使用官方的Ubuntu 22.04镜像作为基础镜像
FROM ubuntu:22.04

# 设置环境变量，避免交互式配置
ENV DEBIAN_FRONTEND=noninteractive

# 替换 APT 源列表
RUN echo "deb http://mirrors.aliyun.com/ubuntu/ jammy main restricted universe multiverse" > /etc/apt/sources.list && \
    echo "deb http://mirrors.aliyun.com/ubuntu/ jammy-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb http://mirrors.aliyun.com/ubuntu/ jammy-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb http://mirrors.aliyun.com/ubuntu/ jammy-security main restricted universe multiverse" >> /etc/apt/sources.list

# 更新软件包列表并安装 OpenJDK 17、maven、mysql
RUN apt-get update && \
    apt-get install -y unzip wget && \
    apt-get install -y openjdk-17-jdk --fix-missing && \
    apt-get install -y maven && \
    apt-get install -y mysql-server && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# 验证Java安装
# RUN java -version
# RUN mvn -version

# 设置JAVA_HOME环境变量
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
ENV PATH=$JAVA_HOME/bin:$PATH

# 设置MAVEN_HOME环境变量
ENV MAVEN_HOME=/usr/share/maven
ENV PATH=$MAVEN_HOME/bin:$PATH

# maven换源 
RUN mkdir -p /root/.m2 && \
    echo '<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" \
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" \
    xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd"> \
    <mirrors> \
      <mirror> \
        <id>aliyun</id> \
        <mirrorOf>central</mirrorOf> \
        <name>Aliyun Maven</name> \
        <url>https://maven.aliyun.com/repository/public</url> \
      </mirror> \
    </mirrors> \
    </settings>' > /root/.m2/settings.xml

# 初始化MySQL
COPY init.sh /docker-entrypoint-init.d/
COPY init.sql /docker-entrypoint-init.d/
COPY start.sh /docker-entrypoint-init.d/
VOLUME ["/var/lib/mysql"]

RUN usermod -d /var/lib/mysql/ mysql
RUN bash /docker-entrypoint-init.d/init.sh

# 定义工作目录
WORKDIR /home/bs

# 暴露端口
EXPOSE 8080

# 设置容器启动时运行的命令
CMD ["bash"]
```

- 使用Dockerfile创建镜像：`docker build -t <image>:<version> .`注意最后这个表示在当前目录寻找Dockerfile文件的点。

## 用镜像创建容器

```shell
docker run -it -v <original data path>:<dest data path> \
--name <name> -p 8080:8080 <image>:<version>
```

这里面的`-v`表示将本机上的`original`路径映射到Docker中的`dest`路径，`-p`表示端口映射。

## 容器建立后的操作

以下所有的`<container>`既可以替换为容器的ID，也可以替换为容器的名字。
这里的ID是一个哈希码，可以通过`docker ps -a`查看。

- 查看所有容器：`docker ps -a`
- 启动容器：`docker start <container>`
- 停止容器：`docker stop <container>`
- 进入启动的容器：`docker attach <container>`
- 进入容器：`docker exec -it <container> /bin/bash`

!!! tip "start与exec的区别"
    `docker start`只能用于启动一个处于停止运行状态的容器，`docker exec`只能用于进入一个已经处于运行状态的容器，同时新开一个进程。

- 删除容器：`docker rm <container>`
- 删除镜像：`docker rmi <image>:<version>`

## 镜像的导入与导出

- 导出镜像：`docker save -o <filename>.tar <image>:<version>`
    - 批量导出：`docker save -o <filename>.tar <image1>:<version> <image2>:<version> ...`
- 导入镜像：`docker load -i <filename>.tar`

## 附录：Docker in OSLAB

在Lab1及以后，可以通过`make debug`在Docker中调试。具体流程如下：

1. 在当前项目目录中执行`make debug`

2. 远程调试
```shell
# 进入同一个 Docker 容器
$ docker exec -it oslab /bin/bash

# 切换到 labX 目录
$ cd /home/oslab/os_experiment/labx/

# 使用 GDB 进行调试
$ riscv64-unknown-linux-gnu-gdb vmlinux

# 远程连接
(gdb) target remote localhost:1234
```