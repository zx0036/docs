# Dockerfile详解

## 前置条件 - docker是什么

## Dockerfile是什么

Docker can build images automatically by reading the instructions from a Dockerfile. 
A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. 
Using docker build users can create an automated build that executes several command-line instructions in succession.

    * 示例dockerfile

## Dockerfile结构；


## Dockerfile构建过程解析
    * 分阶段构建 

## Dockerfile常用命令

### From/RUN

### WorkDir / COPY / ADD 

### ENV EXPOSE 

### ENTRYPOINT vs CMD 
    * CMD特点
    * 含义及区别


### ？？ ONBUILD ARG

### ？？ Healthcheck  /  Volume

## Dockerfile 最佳实践
* https://docs.docker.com/develop/develop-images/dockerfile_best-practices/


## 分阶段构建
* https://docs.docker.com/develop/develop-images/multistage-build/


## 自定义构建镜像
* https://docs.docker.com/develop/develop-images/baseimages/


# ## docker镜像及生成方式
#     * 通过docker容器生成镜像
#     * 通过dockerfile生成镜像；