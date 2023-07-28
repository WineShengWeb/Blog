# `Linux` 软件安装及环境配置

### `Linux` 系统设置网卡

####	1、切换到根目录
```cmd
cd /
```
####	2、进入到 `etc` 目录
```cmd
cd etc
```

####	3、进入到 `sysconfig` 目录
```cmd
cd sysconfig
```	
####	4、进入到 `network-scripts`
```cmd
cd network-scripts
```
	
####	5、编辑 `ifcfg-ens33` 文件
```cmd
vi ifcfg-ens33
```
	
####	6、按  `i`  键进入编辑状态
```cmd
i
```
	
####	7、按上下移动键移动到 `ONBOOT`
	
####	8、删除 `no` ，输入 `yes`
	
####	9、按 `ESC` 键， 输入 `:wq` ，按 `ENTER` 键保存退出

####	10、关机重启
```cmd
shutdown -h now
```

####	11、开机输入 `ip addr` 查看 `ip` 地址
```cmd
ip addr
```

---

### Linux 安装 `JDK` 环境：

####	1、下载 `Linux` 版本的 `JDK`
> 查看本机位数命令: sudo uname --m

> 显示: X86_64

#### 2、下载 `JDK`

- JDK官网下载地址：https://www.oracle.com/java/technologiesdownloads/#java18

- 选择 Linux 下 X64 Compressed Archive 对应的jdk-18_linux-x64_bin.tar.gz

#### 3、查看 `Linux` 是否有安装 `JDK`
```cmd
java -version
```

#### 4、如果有则下载安装的 `JDK`
> 4.1、查看命令
```cmd
rpm -qa | grep jdk
```
> 4.2、卸载命令
```cmd
eg: rpm -e --nodeps xxx（xxx代表删除的文件全名）
rpm -e --nodeps jdk-1.8.0.X86_64
```
	
#### 5、在 `/usr/local` 文件加下新建 `software` 文件夹，`software` 文件新建 `jdk` 文件夹
```cmd
mkdir /usr/local/software
mkdir /usr/local/software/jdk
```

#### 6、使用 `fialshell` 工具将下载好的 `JDK` 上传到 `/usr/localsoftware/jdk` 目录下
```cmd
cd /usr/local/software/jdk
```
将 `JDK` 拖到 `/usr/local/software/jdk` 目录下

#### 7、解压上传的 `JDK` 压缩包
```cmd
tar -zxvf tar -zxvf jdk-18_linux-x64_bin.tar.gz
```
等待解压安装完毕

#### 8、重命名 `JDK` 文件名为 `jdk1.8`
```cmd
mv jdk-18.0.2.1/ jdk1.8
```

#### 9、设置环境变量
```cmd
vi /etc/profile
```
输入上面的命令后，`shift + g` 快速将光标定位到最后一行，然后按 `i` 键，输入下面代码
```cmd
# set java environment
JAVA_HOME=/usr/local/software/jdk/jdk1.8
CLASSPATH=$JAVA_HOME/lib
PATH=$PATH:$JAVA_HOME/bin
export PHTH JAVA_HOME CLASSPATH
```
填写完代码后按 `ESC` 键，输入 `:wq` 保存并退出编辑页面

#### 10、重载 `profile` 文件，让设置的命令生效
```cmd
source /etc/profile
```

#### 11、验证 `JDK` 是否安装成功
```cmd
java -version
```
出现 `java` 版本号则表示已安装成功

---
	
### `Linux` 安装 `MySQL` 环境：

#### 1、下载 `mysql` 安装包

- `mysql` 下载地址：`https://downloads.mysql.com/archives/community/`
- 选择版本为：`5.7.20`
- 选择系统为：`Linux - Generic`
- 选择 `Linux - Generic (glibc 2.12) (x86, 64-bit), CompressedTAR Archive` 点击 `download` 按钮下载
	
#### 2、在 `/usr/local/software` 目录下新建 `mysql` 文件夹
```cmd
cd /usr/local/software
mkdir mysql
```
使用 `fialshell` 工具上传到 `mysql` 目录下 
	
#### 3、解压 mysql 文件
```cmd
tar -zxvf mysql-5.7.20-linux-glibc2.12-x86_64.tar.gz
```

#### 4、创建 `data` 和 `logs` 目录
```cmd
mkdir data
mkdir logs
```

#### 5、修改 `etc/my.cnf` 文件，如果没有则创建
```cmd
cd /etc
vi my.cnf
```

按 i 键进入编辑状态，按以下内容进行修改编辑	
```cmd
[mysql]
# 设置 mysql 客户端默认字符集
default-character-set=utf8
socket=/var/lib/mysql/mysql.sock
[mysqld]
skip-name-resolve
# 设置 3306 端口
port = 3306
socket=/var/lib/mysql/mysql.sock
# 设置 mysql 数据库的数据的存放目录
datadir=/usr/local/software/mysql/data
# 设置 mysql 的安装目录
basedir=/usr/local/software/mysql
# 设置允许最大连接数
max_connections=200
# 服务端使用的字符集默认为 8 比特编码的 latin1 字符集
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
lower_case_table_names=1
max_allowed_packet=16M
[mysqld_safe]
log-error=/usr/local/software/mysql/logs/mysqld.log
pid-file=/usr/local/software/mysql/data/mysqld.pid


# Disabling symbolic-links is recommended to prevent assorted security risks
symbolic-links=0
# Settings user and group are ignored when systemd is used.
# If you need to run mysqld under a different user or group,
# customize your systemd unit file for mariadb according to the
# instructions in http://fedoraproject.org/wiki/Systemd
-- INSERT --
```	

修改完成按 `ESC` 键， 输入 `:wq` , 按 `ENTER` 键保存退出
	
####	6、初始化  `mysql`
```cmd
./bin/mysqld --initialize --user=root --basedir=/usr/local/software/mysql/ --datadir=/usr/local/software/mysql/data/ 
```

##### 未完待续...


