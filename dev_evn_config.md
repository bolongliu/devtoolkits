# 环境配置加速方法

1. 指定conda源进行安装cudatoolkit和cudnn及相关库

`
conda install cudatoolkit=10.1 cudnn=7.6.3 -c https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/linux-64/ -y
`

2. 指定pip源进行安装相关库
`
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple some-package
`
3.flash-attention安装方法

```shell
git clone https://github.com/Dao-AILab/flash-attention
cd flash-attention && pip install .
# 下方安装可选，安装可能比较缓慢。
# pip install csrc/layer_norm
# pip install csrc/rotary
```
注意这里会从出现错误提示flash-attention/csrc/cutlass找不到，git下载cutlass失败
所以cd flash-attention/csrc/ 然后 
```shell
git clone git@github.com:NVIDIA/cutlass.git
```
重新运行python setup.py install 就可以编译成功了

若还是报如下错误
```shell
running bdist_wheel
Guessing wheel URL:  https://github.com/Dao-AILab/flash-attention/releases/download/v2.3.3/flash_attn-2.3.3+cu117torch2.0cxx11abiFALSE-cp310-cp310-linux_x86_64.whl
error: Remote end closed connection without response
[end of output]

```
采用如下解决方法：
```shell
wget https://github.com/Dao-AILab/flash-attention/releases/download/v2.3.3/flash_attn-2.3.3+cu117torch2.0cxx11abiFALSE-cp310-cp310-linux_x86_64.whl
pip install flash_attn-2.3.3+cu117torch2.0cxx11abiFALSE-cp310-cp310-linux_x86_64.whl

# 此时终端应该会显示
Installing collected packages: ninja, flash-attn
Successfully installed flash-attn-2.3.3 ninja-1.11.1.1
```
