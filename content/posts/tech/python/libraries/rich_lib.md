+++
title = 'Rich'
date = 2025-10-21T17:44:41+08:00
draft = true
slug = "156ed8d"
description = "Rich 实战速查：复制即用的常见场景与工程化模板"
summary = "更少概念、更强操作：表格、进度、日志、异常、Syntax、Markdown 等一屏速用"
tags = [ "技术", "开发" ]
categories = [ "tech" ]
cover = ""
author = "MapleScraps"
+++

# Rich 实战速查
直接可用的代码片段与工程化模板，贴到你的 CLI/脚本/服务就能跑。

- 安装与基础
- 复制即用（10 个常见场景）
- 工程化模板（统一 Console/日志）
- 常见陷阱与兼容
- 速查表


## 安装与基础
```bash
python -m pip install rich  # 安装 Rich 库，启用终端富文本能力
```
```python
from rich import print  # 导入 Rich 的 print 函数，替代内置 print
print("Hello, [bold magenta]World[/]!")  # 使用 markup 在字符串内局部着色

from rich.console import Console  # 导入 Console 类，提供更可控的输出
console = Console()  # 创建 Console 实例，自动检测终端宽度与能力
console.print("Hello", "World!", style="bold red")  # 使用 style 为整段应用样式

from rich import pretty  # 导入 pretty 模块，用于美化对象打印
pretty.install()  # 安装后，REPL/脚本中所有对象以更可读的格式显示
```


## 复制即用（10 个常见场景）

### 1) 彩色打印（局部+整段）
```python
from rich import print  # 导入 Rich 的 print
print("错误: [bold red]连接失败[/]，请稍后重试")  # 局部着色：红色加粗强调错误信息

from rich.console import Console  # 导入 Console 类
Console().print("整个段落", style="bold green")  # 整段样式：整段文字加粗绿色
```

### 2) 表格汇总
```python
from rich.table import Table  # 导入表格组件 Table
from rich.console import Console  # 导入 Console 用于打印

console = Console()  # 创建 Console 实例
table = Table(title="服务状态")  # 创建表格并设置标题

table.add_column("服务", style="cyan", no_wrap=True)  # 添加列：服务名，青色，禁止自动换行
table.add_column("状态", style="green")  # 添加列：状态，绿色
table.add_column("耗时(ms)", justify="right")  # 添加列：耗时，右对齐

for name, ok, ms in [("auth", True, 32), ("api", False, 215)]:  # 模拟服务数据迭代
    table.add_row(name, "✅" if ok else "❌", str(ms))  # 添加行：根据状态选择 Emoji，耗时转字符串

console.print(table)  # 打印表格到终端
```

### 3) 进度条（短任务）
```python
from time import sleep  # 导入 sleep 模拟耗时操作
from rich.progress import Progress  # 导入进度条组件 Progress

with Progress() as progress:  # 创建并自动清理进度条上下文
    task = progress.add_task("下载中", total=100)  # 新建任务：名称与总量 100
    for _ in range(100):  # 循环 100 次，模拟逐步推进
        sleep(0.02)  # 模拟每步耗时 20ms
        progress.update(task, advance=1)  # 更新任务：前进 1 单位
```

### 4) Markdown 渲染（说明/帮助）
```python
from rich.console import Console  # 导入 Console
from rich.markdown import Markdown  # 导入 Markdown 渲染器

md = Markdown("""
# 标题
- 支持列表
- 支持代码块
""")  # 创建 Markdown 对象：传入 Markdown 文本
Console().print(md)  # 将 Markdown 渲染并打印到终端
```

### 5) 代码高亮（Syntax）
```python
from rich.syntax import Syntax  # 导入代码高亮组件 Syntax
from rich.console import Console  # 导入 Console

code = "print('hello rich')\nfor i in range(3): print(i)"  # 示例代码字符串（包含换行）
Console().print(Syntax(code, "python", theme="monokai", line_numbers=True))  # 以 Python 语言高亮，启用行号与主题
```

### 6) 异常栈美化（Traceback）
```python
from rich.traceback import install  # 导入异常美化安装函数
install(show_locals=True)  # 安装后所有未捕获异常以彩色/结构化显示，并展示局部变量

# 正常写代码即可；发生异常时自动输出美化后的 Traceback
```

### 7) 调试对象（inspect）
```python
from rich import inspect  # 导入 inspect 用于对象结构化展示
obj = {"user": "alice", "roles": ["admin", "ops"]}  # 示例对象：字典包含列表
inspect(obj, methods=True)  # 展示对象内容并列出可用方法
```

### 8) 日志美化（直接替换 logging）
```python
import logging  # 导入标准库 logging
from rich.logging import RichHandler  # 导入 Rich 的日志处理器，用于着色与结构化输出

logging.basicConfig(  # 配置基础日志设置
    level="INFO",  # 设置日志级别为 INFO
    format="%(message)s",  # 日志格式仅输出消息体（便于终端阅读）
    datefmt="%H:%M:%S",  # 时间格式：时:分:秒
    handlers=[RichHandler()]  # 替换默认 Handler 为 RichHandler
)
log = logging.getLogger("svc")  # 获取名为 svc 的日志记录器
log.info({"event": "started", "port": 8080})  # 输出结构化日志（字典），Rich 友好显示
```

### 9) Panel/状态信息（CLI 友好）
```python
from rich.panel import Panel  # 导入 Panel 面板组件
from rich.console import Console  # 导入 Console
Console().print(Panel.fit("部署完成 ✅", title="结果", border_style="green"))  # 渲染紧凑型面板，设置标题与绿色边框
```

### 10) 关闭颜色（非 TTY/重定向场景）
```python
import sys  # 导入 sys 以检测标准输出是否为 TTY
from rich.console import Console  # 导入 Console

is_tty = sys.stdout.isatty()  # 判断当前 stdout 是否连接到终端
console = Console(color_system=None if not is_tty else "auto")  # 非 TTY 时禁用颜色，TTY 时自动选择颜色系统
console.print("这段在非 TTY 下无颜色输出")  # 打印测试行，确保在重定向/文件中无 ANSI 颜色
```


## 工程化模板（统一 Console/日志）
将 Rich 集中封装，避免到处 new Console/配置 logging。
```python
# utils/console.py  # 模块路径建议：统一管理 Console 与日志
import sys  # 导入 sys 检测终端类型
import logging  # 导入标准库 logging
from rich.console import Console  # 导入 Console
from rich.logging import RichHandler  # 导入 RichHandler 用于日志美化

is_tty = sys.stdout.isatty()  # 判断 stdout 是否为 TTY
console = Console(color_system=None if not is_tty else "auto")  # 根据环境决定是否着色

logging.basicConfig(  # 配置全局日志格式与处理器
    level="INFO",  # 全局日志级别
    format="%(message)s",  # 简洁消息格式，适合人类阅读
    datefmt="%H:%M:%S",  # 时间格式
    handlers=[RichHandler(console=console)]  # 使用同一个 Console 的 RichHandler，保持输出一致
)
log = logging.getLogger("app")  # 提供统一的应用日志记录器
```
```python
# 在任意模块使用  # 示例：如何在其他模块里使用统一的 Console 与日志
from utils.console import console, log  # 导入统一封装的 console 与 log

console.print("启动中…", style="bold cyan")  # 输出启动提示，青色加粗
log.info({"event": "boot", "version": "1.2.3"})  # 输出结构化日志，标记版本信息
```


## 常见陷阱与兼容
- 经典 Windows 终端颜色有限：尽量使用 Windows Terminal 以获得真彩与 Emoji。
- 宽表格/长行：终端宽度有限，设置 `no_wrap`/`justify`，或拆分输出。
- 进度条在 CI：非交互环境可能乱；检测非 TTY 时禁用。
- 重定向到文件：ANSI 颜色会“脏”；关闭颜色或使用支持 ANSI 的查看器。


## 速查表
- 控制台：`Console().print` `style="bold red"` `markup`
- 表格：`Table(title)` `add_column` `add_row` `justify` `no_wrap`
- 进度：`Progress.add_task` `update(advance=...)`
- Markdown：`Markdown(text)`
- 高亮：`Syntax(code, "python")`
- 异常：`traceback.install(show_locals=True)`
- 调试：`inspect(obj, methods=True)`
- 日志：`RichHandler()` `logging.basicConfig(handlers=[...])`
- Emoji：`":rocket:"` `":smiley:"`


## 参考
- Rich 官方 README（简体中文）：https://github.com/textualize/rich/blob/master/README.cn.md