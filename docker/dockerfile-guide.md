# Dockerfile详解
- [Dockerfile详解](#dockerfile详解)
  - [前置 - docker是什么](#前置---docker是什么)
  - [Dockerfile是什么](#dockerfile是什么)
    - [概述](#概述)
    - [如何使用](#如何使用)
  - [Dockerfile结构](#dockerfile结构)
    - [示例dockerfile](#示例dockerfile)
  - [Dockerfile构建过程解析](#dockerfile构建过程解析)
  - [Dockerfile语法格式](#dockerfile语法格式)
    - [.dockerignore file](#dockerignore-file)
  - [Dockerfile 常用命令](#dockerfile-常用命令)
    - [From/RUN](#fromrun)
    - [WorkDir / COPY / ADD](#workdir--copy--add)
    - [ENV EXPOSE](#env-expose)
    - [ENTRYPOINT vs CMD](#entrypoint-vs-cmd)
    - [ARG](#arg)
    - [ONBUILD](#onbuild)
    - [Healthcheck  /  Volume](#healthcheck----volume)
  - [Dockerfile 最佳实践](#dockerfile-最佳实践)
  - [分阶段构建](#分阶段构建)
  - [自定义构建镜像](#自定义构建镜像)
  - [docker镜像及生成方式](#docker镜像及生成方式)
## 前置 - docker是什么
* Docker是一套平台即服务（PaaS）产品，它使用操作系统级的虚拟化，以容器的形式来交付软件。

* Docker的主要好处是它允许用户将一个应用程序及其所有的依赖关系打包成一个标准化的单元(容器)，用于软件开发、交付。与虚拟机不同，主机上所有的容器都共享一个操作系统内核的服务，从而能够更有效地利用底层系统和资源。
  
* 容器之间相互隔离，它们可以通过明确定义的通道相互通信。
  
![Image](./assets/docker-architecture.png)


## Dockerfile是什么

### 概述
![Image](./assets/dockerfile01.png)

* Docker可以通过读取`Dockerfile`中的指令自动构建镜像。
* `Dockerfile`是一个文本文件，定义从一个镜像开始，它包含了用户可以在命令行上调用的所有命令，最后可以通过`docker build` 组装成一个镜像。
### 如何使用

* 一般情况下，`Dockerfile`会使用执行`docker build`命令的根目录下的`Dockerfile`, 当前你也可以使用`-f`指定`Dockerfile`的路径

```sh
# Dockerfile use current root path
$ docker build . 

# Dockerfile use -f flag to point.
$ docker build -f /path/to/a/Dockerfile .
```

* 构建镜像时指定镜像的tag
```sh
# image default use latest tag
$ docker build -t shykes/myapp .

# image use 1.0.2 tag
$ docker build -t shykes/myapp:1.0.2 .

# 当前你也可以同时指定多个镜像tag
$ docker build -t shykes/myapp:1.0.2 -t shykes/myapp:latest .
```

_注_: docker守护程序在`Dockerfile`中运行指令之前，会先执行一个初步验证，如果语法不正确将会返回错误，结束运行。

## Dockerfile结构

### 示例dockerfile

```dockerfile
# syntax=docker/dockerfile:1
FROM ubuntu:18.04
LABEL maintainer="Colynn Liu <colynn.liu@gmail.com>"

WORKDIR /app
COPY . /app
RUN mkdir /app/logs

EXPOSE 8080
CMD python /app/app.py
```
#

![Image](./assets/dockerfile02.png)

注解：
1. Dockerfile 头信息
2. Dockerfile 命令集合
3. Dockerfile 运行时声明

## Dockerfile构建过程解析
    * 分阶段构建 

## Dockerfile语法格式

```Dockerfile
# Comment
INSTRUCTION arguments
```

* Dockerfile命令是不区别大小写的，而我们习惯性用大写，因为这样可以更好与参数区别。

* Docker会按照顺序运行Dockerfile内的指令。__`Dockerfile`必须以`FROM`指令开始__,当然`FROM`也是可以在[解析器指令](https://docs.docker.com/engine/reference/builder/#parser-directives)、注释或是全局范围的[ARG](https://docs.docker.com/engine/reference/builder/#arg)之后。

_注_: [解析器指令](https://docs.docker.com/engine/reference/builder/#parser-directives)是可选的（很少用到），目前仅有`syntax`/`escape` 这两个解析器指令的定义。


### .dockerignore file


##  Dockerfile 常用命令

### From/RUN

### WorkDir / COPY / ADD 

### ENV EXPOSE 

### ENTRYPOINT vs CMD 
    * CMD特点
    * 含义及区别


### ARG
The ARG instruction defines a variable that users can pass at build-time to the builder with the docker build command using the --build-arg <varname>=<value> flag. If a user specifies a build argument that was not defined in the Dockerfile, the build outputs a warning.

### ONBUILD

### Healthcheck  /  Volume

## Dockerfile 最佳实践
* https://docs.docker.com/develop/develop-images/dockerfile_best-practices/


## 分阶段构建
* https://docs.docker.com/develop/develop-images/multistage-build/


## 自定义构建镜像
* https://docs.docker.com/develop/develop-images/baseimages/


## docker镜像及生成方式
  * 通过docker容器生成镜像
  * 通过dockerfile生成镜像；
