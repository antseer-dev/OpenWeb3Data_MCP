---
name: whale-alert-analysis
description: Analyzes large whale wallet movements on-chain including exchange inflows/outflows, large transfers, and specific wallet profiling. Invoke when user mentions whale activity, large transfers, or wants to track a specific address.
---

# Whale Alert Analysis

## Trigger Conditions

Invoke when user says:
- "鲸鱼 / 大户 / 巨鲸在动了"
- "有大额转账 / 大单"
- "交易所出现大额充提"
- "帮我查这个地址 [address]"
- "某某钱包在干什么"

## Steps

### 场景 A：通用鲸鱼动向监控

1. **交易所大额充值** — 鲸鱼往交易所转币（卖出信号）
   ```
   ant_fund_flow(query_type="exchange_inflow", asset="btc", exchange="binance", window="hour", limit=24)
   ```

2. **交易所大额提币** — 鲸鱼从交易所提币（持有信号）
   ```
   ant_fund_flow(query_type="exchange_outflow", asset="btc", exchange="binance", window="hour", limit=24)
   ```

3. **链上鲸鱼转账** — 大额链上转账记录
   ```
   ant_fund_flow(query_type="centralized_exchange_whale_transfer", symbol="BTC")
   ```

4. **Hyperliquid 鲸鱼仓位** — 链上合约大户仓位
   ```
   ant_perp_dex(query_type="perp_dex_whale_position", per_page=10)
   ```

### 场景 B：特定地址分析（用户提供地址时）

1. **钱包余额与交易记录**
   ```
   ant_address_profile(query_type="current_balance", address=[地址], chain=[链])
   ant_address_profile(query_type="transactions", address=[地址], chain=[链])
   ```

2. **盈亏情况**
   ```
   ant_address_profile(query_type="pnl_summary", address=[地址], chain=[链])
   ```

3. **交易对手方** — 这个钱包和谁在交互
   ```
   ant_address_profile(query_type="counterparties", address=[地址], chain=[链])
   ```

4. **地址标签** — 是否是已知实体
   ```
   ant_address_profile(query_type="labels", address=[地址], chain=[链])
   ```

## Output Format

```
## 鲸鱼动向分析

**交易所资金流（BTC，过去24h）：**
- 净流入：+xxx BTC（$xxxM）→ 卖压信号
- 净流出：-xxx BTC（$xxxM）→ 囤币信号

**链上大额转账：**
- [时间] [地址缩写] → [交易所] xxx BTC（$xxxM）

**Hyperliquid 鲸鱼仓位：**
- Top 仓位：[多/空] xxx BTC，入场价 $xxx，未实现盈亏 $xxx

**信号解读：**
[判断鲸鱼整体是在积累还是分发，对价格的潜在影响]
```

## Notes

- 场景 A 和 B 可组合使用
- 如用户关注 ETH，将 asset 从 "btc" 改为 "eth"
