# 安装与版本兼容说明

## 推荐环境

* Python 3.11 或更高版本。
* NumPy 1.26.4 或更高版本，支持 NumPy 2.x。
* pandas 2.2.2 或更高版本，支持 pandas 3.x。
* numexpr 2.10.2 或更高版本、Bottleneck 1.4.2 或更高版本；它们用于
pandas 表达式与缺失值等计算加速。
* 只使用技术指标、数据处理或 SQLite 工具时，不需要安装 QMT 的 xtquant。
安装或升级：

```powershell
python -m pip install --upgrade yuhanbolh
```

项目使用最低兼容版本范围，不再精确锁定某个补丁版本。因此，pip 会根据当前
Python 版本选择可安装的较新版本，不会为了安装 yuhanbolh 强制降级已有兼容版本。

## pandas 的 numexpr 与 Bottleneck 警告

如果导入 pandas 时出现以下含义的警告：

* pandas 要求 numexpr>=2.10.2，但当前环境仍是 2.8.7；
* pandas 要求 Bottleneck>=1.4.2，但当前环境仍是 1.3.7；
说明 pandas 已升级，但 Anaconda 环境中的可选加速库没有同步升级。该警告不是
yuhanbolh 函数计算错误；从包含新依赖声明的 yuhanbolh 版本开始，正常升级会同时
检查这两个最低版本。

Conda 环境优先使用同一包管理器修复：

```powershell
conda install "numexpr>=2.10.2" "bottleneck>=1.4.2"
python -m pip check
```

纯 pip 虚拟环境可以执行：

```powershell
python -m pip install --upgrade "numexpr>=2.10.2" "bottleneck>=1.4.2"
python -m pip check
```

如果基础 Anaconda 环境已经存在多组互相冲突的依赖，建议新建环境，不要用
--force-reinstall 强行覆盖：

```powershell
conda create -n yuhanbolh python=3.12 -y
conda activate yuhanbolh
python -m pip install --upgrade yuhanbolh
```

## Jupyter 与 ipykernel 7

需要最新版 Jupyter 内核时，建议创建独立虚拟环境：

```powershell
py -3.12 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install --upgrade "yuhanbolh[notebook]"
python -m ipykernel install --user --name yuhanbolh-latest --display-name "Python (yuhanbolh latest)"
```

ipykernel 不是 yuhanbolh 的必需运行依赖。可选项 yuhanbolh[notebook]
用于安装 ipykernel>=7，不会影响普通 Python、QMT 或 MT5 用户。

## Spyder 冲突说明

截至 2026-08-04，PyPI 上的 spyder-kernels 2.5.0 要求
ipykernel>=6.23.2,<7；最新版 spyder-kernels 3.1.5 仍要求
ipykernel>=6.29.3,<7。因此 Spyder 控制台与 ipykernel 7 暂时不能放在
同一个 Python 环境中，这属于 Spyder 上游依赖限制，并非 yuhanbolh 的限制。

处理方式二选一：

1. 使用 Spyder：保留 ipykernel 6.x，不要在该环境安装 yuhanbolh[notebook]。
1. 使用最新版 ipykernel：按上文创建独立虚拟环境，在 Jupyter、VS Code 或其他支持的客户端中使用。
检查当前环境：

```powershell
python -m pip show yuhanbolh numpy pandas numexpr bottleneck ipykernel spyder-kernels
python -m pip check
```

## QMT 与 MT5

* xtquant 不能通过普通 PyPI 安装，需要按迅投官方说明放入目标 Python 环境。
* MetaTrader5 功能需要 Windows、MT5 终端和真实账户环境。
* yuhanbolh 的包入口采用按需加载。没有 xtquant 时仍可导入并使用 MA、
EMA、RSI、ADX 等纯 NumPy/pandas 功能；调用 QMT 函数时才要求相应终端依赖。
## 从旧版本升级

旧版本曾精确要求 numpy==1.26.4 和 pandas==2.2.2。升级后建议执行：

```powershell
python -m pip install --upgrade yuhanbolh numpy pandas numexpr bottleneck
python -m pip check
```

如果 pip check 仍报告其他软件包限制 pandas、NumPy 或 ipykernel，请为不同工具
建立独立虚拟环境，不要通过强制覆盖依赖来获得表面上的“安装成功”。

## 2026-09-06 接口迁移

本次源码最低Python 3.11，AKShare >=1.18.94。大QMT独立服务端保持Python 3.6，不能在该内置环境安装本库代替服务端。数据库写入入口默认只返回数据，需显式提供db_path才保存。详见 [[问财与AKShare及大QMT桥接迁移说明]]。本地文档由用户自行同步远端。

