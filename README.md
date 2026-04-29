# TradingAgents-CN 🤖📈

> **TradingAgents-CN** 是 [hsliuping/TradingAgents-CN](https://github.com/hsliuping/TradingAgents-CN) 的 Fork 版本，专注于中国 A 股市场的智能交易代理系统。

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)
[![Docker](https://img.shields.io/badge/Docker-Supported-blue)](https://www.docker.com/)

## 📖 项目简介

TradingAgents-CN 是一个基于多智能体（Multi-Agent）框架的 A 股量化交易分析系统，利用大语言模型（LLM）驱动多个专业分析师代理协同工作，为投资决策提供全面的市场分析支持。

### 核心特性

- 🧠 **多智能体协作**：基本面分析师、技术面分析师、情绪分析师、风险管理师协同决策
- 📊 **A 股数据支持**：集成 AkShare、Tushare 等主流中国金融数据源
- 🔄 **实时市场分析**：支持实时行情数据获取与分析
- 🤖 **多 LLM 支持**：兼容 OpenAI、DeepSeek、通义千问、智谱 AI 等主流大模型
- 🐳 **Docker 部署**：提供完整的容器化部署方案
- 📈 **回测框架**：内置历史数据回测功能

## 🚀 快速开始

### 环境要求

- Python 3.10+
- Docker & Docker Compose（可选）
- 至少一个 LLM API Key

### 安装步骤

#### 方式一：本地安装

```bash
# 克隆项目
git clone https://github.com/your-username/TradingAgents-CN.git
cd TradingAgents-CN

# 创建虚拟环境
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# 安装依赖
pip install -r requirements.txt

# 配置环境变量
cp .env.example .env
# 编辑 .env 文件，填入你的 API Keys
```

#### 方式二：Docker 部署

```bash
# 克隆项目
git clone https://github.com/your-username/TradingAgents-CN.git
cd TradingAgents-CN

# 配置环境变量
cp .env.docker .env
# 编辑 .env 文件，填入你的 API Keys

# 启动服务
docker-compose up -d
```

### 基础使用

```python
from tradingagents import TradingAgentsGraph
from tradingagents.default_config import DEFAULT_CONFIG

# 初始化配置
config = DEFAULT_CONFIG.copy()
config["llm_provider"] = "deepseek"
config["deep_think_llm"] = "deepseek-reasoner"
config["quick_think_llm"] = "deepseek-chat"

# 创建交易代理
ta = TradingAgentsGraph(debug=True, config=config)

# 分析股票
state, decision = ta.propagate("600519", "2024-01-15")
print(decision)
```

## 🏗️ 项目结构

```
TradingAgents-CN/
├── tradingagents/          # 核心模块
│   ├── agents/             # 各类分析师代理
│   │   ├── analysts/       # 分析师（基本面、技术面、情绪、新闻）
│   │   ├── managers/       # 管理层（研究员、风险管理）
│   │   └── trader/         # 交易决策代理
│   ├── dataflows/          # 数据流处理
│   │   ├── akshare_utils.py
│   │   ├── tushare_utils.py
│   │   └── interface.py
│   ├── graph/              # 代理图结构
│   └── default_config.py   # 默认配置
├── web/                    # Web 界面（Streamlit）
├── tests/                  # 测试用例
├── docs/                   # 文档
├── docker-compose.yml      # Docker 编排文件
├── Dockerfile              # Docker 镜像文件
├── requirements.txt        # Python 依赖
└── .env.example            # 环境变量示例
```

## ⚙️ 配置说明

详细配置请参考 [`.env.example`](.env.example) 文件，主要配置项包括：

| 配置项 | 说明 | 必填 |
|--------|------|------|
| `OPENAI_API_KEY` | OpenAI API Key | 否 |
| `DEEPSEEK_API_KEY` | DeepSeek API Key | 否 |
| `DASHSCOPE_API_KEY` | 通义千问 API Key | 否 |
| `ZHIPU_API_KEY` | 智谱 AI API Key | 否 |
| `TUSHARE_TOKEN` | Tushare 数据 Token | 否 |
| `MONGODB_URI` | MongoDB 连接地址 | 否 |

> ⚠️ **注意**：至少需要配置一个 LLM API Key 才能正常运行。

## 🤝 贡献指南

欢迎提交 Issue 和 Pull Request！请先阅读 [贡献指南](CONTRIBUTING.md)。

## 📄 许可证

本项目基于 [MIT License](LICENSE) 开源。

## 🙏 致谢

- 原项目：[hsliuping/TradingAgents-CN](https://github.com/hsliuping/TradingAgents-CN)
- 上游项目：[TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents)
