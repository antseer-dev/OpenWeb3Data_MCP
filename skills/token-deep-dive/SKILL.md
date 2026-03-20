---
name: token-deep-dive
description: Full research report on any crypto token combining on-chain metrics, smart money activity, social sentiment, and market structure. Invoke when user wants comprehensive token research or due diligence.
---

# Token Deep Dive

## Trigger Conditions

Invoke when user says:
- "帮我研究 [代币]"
- "深度分析 / 详细分析这个项目"
- "[代币] 值得投资吗"
- "给我一份 [代币] 研究报告"
- "这个项目基本面怎么样"

## Pre-Check

Ask user for: **代币名称**（如 bitcoin、ethereum）或合约地址 + 链名

## Steps

1. **基本市场数据**
   ```
   ant_spot_market_structure(query_type="coin_detail", coin_id=[代币ID])
   ```

2. **链上网络指标**（BTC/ETH）
   ```
   ant_token_analytics(query_type="nvt", asset=[btc/eth], window="day", limit=30)
   ant_token_analytics(query_type="mvrv", asset=[btc/eth], window="day", limit=7)
   ```
   或链上代币分析（其他代币需合约地址）：
   ```
   ant_token_analytics(query_type="token_screener", chain=[链名])
   ```

3. **聪明钱持仓**
   ```
   ant_smart_money(query_type="holdings", chains='["all"]', filters='{"value_usd":{"min":10000}}')
   ```
   过滤该代币相关记录

4. **聪明钱买卖方向**
   ```
   ant_token_analytics(query_type="who_bought_sold", token_address=[地址], chain=[链], buy_or_sell="BUY")
   ```

5. **社区情绪趋势**
   ```
   ant_market_sentiment(query_type="coin_time_series", coin=[代币标识], bucket="day", interval="1m")
   ```

6. **协议收益**（DeFi 项目时）
   ```
   ant_protocol_tvl_yields_revenue(query_type="protocol_overview", protocol=[协议slug])
   ```

7. **解锁计划**（检查代币抛压）
   ```
   ant_token_analytics(query_type="emission_detail", asset=[协议名])
   ```

## Output Format

```
## [代币名] 深度研究报告

**基本面：**
- 市值：$xxxB | 排名：#xx | 24h 交易量：$xxxM
- 全稀释市值：$xxxB | 流通比例：xx%

**链上健康度：**
- NVT：xx（高估/低估/合理）
- MVRV：x.xx（获利/亏损持仓占比）

**聪明钱信号：**
- 近期净买入/卖出：$xxxM
- 当前持仓价值：$xxxM

**社区情绪：**
- 过去30天趋势：上升/下降/震荡
- 当前情绪得分：xx/100

**代币解锁风险：**
- 近期大额解锁：[日期] xxx个代币（$xxxM）

**综合评分：**
| 维度 | 评分 |
|------|------|
| 基本面 | ⭐⭐⭐⭐ |
| 链上健康 | ⭐⭐⭐ |
| 聪明钱认可 | ⭐⭐⭐⭐ |
| 社区情绪 | ⭐⭐⭐ |

**结论：**
[3-4句话的投资判断，包含主要风险和机会]

⚠️ 以上分析不构成投资建议
```
