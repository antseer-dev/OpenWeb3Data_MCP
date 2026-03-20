---
name: solana-ecosystem-pulse
description: Solana ecosystem snapshot covering SOL price and fundamentals, on-chain DeFi TVL and DEX volumes, smart money activity on Solana, and trending MEME tokens on Solana. Invoke when user asks about Solana ecosystem health, SOL outlook, or what's happening on Solana today.
---

# Solana Ecosystem Pulse

## 触发条件

Invoke when user says:
- "Solana / SOL 生态怎么样"
- "SOL 今天行情 / SOL 能涨吗"
- "Solana 链上在发生什么"
- "Solana DeFi / DEX 情况"
- "Solana 生态热点"
- "SOL 现在值得买吗"

## Steps

1. **SOL 现货行情** — 价格、市值、24h 涨跌
   ```
   ant_spot_market_structure(query_type="coin_detail", coin_id="solana")
   ```

2. **Solana 链上 DeFi TVL** — 生态锁仓总量趋势
   ```
   ant_protocol_tvl_yields_revenue(query_type="chain_tvl_history", chain="Solana")
   ```

3. **Solana DEX 交易量排名** — 哪些协议最活跃
   ```
   ant_protocol_tvl_yields_revenue(query_type="dex_overview", chain="Solana", limit=8)
   ```

4. **Solana 链上收益机会** — 当前最优质的 yield 池
   ```
   ant_protocol_tvl_yields_revenue(query_type="yield_pools", chain="Solana", min_tvl_usd=500000, sort_by="apy", sort_order="desc", limit=5)
   ```

5. **聪明钱 Solana 方向** — 专业玩家在 Solana 上的最新操作
   ```
   ant_smart_money(query_type="dex_trades", chains='["solana"]', order_by='[{"field":"timestamp","direction":"DESC"}]', pagination='{"page":1,"per_page":10}')
   ```

6. **Solana MEME 热门** — 当前最热的 Solana meme 代币
   ```
   ant_meme(query_type="boost_top", limit=5)
   ```
   过滤出 chain_id 为 "solana" 的项目

7. **Solana MEME 社区接管** — 有无 CTO 项目值得关注
   ```
   ant_meme(query_type="community_takeover", limit=5)
   ```

8. **SOL 社区情绪趋势**
   ```
   ant_market_sentiment(query_type="coin_time_series", coin="solana", bucket="day", interval="1m")
   ```

## Output Format

```
## Solana 生态脉搏 — [日期]

**SOL 行情：**
- 价格：$xxx | 24h：+/-x.x% | 市值：$xxxB | 排名：#xx

**链上 DeFi 健康度：**
- Solana 总 TVL：$xxxB（7日趋势：↑/↓）

**DEX 活跃度 Top 3：**
| 协议 | 24h 交易量 | TVL |
|------|-----------|-----|
| xxx  | $xxxM     | $xxxM |

**最优 Yield 机会：**
- [协议] [池子] APY: xx% | TVL: $xM

**聪明钱 Solana 动向：**
- 最新大单：[买入/卖出] [代币] $xxx on Solana
- 整体偏向：[买入/卖出/中性]

**Solana MEME 雷达：**
- 🔥 热度 Top：[代币] Boost: xxx [Golden Ticker标识]
- 🏳️ CTO 项目：[代币]（接管日期）

**情绪指数：**
- SOL 社区情绪：[上升/下降/震荡]（过去30天）

**综合判断：**
[2-3句话：Solana 生态当前活跃度、SOL 价格关键信号、值得关注的机会或风险]

⚠️ 以上分析不构成投资建议
```

## Notes

- 如用户问的是具体 Solana 协议（如 Jupiter、Raydium），在 Step 3 结果中重点展示该协议数据
- 如 MEME 数据中无 Solana 项目，跳过 Step 6/7，说明暂无热点
- SEC 于 2026 年 3 月将 SOL 正式认定为数字商品，分析 SOL 基本面时可提及这一重要背景
