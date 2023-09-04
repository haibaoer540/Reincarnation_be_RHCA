# 0.0zZ项目介绍及更新说明
> 此项目起初是为了提供给`tuotooo`日常办公方便查找命令和相关资料创建。
>>内容主要包括，考RHCSA和RHCE证书涵盖的相关知识。
>>>:construction::rabbit::clamp::cyclone::fire:

# VMware 共享盘
> 在`VMware 虚拟机配置文件`中添加`disk.locking="FALSE"`和`scsi[n].sharedBus = "virtual"`。
# linux各版本基础命令
作为一个linux操作系统的用户，这些内容都是必须要掌握的。
>未做`🍡`标记的命令都是适用于linux各个版本。
## 关机/重启
- 关机
```
shutdown now
```
- 重启
```
reboot
```
## 绝对路径/相对路径
> `绝对路径` ：由`/`开头。
> 
> `相对路径` ：由`当前工作路径`开头。
## 网卡基础配置
- 查询当前网卡配置信息
```
ip addr
```
```
ifconfig
```
## 检查系统版本
```
uname -a
```
- 输出以下内容
  >`内核名`、`主机名`、`内核发行号`、`内核版本号`、`主机的硬件架构`、`操作系统名称`。
## 用户管理
> :mushroom:一个用户可以有多个组。
>
> `/etc/passwd`文件储存了`用户名`:`口令`:`用户uid`:`用户组gid`:`注释性描述`:`用户主目录`:`Shell路径`。
### 创建新用户

- useradd
  
  > useradd&nbsp;-d&nbsp;`用户主目录`&nbsp;-m&nbsp;-s&nbsp;`shell路径`&nbsp;`用户名`
  ```
  useradd -d /home/tuotuo -m -s /bin/sh tuotuo
  ```
>  $\color{#006666}{-p}$   
>> 未使用`-p`参数表示：创建用户时，默认创建与`用户名`相同的组；<br>
>> 使用`-p`参数表示：创建用户时，将用户加入指定`已存在的组`。
### 删除用户

- userdel

  > userdel&nbsp;-r&nbsp;`用户名`
  ```
  userdel -r xxx
  ```
### 修改用户信息

  - usermod
    
    > usermod&nbsp;-d&nbsp;`新的用户主目录`&nbsp;-m&nbsp;-s&nbsp;`新的shell路径`&nbsp;-g&nbsp;`其他用户组`&nbsp;-l&nbsp;`新的用户名`&nbsp;`用户名`
    ```
    usermod -d /home/tuo -m -s /bin/bash -g root -l tuo tuotuo
    ```
### 用户口令

- passwd

  > passwd `用户名`
  ```
  passwd tuotuo
  ```
## 用户组管理
> :mushroom:一个组可以有多个用户。
>
> `/etc/group`文件存储了`用户组名`:`口令`:`用户组gid`:`组内用户列表`。
### 创建用户组
  - groupadd
 
    > groupadd&nbsp;-g&nbsp;`用户组gid`&nbsp;`用户组名`
    ```
    groupadd -g 1020 tuotuo
    ```
### 修改用户组
- groupmod

  > groupmod&nbsp;–g&nbsp;`用户组gid`&nbsp;-n&nbsp;`新用户租名`&nbsp;`用户组名`
    ```
    groupmod –g 10000 -n tuo tuotuo
    ```
### 删除用户组
- groupdel

  > groupdel&nbsp;`用户组名`
    ```
    groupdel tuotuo
    ```
## 磁盘管理
> `/dev/`目录是储存磁盘表的地方。
### 创建新的主分区并挂载
> 使用`fdisk`创建新磁盘，再使用`mkfs`将磁盘格式化，最后使用`mount`将磁盘挂载。
- fdisk
  > 2TB以下磁盘空间。
  1. > fdisk -l
     
    - 输出以下内容
      
      > `所有物理盘的信息`,`所有逻辑分区的信息`。
  2. > fdisk `磁盘名称`
       ```
       fdisk /dev/sdb
       ```
  3. > Command (m for help): <kbd>n</kbd>
     
    - 输出操作提示
      |e|p|
      |:-:|:-:|
      |创建扩展分区|创建主分区|
  4. > Command (m for help): <kbd>w</kbd>
    - 保存并退出
      
- mkfs
  > 可以格式化大部分linux文件系统类型。
  - mkfs.`文件系统类型` `磁盘名称`
    ```
    mkfs.xfs /dev/sdb1
    ```
- mount
  -mount `磁盘名称` `文件目录`
  ```
  mount /dev/sdc1 /home/tuotuo
  ```
