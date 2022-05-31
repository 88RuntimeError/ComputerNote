# 一、Linux网络配置

## 1.CentOS 7 NAT模式

### 1.1 确保虚拟机设置中，网络适配器使用NAT 模式

![image-20220505205105619](Linux配置.assets/image-20220505205105619.png)



### 1.2 设置虚拟机的虚拟网络编辑器

- 打开网络编辑器

![image-20220505205612305](Linux配置.assets/image-20220505205612305.png)

- 点击更改设置

  ![image-20220505210344253](Linux配置.assets/image-20220505210344253.png)

- 切换到VMnet8，配置子网ip和网关ip

  ![无标题](Linux配置.assets/无标题.png)

  

### 1.3 打开CentOS，输入root和密码

- 找到  ifcfg-en*** 文件（文件名不一定，但都是以  ifcfg-en  开头的，具体的可以通过  ll  查看）

  - `vi /etc/sysconfig/network-scripts/ifcfg-eno16777736`

    ![image-20220520163457749](Linux配置.assets/image-20220520163457749.png)

  - 配置ens33文件内容

    - BOOTPROTO=dhcp改为BOOTPROTO=static
    - ONBOOT=no改为ONBOOT=yes
    - 添加：IPADDR=192.168.188.100
    - 添加：NETMASK=255.255.255.0
    - 添加：GATEWAY=192.168.188.2
    - 添加：DNS1=114.114.114.114

  - ifcfg-en文件初始状态

    ![image-20220520163325361](Linux配置.assets/image-20220520163325361.png)

  - 修改后的状态

    ![image-20220520164111212](Linux配置.assets/image-20220520164111212.png)



### 1.4 重新启动网络设置

- 输入 `systemctl restart network.service` 重新启动网络设置
- 输入 `ping www.baidu.com` 检查网络是否配置成功
- 输入 `ip addr` 检查当前网络配置数据

![image-20220520165527269](Linux配置.assets/image-20220520165527269.png)



### 1.5 关闭防火墙

- 本次开机状态下，关闭防火墙（下次开机防火墙又会开启）

  `systemctl stop firewalld`

- 重启后，一直关闭防火墙（本次开机状态不关闭，重启后一直关闭）

  `systemctl disable firewalld`

### 1.6 连接 xshell和xftp

破解版下载地址1：http://xshell.cephp.cn/

破解版下载地址2：http://pan.cephp.cn/index.php/s/bHGGDG59nkEA3Zm

- 打开虚拟机

  ![image-20220520173002794](Linux配置.assets/image-20220520173002794.png)



### xshell

- 打开xshell，用户身份验证

  - 输入 ssh 192.168.188.100

    ![image-20220520173214820](Linux配置.assets/image-20220520173214820.png)

    ![image-20220520173244219](Linux配置.assets/image-20220520173244219.png)

    ![image-20220520173312479](Linux配置.assets/image-20220520173312479.png)

    ![image-20220520173339859](Linux配置.assets/image-20220520173339859.png)

    

    

  - 成功连接xshell

    ![image-20220520173402716](Linux配置.assets/image-20220520173402716.png)



### xftp

- 打开xshell，点击“新建文件传输”

  ![image-20220520173734395](Linux配置.assets/image-20220520173734395.png)

- 就完成了xftp的连接

  ![image-20220520173803304](Linux配置.assets/image-20220520173803304.png)

## 2. CentOS 7 桥接模式





## 3. Ubuntu



# 二、Linux软件安装与配置

## 1. 配置Yum源

### 配置CentOS7的yum源

- 查看系统默认Yum源

  ```
  yum repolist
  ```

- 查看Yum配置文件

  ```
  cd /etc/yum.repos.d/
  ls
  vi CentOS-Base.repo
  ```

- 备份原文件

  ```
  mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
  ```

- 配置阿里云的Yum源文件

  ```
  curl -o /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-7.repo
  ```

- 生成缓存

  ```
  yum makecache
  ```

### 添加epel Yum源

- 安装wget

  ```
  yum install wget
  ```

- 添加epel Yum源

  ```
  wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo
  ```

- 生成缓存

  ```
  yum makecache
  ```





## 2. 安装python3.8

- 按python关键字查询

  ```
  yum search python
  ```

  找到python解释器

  `python3.x86_64 : Interpreter of the Python programming language`

- 查看python安装包的详细信息

  ```
  yum info python3.x86_64
  ```

  > Name        : python3
  > Arch        : x86_64
  > Version     : 3.6.8
  > Release     : 18.el7
  > Size        : 70 k
  > Repo        : updates/7/x86_64
  > Summary     : Interpreter of the Python programming language
  > URL         : https://www.python.org/
  > License     : Python
  > Description : Python is an accessible, high-level, dynamically typed, interpreted programming
  >          : language, designed with an emphasis on code readability.
  >          : It includes an extensive standard library, and has a vast ecosystem of
  >          : third-party libraries.
  >          : 
  >          : The python3 package provides the "python3" executable: the reference
  >          : interpreter for the Python language, version 3.
  >          : The majority of its standard library is provided in the python3-libs package,
  >          : which should be installed automatically along with python3.
  >          : The remaining parts of the Python standard library are broken out into the
  >          : python3-tkinter and python3-test packages, which may need to be installed
  >          : separately.
  >          : 
  >          : Documentation for Python is provided in the python3-docs package.
  >          : 
  >          : Packages containing additional libraries for Python are generally named with
  >          : the "python3-" prefix.

- 去python官网寻找3.8.7版本的python下载链接