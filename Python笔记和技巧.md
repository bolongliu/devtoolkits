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
2. 使用专用函数导入

```python
#!/usr/bin/env python3
"""
测试导入辅助模块
帮助test目录下的文件正确导入其他模块
"""
import os
import sys
from pathlib import Path

def setup_test_environment():
    """
    设置测试环境，添加必要的路径到sys.path
    """
    # 获取当前文件的目录
    current_dir = Path(__file__).parent
    
    # 获取项目根目录（code目录）
    project_root = current_dir.parent
    
    # 将项目根目录添加到Python路径
    if str(project_root) not in sys.path:
        sys.path.insert(0, str(project_root))
    
    # 将当前目录也添加到路径中
    if str(current_dir) not in sys.path:
        sys.path.insert(0, str(current_dir))
    
    print(f"测试环境设置完成:")
    print(f"  项目根目录: {project_root}")
    print(f"  测试目录: {current_dir}")
    print(f"  Python路径: {sys.path[:3]}...")

def import_from_project(module_name):
    """
    从项目根目录导入模块
    
    Args:
        module_name: 模块名称
        
    Returns:
        导入的模块
    """
    setup_test_environment()
    return __import__(module_name)

# 自动设置环境
setup_test_environment()

使用方法

例如在test/目录下测试所有测试脚本
test_import_sample.py中导入如下命令
# 首先导入测试环境设置
from test_import_helper import setup_test_environment
setup_test_environment()
```

