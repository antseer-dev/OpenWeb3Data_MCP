---
name: smart-money-analysis
description: Tracks smart money wallet activity — what professional traders and institutions are buying, selling, or holding on-chain. Invoke when user asks about smart money flows, what whales are buying, or institutional on-chain activity.
---

# Smart Money Analysis

## Trigger Conditions

Invoke when user says:
- "聪明钱在买什么 / 卖什么"
- "smart money 最新动向"
- "机构在链上买了什么"
- "专业交易员在操作什么"
- "链上大户最新持仓"

## Steps

1. **资金净流向** — 聪明钱最近在净买入还是净卖出哪些代币
   ```
   ant_smart_money(query_type="netflows", chains='["all"]', pagination='{"page":1,"per_page":20}')
   ```

2. **当前持仓** — 聪明钱现在重仓哪些代币
   ```
   ant_smart_money(query_type="holdings", chains='["all"]', filters='{"value_usd":{"min":100000}}', order_by='[{"field":"value_usd","direction":"DESC"}]')
   ```

3. **DEX 交易记录** — 过去 24 小时的链上交易
   ```
   ant_smart_money(query_type="dex_trades", chains='["all"]', order_by='[{"field":"timestamp","direction":"DESC"}]', pagination='{"page":1,"per_page":10}')
   ```

4. **合约交易**（可选，用户关注衍生品时）
   ```
   ant_smart_money(query_type="perp_trades", order_by='[{"field":"timestamp","direction":"DESC"}]', pagination='{"page":1,"per_page":10}')
   ```

## Output Format

```
## 聪明钱动向摘要

**净流向 Top 5（买入）：**
- [代币] +$xxx,xxx（过去24h）

**净流向 Top 5（卖出）：**
- [代币] -$xxx,xxx（过去24h）

**当前重仓 Top 5：**
- [代币] $xxx,xxx

**最新 DEX 大单：**
- [时间] [买入/卖出] [代币] $xxx,xxx on [链]

**信号解读：**
[1-2句话总结聪明钱当前偏好方向]
```

## Notes

- 如用户指定链（如 "以太坊上的聪明钱"），在 chains 参数中指定对应链名
- 如用户指定标签（如 "Fund"），在 filters 中加 `include_smart_money_labels`
