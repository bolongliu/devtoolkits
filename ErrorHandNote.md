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
