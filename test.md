## 卸载：
#### 打开Powershell

`wslconfig /l`  #显示出你安装的列表

`wslconfig /u debian` #debian为上述列表中的名字

#### 点进开始菜单，右键卸载

---
## 切换 root 用户
`sudo -i`
## 退出 root 用户
`su lyy_fdu`

---
## 换源
#### 打开列表
`sudo vim sources.list`

#### 替换为

`#阿里云

deb http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse

deb-src http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse

deb-src http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse

deb-src http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse

deb-src http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse

deb-src http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse

#中科大

deb https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse

deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse

deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse

deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse

deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse

deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse

deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse

deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse

deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse

deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse

#清华

deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse

deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse

deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse

deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse

deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse

deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse

deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse

deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse

deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse

deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse`

#### 保存并退出

`Esc`
`:wq`

#### 更新

`sudo apt-get update`
`sudo apt-get upgrade`

---
## 更换安装路径：
[reference](https://blog.csdn.net/qq_41233171/article/details/106268552)
#### 打开PowerShell查看版本
`LxRunOffline list` 
#### 更换路径，如：`LxRunOffline move -n Ubuntu-20.04 -d D:\WinLinux`
`LxRunOffline move -n {version} -d {dir}`

---
## 修改SSH以便git clone(注意最后一步)
[reference](https://blog.cofface.com/archives/2971.html)
#### 安装一些必要的环境和依赖
`sudo apt-get install build-essential fakeroot dpkg-dev`
#### 创建一个名为git-rectify的路径
`mkdir ~/git-rectify`
#### 进入路径，获取git的源文件
`cd ~/git-rectify`

`apt-get source git`
#### 安装依赖
`sudo apt-get build-dep git`
#### 安装libcurl的依赖文件
`sudo apt-get install libcurl4-openssl-dev`
#### 进入目录
`cd git-2.25.1/`
#### 修改文件内容，需要修改两个文件
`gedit ./debian/control # 把libcurl4-gnutls-dev 修改为 libcurl4-openssl-dev`

`gedit ./debian/rules # 把TEST =test整行删除`

需先安装 `sudo apt-get install gedit`
#### 编译和构建安装包
`sudo dpkg-buildpackage -rfakeroot -b`
#### 退回上一级目录，安装编译好的安装包
`cd ..`

`sudo dpkg -i git_2.25.1-1ubuntu3_amd64.deb`
#### WSL自带的SSH有点的问题，要remove并重新install，然后修改配置文件中的端口并重启ssh服务
`sudo apt autoremove --purge openssh-server -y && sudo apt install openssh-server -y`

`sudo service ssh --full-restart`

