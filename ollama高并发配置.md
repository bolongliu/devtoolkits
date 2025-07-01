# ollama高并发配置

```shell
sudo vim /etc/systemd/system/ollama.service
添加====之间的配置
[Unit]
Description=Ollama Service
After=network-online.target

[Service]
ExecStart=/usr/local/bin/ollama serve
============================================
# 配置并行处理请求的数量
Environment="OLLAMA_NUM_PARALLEL=8"
# 配置同时加载的模型数量
Environment="OLLAMA_MAX_LOADED_MODELS=20"
# 是否在所有GPU上调度模型（默认false，示例：true）
Environment="OLLAMA_SCHED_SPREAD=true"
# 启用 Flash Attention（默认false，示例值：1）
Environment="OLLAMA_FLASH_ATTENTION=1"
# ollama 指定GPU运行
Environment="CUDA_VISIBLE_DEVICES=2"
============================================
User=ollama
Group=ollama
Restart=always
RestartSec=3
Environment="PATH=/home/liubl/miniconda3/envs/RP8/bin:/home/liubl/miniconda3/condabin:/home/liubl/miniconda3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin"

[Install]
WantedBy=default.target
```

保存并退出后，重新加载 systemd 配置：
```shell
sudo systemctl daemon-reload
```

启动并使 Ollama 服务开机自启：
```shell
sudo systemctl start ollama
sudo systemctl enable ollama
```
重启Ollama服务
```shell
sudo systemctl restart ollama.service
```

检查服务状态：
```shell
sudo systemctl status ollama
```

**Ollama可配置环境变量 **

```shell
OLLAMA_DEBUG: 显示调试信息（默认false，示例值：1）
OLLAMA_FLASH_ATTENTION: 启用 Flash Attention（默认false，示例值：1）
OLLAMA_KV_CACHE_TYPE: K/V 缓存类型（默认f16，可选：f32/q8等）
OLLAMA_GPU_OVERHEAD: 单GPU预留VRAM[字节]（默认0，示例：2147483648=2GB）
OLLAMA_HOST: 服务地址（默认127.0.0.1:11434，示例：0.0.0.0:443）
OLLAMA_KEEP_ALIVE: 模型驻留时长（默认"5m"，示例："24h"/"-1"表示永久）
OLLAMA_LLM_LIBRARY: 强制指定LLM库（示例：custom_cuda_lib，用于绕过自动检测）
OLLAMA_LOAD_TIMEOUT: 模型加载超时时间（默认"5m"，示例："10m"）
OLLAMA_MAX_LOADED_MODELS: 单GPU最大加载模型数（默认自动，示例：3）
OLLAMA_MAX_QUEUE: 最大请求队列长度（默认512，示例：1024）
OLLAMA_MODELS: 模型存储路径（默认~/.ollama/models，示例：/mnt/data/models）
OLLAMA_NOHISTORY: 禁用CLI历史记录（默认false，示例：true）
OLLAMA_NOPRUNE: 禁用启动时修剪模型blob（默认false，示例：true）
OLLAMA_NUM_PARALLEL: 最大并行请求数（默认自动，示例：4）
OLLAMA_ORIGINS: 允许的跨域源（逗号分隔，示例：http://*.example.com,https://app.test ）
OLLAMA_SCHED_SPREAD: 是否在所有GPU上调度模型（默认false，示例：true）
OLLAMA_MULTIUSER_CACHE: 多用户缓存优化（默认false，示例：1）
OLLAMA_CONTEXT_LENGTH: 默认上下文长度（默认4096，示例：8192）
OLLAMA_NEW_ENGINE: 启用新引擎（默认false，示例：1）

# 代理设置
HTTP_PROXY: HTTP代理地址（示例：http://proxy.example.com:8080）
HTTPS_PROXY: HTTPS代理地址（示例：https://proxy.example.com:8080 ）
NO_PROXY: 不使用代理的域名或IP列表（逗号分隔，示例：localhost,127.0.0.1）

# GPU相关（非macOS平台）
CUDA_VISIBLE_DEVICES: 可见的NVIDIA设备ID（示例：0,1）
HIP_VISIBLE_DEVICES: 可见的AMD设备ID（按数字编号）（示例：0,1）
ROCR_VISIBLE_DEVICES: 可见的AMD设备ID（支持UUID或数字编号）（示例：0,1）
GPU_DEVICE_ORDINAL: 设置可见的AMD设备（按数字编号）（示例：0）
HSA_OVERRIDE_GFX_VERSION: 强制覆盖AMD GPU的GFX版本（示例：9.0.0）
OLLAMA_INTEL_GPU: 启用实验性Intel GPU检测（默认false，示例：1）
```

**常用配置**

1.显卡资源使用不均横
设置环境变量OLLAMA_SCHED_SPREAD为1即可

2.加速计算
FlashAttention 是一种优化的注意力机制，用于加速深度学习模型中常见的自注意力计算，尤其是在Transformer架构中。它通过改进内存访问模式和计算策略，显著提高了计算效率和内存使用率。
我们可以通过设置环境变量OLLAMA_FLASH_ATTENTION为1，开启改选项

3.增加上下文窗口
假设你从Ollama上拉取了大模型，其默认的窗口大小只有2048。我们可以通过如下方法，提高上下文窗口
ollama show --modelfile qwen2.5-coder > Modelfile
