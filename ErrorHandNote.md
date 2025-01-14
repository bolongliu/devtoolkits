# 常见报错处理笔记

## 深度学习环境配置报错处理
1. OSError: CUDA_HOME environment variable is not set. Please set it to your CUDA install root.

- 使用conda环境解决方法

```shell
conda install -c nvidia cuda -y
conda install -c nvidia cuda-compiler -y

which nvcc
# /home/liubl/miniconda3/envs/env_name/bin/nvcc
export CUDA_HOME=/home/liubl/miniconda3/envs/env_name/bin/nvcc
```
- 使用apt直接安装nvidia-cuda-toolkit,因为conda安装的nvidia-cuda-toolkit不是完全的版本。
pytorch安装的cuda toolkit是不带nvcc编译器的
```shell
sudo apt install nvidia-cuda-toolkit -y
which nvcc
export CUDA_HOME=/usr/local/cuda
```
注：
在大多数情况下，基于Pytorch安装的cudatoolkit 是可以满足 Pytorch 等框架的使用需求的。但对于一些特殊需求，如需要为 Pytorch 框架添加 CUDA 相关的拓展时( Custom C++ and CUDA Extensions )，需要对编写的 CUDA 相关的程序进行编译等操作，则需安装完整的 Nvidia 官方提供的 CUDA Toolkit.

## 软件安装deb包时报错处理
1.出现某些包没有安装，使用如下命令处理和安装
```shell
sudo dpkg -i xxx
# 报错某些package没有安装,使用如下命令安装即可。
sudo apt --fix-broken install
或者
sudo apt install --fix-missing
```

例如:安装网易邮箱大师.
```shell
(base) ➜  Downloads sudo dpkg -i mail.deb             
Selecting previously unselected package mailmaster.
(Reading database ... 528345 files and directories currently installed.)
Preparing to unpack mail.deb ...
Unpacking mailmaster (5.0.2.1009) ...
dpkg: dependency problems prevent configuration of mailmaster:
 mailmaster depends on libnss-wrapper; however:
  Package libnss-wrapper is not installed.
 mailmaster depends on libgconf-2-4; however:
  Package libgconf-2-4 is not installed.

dpkg: error processing package mailmaster (--install):
 dependency problems - leaving unconfigured
Processing triggers for gnome-menus (3.36.0-1ubuntu1) ...
Processing triggers for desktop-file-utils (0.24-1ubuntu3) ...
Processing triggers for mime-support (3.64ubuntu1) ...
Errors were encountered while processing:
```
```shell

(base) ➜  Downloads sudo apt --fix-broken install
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Correcting dependencies... Done
The following packages were automatically installed and are no longer required:
  gir1.2-goa-1.0 libfwupdplugin1 libllvm11 libxmlb1
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  gconf-service gconf-service-backend gconf2-common libgconf-2-4
  libnss-wrapper
The following NEW packages will be installed:
  gconf-service gconf-service-backend gconf2-common libgconf-2-4
  libnss-wrapper
0 upgraded, 5 newly installed, 0 to remove and 22 not upgraded.
1 not fully installed or removed.
Need to get 885 kB of archives.
After this operation, 8,181 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://mirrors.hit.edu.cn/ubuntu focal/universe amd64 libnss-wrapper amd64 1.1.3-1 [26.0 kB]
Get:2 http://mirrors.hit.edu.cn/ubuntu focal/universe amd64 gconf2-common all 3.2.6-6ubuntu1 [698 kB]
Get:3 http://mirrors.hit.edu.cn/ubuntu focal/universe amd64 libgconf-2-4 amd64 3.2.6-6ubuntu1 [84.8 kB]
Get:4 http://mirrors.hit.edu.cn/ubuntu focal/universe amd64 gconf-service-backend amd64 3.2.6-6ubuntu1 [58.6 kB]
Get:5 http://mirrors.hit.edu.cn/ubuntu focal/universe amd64 gconf-service amd64 3.2.6-6ubuntu1 [17.4 kB]
Fetched 885 kB in 0s (3,497 kB/s)        
Selecting previously unselected package libnss-wrapper.
(Reading database ... 528624 files and directories currently installed.)
Preparing to unpack .../libnss-wrapper_1.1.3-1_amd64.deb ...
Unpacking libnss-wrapper (1.1.3-1) ...
Selecting previously unselected package gconf2-common.
Preparing to unpack .../gconf2-common_3.2.6-6ubuntu1_all.deb ...
Unpacking gconf2-common (3.2.6-6ubuntu1) ...
Selecting previously unselected package libgconf-2-4:amd64.
Preparing to unpack .../libgconf-2-4_3.2.6-6ubuntu1_amd64.deb ...
Unpacking libgconf-2-4:amd64 (3.2.6-6ubuntu1) ...
Selecting previously unselected package gconf-service-backend.
Preparing to unpack .../gconf-service-backend_3.2.6-6ubuntu1_amd64.deb ...
Unpacking gconf-service-backend (3.2.6-6ubuntu1) ...
Selecting previously unselected package gconf-service.
Preparing to unpack .../gconf-service_3.2.6-6ubuntu1_amd64.deb ...
Unpacking gconf-service (3.2.6-6ubuntu1) ...
Setting up gconf2-common (3.2.6-6ubuntu1) ...

Creating config file /etc/gconf/2/path with new version
Setting up libnss-wrapper (1.1.3-1) ...
Setting up gconf-service (3.2.6-6ubuntu1) ...
Processing triggers for libc-bin (2.31-0ubuntu9.9) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for sgml-base (1.29.1) ...
Setting up libgconf-2-4:amd64 (3.2.6-6ubuntu1) ...
Setting up gconf-service-backend (3.2.6-6ubuntu1) ...
Setting up mailmaster (5.0.2.1009) ...
Processing triggers for libc-bin (2.31-0ubuntu9.9) ...
(base) ➜  Downloads sudo dpkg -i mail.deb         
(Reading database ... 528787 files and directories currently installed.)
Preparing to unpack mail.deb ...
Unpacking mailmaster (5.0.2.1009) over (5.0.2.1009) ...
Setting up mailmaster (5.0.2.1009) ...
Processing triggers for gnome-menus (3.36.0-1ubuntu1) ...
Processing triggers for desktop-file-utils (0.24-1ubuntu3) ...
Processing triggers for mime-support (3.64ubuntu1) ...
(base) ➜  Downloads 
```
### 安装的jupyterlab 死活无法打开，打开都是jupyter notebook的解决方法。
```bash
卸载jupyter notebook
pip uninstall -y notebook jupyter-console jupyter-client jupyter-packaging nbconvert nbformat

清理并重建 Jupyter 配置（如果有必要）
有时，Jupyter 可能仍然会加载旧的配置或扩展，导致问题。你可以尝试清理配置并重建它：
jupyter nbextension disable --all
jupyter serverextension disable --all
jupyter lab clean

安装jupyterlab
pip install jupyterlab
(RP2bp) ➜  RPS-Code jupyter lab --version
4.3.4

jupyter --version

Selected Jupyter core packages...
IPython          : 8.24.0
ipykernel        : 6.29.3
ipywidgets       : 8.1.3
jupyter_client   : 7.4.9
jupyter_core     : 5.7.2
jupyter_server   : 2.14.2
jupyterlab       : 4.3.4
nbclient         : 0.10.2
nbconvert        : 7.16.4
nbformat         : 5.10.4
notebook         : 7.3.1
qtconsole        : not installed
traitlets        : 5.14.3

确保 Jupyter Lab 启动为默认应用，如果你之前尝试过 Jupyter Notebook 并且它仍然是默认启动程序，可以执行以下命令来确认启动时是启动 Jupyter Lab：
jupyter serverextension enable --py jupyterlab
# 重要的是这句，将notebook直接升级到最新版本。
pip install --upgrade notebook
pip install --upgrade jupyterlab
```


## ubuntu@192.168.1.108: Permission denied (publickey).

其主要原因是在`/etc/ssh/sshd_config`中配置了`PermitRootLogin prohibit-password`
【解决方法】
```shell
sudo vim /etc/ssh/sshd_config

PasswordAuthentication no
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
PermitRootLogin no
```
PermitRootLogin prohibit-password 表示允许 root 账户登录，但是不能以密码的方式登录，所以只能以公私钥的方式登录，为了简便，我们不采用这种方式，而是采用 PermitRootLogin yes，这样，直接使用密码就可以登录了。
