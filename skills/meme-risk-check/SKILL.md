---
name: meme-risk-check
description: Evaluates MEME token risk before buying. Combines on-chain data, smart money presence, and social sentiment to give a risk rating. Invoke when user asks if a meme token is worth buying or wants a risk assessment.
---

# MEME Risk Check

## Trigger Conditions

Invoke when user says:
- "这个土狗能不能买 / 值得买吗"
- "帮我看看这个 MEME 币"
- "[代币名] 风险怎么样"
- "这个项目是不是骗局 / rug pull"
- "MEME 风险评估"

## Pre-Check

Ask user for: **代币名称或合约地址 + 链名**（如果没有提供）

## Steps

1. **搜索交易对** — 确认代币存在并获取基本数据
   ```
   ant_meme(query_type="search_pairs", query=[代币名或地址])
   ```

2. **链上指标** — 检查代币健康度
   ```
   ant_token_analytics(query_type="token_screener", chain=[链名])
   ```

3. **聪明钱是否介入** — 专业玩家有没有买
   ```
   ant_smart_money(query_type="dex_trades", chains='["[链名]"]', filters='{"value_usd":{"min":5000}}')
   ```
   然后过滤出该代币的交易记录

4. **社区热度** — 检查 Boost 和社区接管状态
   ```
   ant_meme(query_type="boost_top")
   ant_meme(query_type="community_takeover")
   ```

5. **情绪时序**（如果代币有足够知名度）
   ```
   ant_market_sentiment(query_type="coin_time_series", coin=[代币标识], interval="1w")
   ```

## Output Format

```
## [代币名] 风险评估

**风险评级：** 🔴 高风险 / 🟡 中风险 / 🟢 相对安全

**基本面：**
- 流动性：$xxx
- 24h 交易量：$xxx
- FDV：$xxx

**聪明钱信号：**
- [有/无] 聪明钱介入，[买入/卖出]金额 $xxx

**社区热度：**
- Boost 数量：xxx（500+ 解锁 Golden Ticker）
- 是否 CTO：[是/否]

**风险点：**
- [流动性过低 / 无聪明钱 / 情绪下行 / ...]

**结论：**
[1-2句话直接给出建议]
```

## Notes

- 风险评级标准：聪明钱介入 + 流动性 > $100k + 情绪上升 → 🟢；任意两项不满足 → 🟡；三项均不满足 → 🔴
- 永远提醒用户：MEME 投资高风险，以上分析不构成投资建议
