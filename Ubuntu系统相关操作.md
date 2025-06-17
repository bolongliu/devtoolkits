# Ubuntu系统相关操作

## 1. ubuntu添加环境变量
例如，将ollama增加高并发能力。
```shell
sudo vim /etc/environment

OLLAMA_MAX_LOADED_MODELS=4
OLLAMA_NUM_PARALLEL=4
```
