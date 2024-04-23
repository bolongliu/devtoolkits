# colab base config

## 1. base env config
```bash
# 环境配置
!conda install --yes -c pytorch pytorch=1.7.1 torchvision cudatoolkit=11.0
!pip install ftfy regex tqdm
!pip install git+https://github.com/openai/CLIP.git
# 切换目录并安装
!git clone https://github.com/SunzeY/AlphaCLIP.git
# [注] %cd 表示永久进入某个目录， !cd 只在当前行有用，还是会推出目录
%cd /content/AlphaCLIP
!pip install -e .
```
## 2. tools config
```bash
# 安装下载谷歌网盘工具gdown
!pip install gdown
```


## Usage demo
### gdwon usage demo
```python
import gdown
# a file
url = "https://drive.usercontent.google.com/download?id=1WykuBYWePriCVeW5lOwBsgxgeBMzb1nd"
output = "./checkpoints/clip_l14_grit20m_fultune_2xe.pth"
gdown.download(url, output)
```


