---
name: defi-yield-scout
description: Discovers the best DeFi yield opportunities across protocols and chains, including liquidity pools, lending rates, and LSD yields. Invoke when user asks about DeFi yields, where to earn, or staking returns.
---

# DeFi Yield Scout

## Trigger Conditions

Invoke when user says:
- "哪里有高收益 / 高 APY"
- "DeFi 怎么赚钱 / 哪里挖矿"
- "质押 / staking 收益"
- "借贷利率 / 借贷收益"
- "流动性挖矿推荐"
- "稳定币哪里放最好"

## Pre-Check

Ask user：**关注哪条链？** 哪种风险偏好（稳定币/主流币/高风险）？最低 TVL 要求？

## Steps

1. **顶级收益池** — 按 APY 排序的流动性池
   ```
   ant_protocol_tvl_yields_revenue(query_type="yield_pools", chain=[用户指定链或留空], min_tvl_usd=1000000, sort_by="apy", sort_order="desc", limit=10)
   ```

2. **借贷收益** — 存款利率
   ```
   ant_protocol_tvl_yields_revenue(query_type="yield_borrow", chain=[链], min_tvl_usd=500000, limit=10)
   ```

3. **LSD 收益** — 流动性质押（ETH staking 等）
   ```
   ant_protocol_tvl_yields_revenue(query_type="yield_lsd", limit=10)
   ```

4. **协议 TVL 健康度** — 确认协议规模足够安全
   ```
   ant_protocol_tvl_yields_revenue(query_type="dex_overview", chain=[链], limit=5)
   ```

5. **安全记录检查** — 该协议是否有被黑历史
   ```
   ant_protocol_ecosystem(query_type="ecosystem_hacks", limit=20)
   ```
   对比用户感兴趣的协议名称

## Output Format

```
## DeFi 收益机会

**流动性池 Top 5（APY 排序）：**
| 协议 | 池子 | APY | TVL | 链 |
|------|------|-----|-----|-----|
| xxx  | xxx  | xx% | $xM | xxx |

**借贷存款利率 Top 3：**
- [协议] [代币] 存款利率：xx% APY，TVL $xM

**LSD 质押收益：**
- [协议] ETH 质押：x.xx% APY

**安全提示：**
- [协议名] [有/无] 黑客历史记录

**推荐：**
[根据用户风险偏好给出 1-2 个具体建议，说明理由]

⚠️ DeFi 存在智能合约风险，请做好风险管理
```

## Notes

- 高 APY（>100%）往往伴随高风险，需重点检查 TVL 和安全记录
- 稳定币策略优先推荐 TVL > $50M 的知名协议
