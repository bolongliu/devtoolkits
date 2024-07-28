# 环境配置加速方法

## 0. conda镜像,pypi镜像,Docker镜像配置
### conda

**HIT镜像**
```shell
vim .condarc
# 写入如下内容：

channels:
  - defaults
  - conda-forge
show_channel_urls: true
default_channels:
  - https://mirrors.hit.edu.cn/anaconda/pkgs/main
  - https://mirrors.hit.edu.cn/anaconda/pkgs/r
  - https://mirrors.hit.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.hit.edu.cn/anaconda/cloud
  msys2: https://mirrors.hit.edu.cn/anaconda/cloud
  bioconda: https://mirrors.hit.edu.cn/anaconda/cloud
  menpo: https://mirrors.hit.edu.cn/anaconda/cloud
  pytorch: https://mirrors.hit.edu.cn/anaconda/cloud
  pytorch-lts: https://mirrors.hit.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.hit.edu.cn/anaconda/cloud
```

**USTC镜像**

```shell
channels:
  - https://mirrors.ustc.edu.cn/anaconda/pkgs/main/
  - https://mirrors.ustc.edu.cn/anaconda/pkgs/free/
  - https://mirrors.ustc.edu.cn/anaconda/cloud/conda-forge/
ssl_verify: true
```

### pypi
```shell
python -m pip install --upgrade pip
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

```shell
vim .config/pip/pip.conf 或者vim .pip/pip.conf
# 写入如下内容：

[global]
index-url = https://mirrors.hit.edu.cn/pypi/web/simple
# index-url = https://pypi.tuna.tsinghua.edu.cn/simple
# index-url = https://pypi.mirrors.ustc.edu.cn/simple
# index-url = https://pypi.douban.com/simple

```
**配置多个镜像源平衡负载**

可在已经替换 index-url 的情况下通过以下方式继续增加源站：
```shell
pip config set global.extra-index-url "<url1> <url2>..."
```
**例子**
```shell
pip config set global.extra-index-url "https://mirrors.hit.edu.cn/pypi/web/simple https://pypi.mirrors.ustc.edu.cn/simple  https://pypi.tuna.tsinghua.edu.cn/simple"
```
可用的 pypi 源列表（校园网联合镜像站）：https://mirrors.cernet.edu.cn/list/pypi

**换回默认源**
```shell
pip config unset global.index-url
```

### docker
```shell
# 修改 /etc/docker/daemon.json 文件，执行命令：
vim /etc/docker/daemon.json
# 修改为如下形式：
{
 "registry-mirrors": ["https://docker.mirrors.ustc.edu.cn"]
}

# 多个软件源使用
{
 "registry-mirrors": ["http://hub-mirror.c.163.com",
                      "https://registry.docker-cn.com",
                      "https://docker.mirrors.ustc.edu.cn",
                      "https://kfwkfulq.mirror.aliyuncs.com"
                      ]
}

# 重启Docker,以使docker的配置文件生效
sudo systemctl daemon-reload
sudo systemctl restart docker
docker info
# 显示如下表示配置成功
 Insecure Registries:
  127.0.0.0/8
 Registry Mirrors:
  https://ustc-edu-cn.mirror.aliyuncs.com/
 Live Restore Enabled: false
```
**配置Docker加速器完成。**

## 1. 深度学习环境配置
### 1. 若只使用Pytorch，则无需安装完整版本cudatoolkit cudnn，尤其是不需要进行相关【包编译安装】时选择该方法。
`
conda pytorch torchvision cudatoolkit=10.0 -c pytorch
`
### 2. 【需要编译】，通过conda安装的cudatoolkit cudnn是阉割版，因此需要编译的需要安装完整版本的cudatoolkit cudnn

【官网下载，手动安装】
https://developer.nvidia.com/cuda-toolkit-archive
https://developer.nvidia.com/cudnn-archive

选择合适的版本：
```
wget https://developer.download.nvidia.com/compute/cuda/11.2.0/local_installers/cuda_11.2.0_460.27.04_linux.run
sudo sh cuda_11.2.0_460.27.04_linux.run
```

nvidia conda 通道现已可用：nvidia/cuda 和 nvcc 已在其中：
`
conda install cuda -c nvidia

conda install pytorch torchvision cudatoolkit=10.2 -c pytorch -c hcc

`



## 1. 指定conda源进行安装cudatoolkit和cudnn及相关库

`
conda install cudatoolkit=10.1 cudnn=7.6.3 -c https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/linux-64/ -y
`

**[注]**

- 使用 conda install 安装的 cudatoolkit 与NVIDIA打包的CUDA工具包不一样。它是一个子集，为 conda 安装的其他软件包（例如 pytorch ）提供所需的组件。如果您只需要使用 pytorch，那么这可能就是您所需要的。随 pytorch 安装的 cudatoolkit 仅是运行时，不附带开发编译器 nvcc 。要获得 nvcc ，您需要安装 cudatoolkit-dev
- 不写版本会自动选版本与cuda版本相匹配：
conda install cudnn

## 2. 指定pip源进行安装相关库
`
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple some-package
`
## 3.flash-attention安装方法

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

## 4. huggingface国内加速下载方法
(1) 安装依赖
```shell
pip install -U huggingface_hub hf_transfer
```

(2) 将huggingface仓库下载在本地指定目录基本命令示例：
```shell
export HF_ENDPOINT=https://hf-mirror.com
huggingface-cli download --resume-download repo_id --local-dir local_dir
# 举例
huggingface-cli download --resume-download bigscience/bloom-560m --local-dir bloom-560m
huggingface-cli download --resume-download THUDM/chatglm3-6b --local-dir chatglm3-6b
huggingface-cli download --resume-download shibing624/text2vec-base-chinese --local-dir text2vec-base-chinese
```
(3)直接替换镜像地址后使用from_pretrained下载模型
```shell
pip install protobuf transformers==4.30.2 cpm_kernels torch>=2.0 gradio mdtex2html sentencepiece accelerate

export HF_ENDPOINT=https://hf-mirror.com

from transformers import AutoTokenizer, AutoModel
tokenizer = AutoTokenizer.from_pretrained("THUDM/chatglm3-6b", trust_remote_code=True)
model = AutoModel.from_pretrained("THUDM/chatglm3-6b", trust_remote_code=True).half().cuda()
model = model.eval()
response, history = model.chat(tokenizer, "你好", history=[])
print(response)
```

## 5. 原始jupyter notebook安装，不要jupyter lab
```shell
conda install -c conda-forge notebook
conda install -c conda-forge jupyter_contrib_nbextensions
jupyter contrib nbextension install --user
```
Then, jupyter contrib nbextension install --user executes without error.
Now you can enable jupyter extensions (e.g. black) like this:
```shell
jupyter nbextensions_configurator enable --user
```

