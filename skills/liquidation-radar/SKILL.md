---
name: liquidation-radar
description: Monitors futures liquidation risks including liquidation heatmaps, recent liquidations, and key price levels where mass liquidations would occur. Invoke when user asks about liquidation risks, forced selling, or dangerous price levels.
---

# Liquidation Radar

## Trigger Conditions

Invoke when user says:
- "现在有什么爆仓风险"
- "哪个价位会触发大量爆仓"
- "最近爆仓了多少"
- "多头 / 空头爆仓情况"
- "清算 / 强平 风险"
- "杠杆风险分析"

## Steps

1. **爆仓热力图** — 价格移动会在哪里触发大量爆仓
   ```
   ant_futures_liquidation(query_type="futures_liquidation_heatmap", symbol="BTC", range="24h", model=1)
   ```

2. **聚合爆仓地图** — 各价位的爆仓密集区
   ```
   ant_futures_liquidation(query_type="futures_liquidation_aggregated_map", symbol="BTC", range="1d")
   ```

3. **近期爆仓历史** — 实际发生了多少
   ```
   ant_futures_liquidation(query_type="futures_liquidation_aggregated", symbol="BTC", interval="1h", limit=24)
   ```

4. **各交易所爆仓排行** — 哪个交易所最危险
   ```
   ant_futures_liquidation(query_type="futures_liquidation_exchange_list", symbol="BTC", range="24h")
   ```

5. **当前 OI 与杠杆水平**
   ```
   ant_futures_market_structure(query_type="futures_oi_aggregated", symbol="BTC", interval="1h", limit=1)
   ```

6. **资金费率** — 过高的资金费率意味着市场过度杠杆
   ```
   ant_futures_market_structure(query_type="futures_funding_rate_oi_weight", symbol="BTC", interval="1h", limit=1)
   ```

## Output Format

```
## BTC 爆仓雷达

**关键爆仓价位：**
- 上方爆仓密集区（空头）：$xxx,xxx — $xxx,xxx（预计 $xxxM 空头）
- 下方爆仓密集区（多头）：$xxx,xxx — $xxx,xxx（预计 $xxxM 多头）

**近24小时爆仓统计：**
- 多头爆仓：$xxxM
- 空头爆仓：$xxxM
- 最大单笔：$xxxM on [交易所]

**当前杠杆风险：**
- 总 OI：$xxxB
- 资金费率：x.xxx%（[正常/偏高/危险]）

**风险等级：** 🔴 高 / 🟡 中 / 🟢 低

**警示：**
[如果资金费率过高或OI异常，给出具体警示；说明最危险的价位和方向]
```

## Notes

- 默认分析 BTC，如用户指定 ETH 等，修改 symbol 参数
- 资金费率 > 0.1% 或 < -0.05% 视为偏高，需特别提示
