## 项目名称
**FinRL® (Financial Reinforcement Learning)** - 金融强化学习框架

## 系统功能
FinRL是第一个开源的金融强化学习框架，主要功能包括：

- **多数据源支持**：支持15+个数据源，包括Yahoo Finance、Alpaca、Binance、Tushare等
- **强化学习算法集成**：集成多种DRL算法（A2C、PPO、DDPG、TD3、SAC等）
- **多种金融应用**：股票交易、加密货币交易、投资组合优化、高频交易等
- **技术指标计算**：支持MACD、RSI、布林带等多种技术指标
- **回测与实盘交易**：提供完整的训练-测试-交易流水线
- **风险管理**：包含波动率指标(VIX)和湍流度指标

## 系统架构
采用**三层架构设计**：

1. **应用层 (Applications)**：具体的金融任务实现
2. **智能体层 (Agents)**：强化学习算法实现
3. **环境层 (Meta)**：市场环境和数据处理

**核心流水线**：Train → Test → Trade

## 业务模块

### 1. 数据处理模块 (`meta/data_processors/`)
- 支持多个数据源的统一接口
- 数据清洗和预处理
- 技术指标计算

### 2. 环境模块 (`meta/env_*/`)
- **股票交易环境**：标准股票交易、现金惩罚、止损等
- **加密货币交易环境**：比特币和多币种交易
- **投资组合环境**：资产配置和优化

### 3. 智能体模块 (`agents/`)
- **ElegantRL**：高性能DRL算法库
- **Stable Baselines3**：经典强化学习算法
- **RLlib**：分布式强化学习
- **投资组合优化**：专门的投资组合算法

### 4. 应用模块 (`applications/`)
- **Stock_NeurIPS2018**：经典股票交易案例
- **加密货币交易**：数字货币交易策略
- **高频交易**：高频交易算法
- **模仿学习**：基于专家策略的学习
- **投资组合分配**：资产配置策略

## 层次结构

```
FinRL/
├── finrl/                    # 核心框架
│   ├── applications/         # 应用层
│   ├── agents/              # 智能体层
│   ├── meta/                # 环境和数据层
│   ├── config.py            # 全局配置
│   ├── main.py              # 主入口
│   ├── train.py             # 训练模块
│   ├── test.py              # 测试模块
│   └── trade.py             # 交易模块
├── examples/                # 示例和教程
├── docs/                    # 文档
├── unit_tests/              # 单元测试
└── requirements.txt         # 依赖配置
```

## 使用方法

### 1. 安装依赖
```bash
pip install -r requirements.txt
# 或使用 Poetry
poetry install
```

### 2. 基本使用流程

**数据下载和处理**：
```python
from finrl.meta.data_processor import DataProcessor
dp = DataProcessor(data_source="yahoofinance")
data = dp.download_data(ticker_list, start_date, end_date, time_interval)
```

**模型训练**：
```python
from finrl.train import train
train(start_date, end_date, ticker_list, data_source, 
      time_interval, technical_indicator_list, drl_lib, env, model_name)
```

**回测和交易**：
- 使用 `test.py` 进行策略回测
- 使用 `trade.py` 进行实盘交易

### 3. 配置参数
- **时间配置**：训练、测试、交易时间段
- **技术指标**：MACD、RSI、布林带等
- **模型参数**：各种DRL算法的超参数
- **API配置**：各数据源的API密钥

### 4. 运行模式
```bash
python -m finrl.main --mode train      # 训练模式
python -m finrl.main --mode backtest   # 回测模式
python -m finrl.main --mode download_data  # 数据下载
```

## 技术栈
- **核心框架**：Python 3.7+
- **机器学习**：Stable Baselines3、ElegantRL、Ray RLlib
- **数据处理**：Pandas、NumPy、Stockstats
- **可视化**：Matplotlib、TensorBoard
- **金融数据**：yfinance、alpaca-trade-api、ccxt
- **依赖管理**：Poetry

FinRL提供了一个完整的金融强化学习生态系统，从数据获取到模型训练再到实盘交易，为量化交易研究和应用提供了强大的工具支持。
        