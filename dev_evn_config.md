# 统一ML-Workspace
All-in-one web-based IDE specialized for machine learning and data science.
https://github.com/ml-tooling/ml-workspace
Features
Jupyter • Desktop GUI • VS Code • JupyterLab • Git Integration • File Sharing • Access Ports • Tensorboard • Extensibility • Hardware Monitoring • SSH Access • Remote Development • Job Execution
![image](https://github.com/user-attachments/assets/46cb7f14-8396-42db-bec4-1ed90379563d)
![image](https://github.com/user-attachments/assets/1acaeba4-a51e-4360-af98-2144c41f6efb)



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


## 6. 本地浏览器打开远程服务器上的Jupyter Notebook
```bash
# 远程服务器配置：
jupyter notebook --generate -config
jupyter notebook password # 按提示，输入密码

vim ~/.jupyter/jupyter_notebook_config.py 
添加
c.NotebookApp.open_browser = False
c.NotebookApp.port = 8888 #随便指定一个端口

jupyter notebook --no-browser --port=8889
# 本地服务器访问远程服务器
ssh -N -f -L localhost:8882:localhost:8889 a100
# ssh -N -f -L localhost:8889:localhost:8848 a100
# 其中： -N 告诉SSH没有命令要被远程执行； -f 告诉SSH在后台执行； -L 是指定port forwarding的配置，远端端口是8848，本地的端口号的8888。remote_user@remote_host 用实际的远程帐户和远程地址替换
# 然后打开浏览器，输入地址：http://localhost:8888/，再输入密码，即可登陆

```

## 7.conda常用操作
```shell
# 复制指定环境并重命名
conda create --name RP1bp --clone RP1
```
## 8.jupyterlab好用插件
参考连接：https://github.com/mauhai/awesome-jupyterlab
```text
jupyterlab-kite #免费的 AI 赋能代码补全服务 Kite
jupyterlab-variableInspector 该插件可以在Lab中展示代码中的变量及其属性，类似RStudio中的变量检查器。你可以一边撸代码，一边看有哪些变量。
gather 在Lab中清理代码，恢复丢失的代码以及比较代码版本的工具。
go to Definition 该插件用于在Lab笔记本和文件编辑器中跳转到变量或函数的定义。https://github.com/krassowski/jupyterlab-go-to-definition
lsp 该插件用于自动补全、参数建议、函数文档查询、跳转定义等。https://github.com/krassowski/jupyterlab-lsp
jupyter-matplotlib帮助我们在notebook界面配合matplotlib实现交互式的作图，只需要在绘图之前执行魔法命令%matplotlib widget，之后绘制的所有matplotlib图表即可自动转换为交互式的：
jupyterlab-system-monitor  #在 Jupyter Lab UI 的顶部栏显示 CPU 和内存使用情况
jupyterlab-spreadshee # 在 Jupyter Lab 中嵌入了 xls/xlsx 电子表格查看功能
1. JupyterLab-TOC #notebook 有一个目录
2.  jupyterlab-drawio # 绘制图表的工具
jupyterlab-latex 支持在线编辑并预览LaTeX文档。
```
```shell
pip install ipympl
jupyter labextension install @jupyter-widgets/jupyterlab-manager jupyter-matplotlib
jupyter labextension install jupyterlab-drawio
jupyter labextension install jupyterlab-execute-time
jupyter labextension install jupyterlab-spreadsheet
pip install nbresuse
jupyter labextension install jupyterlab-topbar-extension jupyterlab-system-monitor

pip install jupyter-kite
jupyter labextension install @kiteco/jupyterlab-kite

jupyter labextension install @lckr/jupyterlab_variableinspector
pip install aquirdturtle_collapsible_headings



pip install jupyterlab-code-formatter
pip install black isort
pip install jupyterlab_tensorboard
# theme 
jupyter labextension install @telamonian/theme-darcula
jupyter labextension install @rahlir/theme-gruvbox
jupyter labextension install @oriolmirosa/jupyterlab_materialdarker
```
