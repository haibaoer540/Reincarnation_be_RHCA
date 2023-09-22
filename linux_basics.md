## 关机/重启
- 关机
```python
shutdown now
```
- 重启
```python
reboot
```
## 查看网卡配置
- 查询当前网卡配置信息
```python
ip addr
```
```python
ifconfig
```
## 检查系统版本
```python
uname -a
```
- 输出以下内容
  >`内核名`、`主机名`、`内核发行号`、`内核版本号`、`主机的硬件架构`、`操作系统名称`。
## 用户管理
> :mushroom:一个用户可以有多个组。<br>
> `/etc/passwd`文件储存了`用户名`:`口令`:`用户uid`:`用户组gid`:`注释性描述`:`用户主目录`:`Shell路径`。
### 创建新用户
  > useradd&nbsp;-d&nbsp;`用户主目录`&nbsp;-m&nbsp;-s&nbsp;`shell路径`&nbsp;`用户名`
  ```python
  useradd -d /home/tuotuo -m -s /bin/sh tuotuo
  ```
> 未使用`-p`参数表示：创建用户时，默认创建与`用户名`相同的组；<br>
> 使用`-p`参数表示：创建用户时，将用户加入指定`已存在的组`。
### 删除用户
> userdel&nbsp;-r&nbsp;`用户名`
```python
userdel -r xxx
```
### 修改用户信息
> usermod&nbsp;-d&nbsp;`新的用户主目录`&nbsp;-m&nbsp;-s&nbsp;`新的shell路径`&nbsp;-g&nbsp;`其他用户组`&nbsp;-l&nbsp;`新的用户名`&nbsp;`用户名`
```python
usermod -d /home/tuo -m -s /bin/bash -g root -l tuo tuotuo
```
### 用户口令
  > passwd `用户名`
  ```python
  passwd tuotuo
  ```
## 用户组管理
> :mushroom:一个组可以有多个用户。<br>
> `/etc/group`文件存储了`用户组名`:`口令`:`用户组gid`:`组内用户列表`。
### 创建用户组
> groupadd&nbsp;-g&nbsp;`用户组gid`&nbsp;`用户组名`
  ```python
  groupadd -g 1020 tuotuo
  ```
### 修改用户组
> groupmod&nbsp;–g&nbsp;`用户组gid`&nbsp;-n&nbsp;`新用户租名`&nbsp;`用户组名`
```python
groupmod –g 10000 -n tuo tuotuo
```
### 删除用户组
> groupdel&nbsp;`用户组名`
  ```python
  groupdel tuotuo
  ```
## 磁盘管理
> `/dev/`目录是储存磁盘表的地方。
### 创建新的主分区
- fdisk
  > 2TB以下磁盘空间。
  1. > fdisk -l 
    - 输出以下内容 
      > `所有物理盘的信息`,`所有逻辑分区的信息`。 
  2. > fdisk `磁盘名称`     
       ```python
       fdisk /dev/sdb
       ```       
  3. > Command (m for help): <kbd>n</kbd>  
    - 输出操作提示
       
      |e|p|
      |:-:|:-:|
      |创建扩展分区|创建主分区|
  
  4. > Command (m for help): <kbd>w</kbd>

### 格式化磁盘
> mkfs.`文件系统类型` `磁盘名称`
>> 可以格式化大部分linux文件系统类型。
  ```python
  mkfs.xfs /dev/sdb1
  ```
### 挂载磁盘
> mount `磁盘名称` `文件目录`
  ```python
  mount /dev/sdc1 /home/tuotuo
  ```    
## 文件与目录管理
> **绝对路径**：由根目录`/`开始。<br>
> **相对路径**：由当前工作路径开始。
### 查看当前目录下的文件
> ls -l
- 输出以下内容
  ```python
  total 1 #目录下的文件个数
  drwxrwxrwx 1 tuo tuotuo 4096 Jan 15 00:00 tuotu0
  ```
<details> 
    <summary><b>drwxrwxrwx</b></summary>   
  
- 第一个字符为`d`表示该文件是一个文件夹（目录）
- 第一个字符为`-`表示该文件是一个文件
- 第一个字符为`l`表示该文件是一个链接文件
- 后面的字符每三个为一组，分别代表`文件所属用户的权限`、`文件所属用户组的权限`、`文件所属其他用户的权限`
- <code>r</code>可读、`w`可写、`x`可执行、`-`无      

</details>

|1|tuo|tuotuo|4096|Jan 15 00:00|tuotu0|
|:-:|:-:|:-:|:-:|:-:|:-:|
|number of hard links|文件所属用户的名称|文件所属组的名称|文件大小|文件最后修改时间|文件名称|

### 查看当前工作目录
```python
pwd
```
### 更改文件所属用户组  
> chgrp&nbsp;-R&nbsp;`新的所属用户组`&nbsp;`文件名`
  ```
  chgrp -R tuotuo tuotuo
  ```
### 更改所属用户
> chown&nbsp;`新的用户`&nbsp;`文件名`
  ```python
  chown tuotuo tuotu0
  ```
### 更改文件各用户及用户组权限
> chmod&nbsp;`权限`&nbsp;`文件名`
  ```pyhton
  chmod 770 tuotuo
  ```
### 切换工作目录
> cd&nbsp;`绝对路径或相对路径`
  ```python
  cd /home/tuotuo
  ```
### 创建目录
> mkdir&nbsp;`目录名`
  ```python
  mkdir tu0tu0
  ```
### 复制文件或目录
> cp&nbsp;`被复制的文件名或目录名`&nbsp;`复制到xx文件或目录`
  ```python
  cp /home/tuotuo /home/tu0tu0
  ```
### 删除文件或目录
> rm&nbsp;-f&nbsp;-r&nbsp;`文件或目录名`
  ```python
  rm -f -r xxx
  ```
### 移动文件或目录
> mv&nbsp;`被移动的文件名或目录名`&nbsp;`移动到xx目录`
  ```python
  mv /home/tuotuo /home/tuotu0
  ```
## 进程管理
### 打断当前任务
> <kbd>CTRL</kbd>+<kbd>C</kbd>
### 暂停当前任务放入后台
> <kbd>CTRL</kbd>+<kbd>Z</kbd>
### 查看后台任务
```
jobs -l
```
- 输出以下内容
  > `任务编号`、`PID`、`CMD`。
### 将暂停的后台任务移动到前台继续执行
> fg %`进程编号`
  ```
  fg %1
  ```
### 在创建任务时将命令放入后台执行
> `命令` &
  ```
  ping 1.1.1.1 &
  ```
  ```
  msfconsole &
  ```
### 结束进程
> kill `程序标识`
```python
kill 3784 #PID
```
```python
kill %1 #任务编号
```
```python
kill ftp #进程名称
```
