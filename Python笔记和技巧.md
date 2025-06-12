# Python笔记和技巧

## python 路径导入问题解决方法

1. 方法1:通过sys.path将上级，上上级目录添加到路径中。
```python
# 在任何入口文件开头添加以下代码
import os
import sys

# 自动定位项目根目录
PROJECT_ROOT = os.path.abspath(os.path.join(os.path.dirname(__file__), '..', '..'))
if PROJECT_ROOT not in sys.path:
    sys.path.insert(0, PROJECT_ROOT)

# 现在可以安全导入顶层模块
from configs import cfgs

```
