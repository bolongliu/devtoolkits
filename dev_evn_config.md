# 环境配置加速方法

## 1. 指定conda源进行安装cudatoolkit和cudnn及相关库

`
conda install cudatoolkit=10.1 cudnn=7.6.3 -c https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/linux-64/ -y
`

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
