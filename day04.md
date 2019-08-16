# day04

### 压缩和解压

- zip/unzip,文件后缀.zip

```shell
touch 1.txt 2.txt 3.txt  #创建文件
zip 1.zip 1.txt #把1.txt 压缩成1.zip
unzip 1.zip #把1.zip解压
zip 123.zip *.txt

#压缩所有的文件
```

- gzip/gunzip,文件后缀.gz,只能压缩单个文件，不能是多个或者是目录

  

```shell
gzip 1.txt#压缩1.txt为  1.txt.gz, 源文件会消失
gzip -c 1.txt > 1.txt.gz#功能同上，但是源文件会保留
gunzip 1.txt.gz#解压文件，源文件会消失
gunzip -c 1.txt.gz > 1.txt #功能同上，源文件会保留



gzip -d 1.txt.gz#也可以进行解压
```

- bzip2/bunzip2,文件是后缀bz2，也只能是压缩单个文件，不能是多个或者是目录

  

```shell
bzip2 3.txt #压缩3.txt  但是源文件会消失
bunzip2 3.txt.bz2#解压3.txt.bz2文件，源文件会消失
bzip2 -c 3.txt > 3.txt.bz2#压缩3.txt文件，源文件会保留
bunzip2 -c 3.txt.bz2 > 3.txt#解压文件，源文件会保留


```

- tar,用于打包和解包，后缀为.tar

  

| 选项      | 说明                            |
| --------- | ------------------------------- |
| -c        | 创建新的包                      |
| -x        | 解包                            |
| -t        | 检查包（不解包）                |
| -f        | 指定操作文件                    |
| -v        | 显示相关信息                    |
| -z        | 调用gzip/gunzip进行压缩或者解压 |
| -j        | 调用bzip2/bunzip进行压缩或解压  |
| -C        | 指定解压的位置                  |
| --exclude | 排除指定的文件                  |

基本使用：

```
tar -cvf 123.tar *.txt     #将所有的txt文件打包成123.tar文件
tar -tf 123.tar            #查看包中的文件
tar -xvf 123.tar  			#解包
tar -zcvf 123.tar.gz *.txt --exclude 3.txt  #打包并压缩，除3.txt以外的文件
tar -zxvf 123.tar.gz

```





### 网络服务

- ping：检查网路的连通性， -c 可以指定发生测试数据包的数量

  - 如:ping www.baidu.com -c 5

    

  

- ifconfig :查看或者设置网卡信息的
  
  - if config 网卡名称 up|down:开启或者关闭指定的网卡

### 资源监测

- free:查看内存使用的情况
  - free -h:人性化显示内存的使用后情况
  - swap:交换分区
- df：查看磁盘的使用情况
- netstat：查看网络端口的使用情况
- w：正在做的事情
- top：是w的详细信息

### 进程管理

- ps:查看进程状态的信息

  选项

  | 选项 | 说明                          |
  | ---- | ----------------------------- |
  | -e   | 显示所有的进程                |
  | -f   | 显示完整的格式                |
  | a    | 显示所有的进程                |
  | u    | 以用户为主进行显示            |
  | x    | 结合a一起使用，显示完整的信息 |

  ps -ef | grep  nginx:查看nginx的进程（重点）

  kill：用来结束进程的

  ​	sudo kill 进程的pid

  ​	sudo kill -9 进程的pid ：强制杀掉这个进程

  出现什么情况才杀死进程：当你启动软件的时候，报错了，端口被占用的情况

  

### 软件安装

- 方式1：专门的命令进行安装，无需考虑软件包的依赖关系的

  - debain系列：apt-get（ubuntu）

  - redhat系列：yum（centos）

  - 常用的操作

    | 操作    | 说明                 |
    | ------- | -------------------- |
    | install | 安装软件包           |
    | remove  | 移除软件包           |
    | update  | 更新软件包的列表信息 |
    | upgrade | 进行一次系统的更新   |

  - 示例：sudo apt-get install openssh-server

    使用：sudo service  sshd  start|stop|restart

- 更改为阿里源的操作

  https://opsx.alibaba.com/mirror

  阿里云镜像

  ```ini
  deb http://mirrors.aliyun.com/ubuntu/ xenial main
  deb-src http://mirrors.aliyun.com/ubuntu/ xenial main
  
  deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main
  deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main
  
  deb http://mirrors.aliyun.com/ubuntu/ xenial universe
  deb-src http://mirrors.aliyun.com/ubuntu/ xenial universe
  deb http://mirrors.aliyun.com/ubuntu/ xenial-updates universe
  deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates universe
  
  deb http://mirrors.aliyun.com/ubuntu/ xenial-security main
  deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main
  deb http://mirrors.aliyun.com/ubuntu/ xenial-security universe
  deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security universe
  
  ```

  - 备份文件：sudo mv /etc/apt/sources.list  /etc/apt/sources.list.bak
  - 新建软件：sudo vim /etc/apt/sources.list      
  - 更新软件包的列表信息：sudo apt-get update

- 方式2:使用特定的安装包的命令来进行安装，考虑包的依赖

  

  

  - debain:dpkg的命令，要安装的软件必须是后缀为.deb

  - redhat:rpm的命令，软件后缀是.rpm

  - 常用选项

    | 命令 | 说明               |
    | ---- | ------------------ |
    | -i   | 安装               |
    | -r   | 卸载               |
    | -l   | 查看软件的信息     |
    | -L   | 查看软件的安装目录 |

    sudo dpkg -i wps-office_10.1.0.5672~a21_amd64.deb 

    sudo unzip wps_symbol_fonts.zip -d /usr/share/fonts/

    dpkg: 无法恢复的致命错误，中止：
     fork 失败: 无法分配内存

    

- 方式3(最难的)：源码安装，需要对源码进行编译进行安装

  - 安装步骤

    - #### 配置:configure

      ./configure --prefix=/usr/local/nginx/

    - 编译：make

    - 安装：make install

      ```
      tar -zxvf nginx-1.13.7.tar.gz #解压
      cd nginx-1.13.7/#解压之后会有一个详细的文件夹，进入到文件夹
      ./configure --prefix=/usr/local/nginx/#配置到这个地方
      make#编译
      sudo make install #安装
      cd  /usr/local/nginx/sbin/
      sudo ./nginx     #启动nginx
      
      
      #如果端口被占用，
      ps -ef | grep nginx
      sudo kill -9 pid
      
      
      ```

      

  示例：安装nginx