# 环境配置加速方法

1. 指定conda源进行安装cudatoolkit和cudnn及相关库

`
conda install cudatoolkit=10.1 cudnn=7.6.3 -c https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/linux-64/ -y
`

2. 指定pip源进行安装相关库
`
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple some-package
`
