# Python笔记和技巧

## python 路径导入问题解决方法

0. 终极解决方案（简单直接版）在 运行的文件，如md_loader.py 开头添加：
```python
import os
import sys

# 简单直接：将项目根目录添加到模块搜索路径
sys.path.append(os.path.dirname(os.path.dirname(os.path.abspath(__file__))))
```


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
# 2. python专业项目结构示例
```shell
my_project/
├── pyproject.toml          # 项目配置
├── setup.cfg               # 包配置
├── src/                    # 源代码目录
│   └── my_package/         # Python 包
│       ├── __init__.py     # 使用绝对导入定义公开接口
│       ├── core/           # 核心模块
│       │   ├── __init__.py
│       │   ├── database.py
│       │   └── models.py   # 内部使用相对导入
│       ├── utils/          # 工具模块
│       │   ├── __init__.py
│       │   ├── logger.py
│       │   └── validators.py
│       └── api/            # API模块
│           ├── __init__.py
│           └── routes.py
├── tests/                  # 测试目录
│   ├── __init__.py
│   ├── test_database.py    # 使用绝对导入
│   └── test_routes.py
└── scripts/                # 脚本目录
    ├── deploy.py           # 使用绝对导入
    └── migrate_db.py
```

对于稳定可靠的项目：

​​优先使用绝对导入​​
​​将项目安装为包​​ (pip install -e .)
​​通过 init.py 明确定义公共API​​
​​测试代码统一使用绝对导入​​
​​包内部可使用显式相对导入，但通过公共接口暴露更好​​
这种混合策略结合了两种导入方式的优点，提供了清晰、稳定且易于维护的代码结构，适用于从初创项目到大型企业应用的各类场景。

## 3. python使用单元测试
这个脚本是使用 Python 标准库中的 unittest 框架实现的一个​​统一测试运行器​​，其主要功能是发现并执行项目中所有的测试用例。
```text
主要优势
1. ​​统一入口点 (Single Entry Point)​​
​​自动化测试发现​​：自动找到所有测试，无需手动管理测试列表
​​标准化运行方式​​：只需运行一个脚本即可执行全部测试
​​集中控制​​：可在单个点配置测试参数（如详细度、过滤等）
2. ​​平台无关性​​
基于 Python 标准库实现，不需要额外依赖
在任何支持 Python 的环境中都能运行
没有操作系统特异性命令，Windows/Linux/macOS 均可使用
3. ​​集成友好​​
​​CI/CD 友好​​：清晰的退出代码 (0/1) 让 CI 系统简单判断成败
​​日志输出规范​​：结构化的执行输出易于集成报告系统
​​可扩展性​​：轻松添加前置/后置操作
4. ​​维护性与可靠性​​
​​避免重复代码​​：共用统一的测试运行逻辑
​​错误隔离​​：捕获全局异常，避免错误导致脚本中断
​​健壮性​​：自动处理测试执行错误，继续运行其它测试
```


```python
#!/usr/bin/env python3
"""运行所有测试的统一入口"""
import unittest
import os

def run_all_tests():
    """发现并运行所有测试"""
    test_dir = os.path.join(os.path.dirname(__file__), 'tests')
    loader = unittest.TestLoader()
    suite = loader.discover(test_dir, pattern='test_*.py')
    
    print("=" * 50)
    print(f" 开始运行所有测试 (来自: {test_dir})")
    print("=" * 50)
    
    runner = unittest.TextTestRunner(verbosity=2)
    result = runner.run(suite)
    
    print("=" * 50)
    print(f" 测试结果: {'成功' if result.wasSuccessful() else '失败'}")
    print("=" * 50)
    
    return result.wasSuccessful()

if __name__ == '__main__':
    import sys
    success = run_all_tests()
    sys.exit(0 if success else 1)
```

**最佳实践建议**

组织测试结构​​：
```shell
​​
project/
├── src/
├── tests/
│   ├── test_unit/
│   ├── test_integration/
│   ├── test_system/
│   └── test_performance/
├── run_tests.py
```
