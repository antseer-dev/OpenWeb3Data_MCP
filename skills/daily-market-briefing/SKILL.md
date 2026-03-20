---
name: daily-market-briefing
description: Comprehensive daily crypto market summary covering spot prices, futures structure, funding rates, ETF flows, and key signals. Invoke when user asks for today's market overview or daily briefing.
---

# Daily Market Briefing

## Trigger Conditions

Invoke when user says:
- "今天市场怎么样 / 行情如何"
- "给我一个市场总结 / 日报"
- "BTC 今天能不能上 / 涨跌分析"
- "市场概览 / 全局行情"
- "早报 / 晚报"

## Steps

1. **现货行情** — 主流币价格和涨跌幅
   ```
   ant_spot_market_structure(query_type="coins_markets", order="market_cap_desc", per_page=10)
   ```

2. **全局统计** — 总市值、BTC 占比、贪婪恐惧
   ```
   ant_spot_market_structure(query_type="global_stats")
   ```

3. **期货 OI 与资金费率** — 市场情绪方向
   ```
   ant_futures_market_structure(query_type="futures_oi_aggregated", symbol="BTC", interval="1h", limit=24)
   ant_futures_market_structure(query_type="futures_funding_rate_oi_weight", symbol="BTC", interval="1h", limit=1)
   ```

4. **多空比** — 大户持仓方向
   ```
   ant_futures_market_structure(query_type="futures_long_short_top_position", symbol="BTC", interval="1h", limit=1)
   ```

5. **ETF 资金流** — 机构资金进出
   ```
   ant_etf_fund_flow(query_type="btc_etf_flow", limit=3)
   ```

6. **技术指标** — RSI 超买超卖
   ```
   ant_market_indicators(query_type="rsi", symbol="BTC")
   ```

## Output Format

```
## 加密市场日报 — [日期]

**主流币行情：**
- BTC: $xxx (+x.x%) | ETH: $xxx (+x.x%) | SOL: $xxx (+x.x%)
- 总市值：$x.xT | BTC 占比：xx%

**期货市场：**
- BTC OI：$xxxB（↑/↓ x%）
- 资金费率：x.xxx%（多/空 占优）
- 大户多空比：x.xx（偏多/偏空）

**机构动向：**
- BTC ETF 近3日净流入：+$xxxM / 净流出：-$xxxM

**技术信号：**
- BTC RSI：xx（超买/超卖/中性）

**今日核心信号：**
[2-3句话总结今日最重要的市场信号和方向判断]
```
