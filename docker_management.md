# docker安装
> [docker官网安装教程-将docker安装在各个操作系统](https://docs.docker.com/get-docker/)<br>

主要安装以下组件
- docker-ce
- docker-ce-cli
- containerd.io

# 镜像管理
## 查询所有已安装的镜像
```python
docker images
```
- 输出以下内容
  > `镜像的仓库源`、`版本`、`镜像ID`、`创建时间`、`大小`

## 搜索镜像
- docker search `镜像名`

  ```python
  docker search ubuntu
  ```
- 输出以下内容
  > `镜像的仓库源`、`描述`、`自动构建`、`官方标识`、`好评`
  
## 获取新镜像

- docker pull `镜像名`:`版本`

  ```python
  docker pull ubuntu:18.04
  ```

## 删除镜像
- docker rmi `镜像名`:`版本`
  
  ```python
  docker rmi ubuntu:18.04
  ```

# 容器管理

## 查询现有的容器
```python
docker ps -a
```

- 输出以下内容
  > `容器ID`、`镜像名`、`shell交互路径`等

## 创建并启动容器
- docker run -itd --name `容器名` `镜像名` `shell交互路径`

  ```c
  docker run -itd --name tuotuo ubuntu:18.04 /bin/bash
  ```

## 创建并启动进入容器
- docker run -it --name `容器名` `镜像` `shell交互路径`
  
  ```python
  docker run -it --name tuotuo ubuntu:18.04 /bin/bash
  ```
## 停止一个容器
- docker stop `容器ID`

  ```c
  docker stop o000tuotuo00
  ```
## 启动现有已停止的容器
- docker start `容器ID`
  
  ```python
  docker start o000tuotuo00
  ```
## 进入容器
- docker exec -it `容器ID` `shell交互路径`

  ```C
  docker attach o000tuotuo00 /bin/bash
  ```
