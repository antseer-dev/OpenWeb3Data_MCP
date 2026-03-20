---
name: macro-crypto-outlook
description: Analyzes macro economic indicators and their impact on crypto markets, including Fed policy, ETF flows, treasury yields, and institutional adoption. Invoke when user asks about macro factors affecting crypto.
---

# Macro Crypto Outlook

## Trigger Conditions

Invoke when user says:
- "宏观对加密有什么影响"
- "美联储 / 降息 / 加息 对 BTC 的影响"
- "ETF 资金流情况"
- "通胀数据 / CPI 出来了，对加密怎么看"
- "机构在买 BTC 吗"
- "美股和加密的关系"

## Steps

1. **美联储利率** — 当前货币政策环境
   ```
   ant_macro_economics(query_type="federal_funds_rate", interval="monthly")
   ```

2. **通胀数据** — CPI 趋势
   ```
   ant_macro_economics(query_type="cpi", interval="monthly")
   ```

3. **国债收益率** — 无风险利率（影响风险资产估值）
   ```
   ant_macro_economics(query_type="treasury_yield", interval="monthly", maturity="10year")
   ```

4. **BTC ETF 资金流** — 机构实际入场情况
   ```
   ant_etf_fund_flow(query_type="btc_etf_flow", limit=30)
   ant_etf_fund_flow(query_type="btc_etf_aum")
   ```

5. **ETH ETF 资金流**
   ```
   ant_etf_fund_flow(query_type="eth_etf_flow", limit=7)
   ```

6. **灰度溢价/折价** — 机构情绪温度计
   ```
   ant_etf_fund_flow(query_type="grayscale_premium", symbol="BTC")
   ```

7. **公司持仓** — 上市公司 BTC 持仓
   ```
   ant_spot_market_structure(query_type="companies_public_treasury", coin_id="bitcoin")
   ```

## Output Format

```
## 宏观加密展望

**货币政策环境：**
- 当前联邦基金利率：x.xx%（上升/下降/持平趋势）
- CPI 最新：x.x%（通胀压力：高/中/低）
- 10年国债收益率：x.xx%

**宏观对加密影响评级：**
🟢 利好 / 🟡 中性 / 🔴 利空

**机构资金动向：**
- BTC ETF 近7日净流入：+$xxxM / 净流出：-$xxxM
- BTC ETF 总 AUM：$xxxB
- ETH ETF 近7日：+/-$xxxM
- 灰度 GBTC 溢价/折价：x.xx%

**企业持仓：**
- 上市公司共持有 xxx BTC（$xxxB）

**综合判断：**
[当前宏观环境对加密市场的整体影响分析，2-3句话]
```
