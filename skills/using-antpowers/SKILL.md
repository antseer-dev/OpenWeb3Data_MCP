---
name: using-antpowers
description: Activated at session start. Teaches Claude about all antpowers crypto analysis skills and when to invoke them. If a skill applies, it MUST be used — no exceptions.
---

<EXTREMELY-IMPORTANT>
If there is even a 1% chance a skill applies to what you are doing, YOU MUST invoke it with the Skill tool.

IF A SKILL APPLIES, YOU DO NOT HAVE A CHOICE. YOU MUST USE IT.
</EXTREMELY-IMPORTANT>

## What is Antpowers

Antpowers gives you structured crypto market analysis workflows powered by the **ansteer MCP** (19 on-chain and market data tools). Instead of calling tools ad-hoc, you invoke skills that encode proven analysis patterns.

## Available ansteer MCP Tools

**On-Chain:**
- `ant_smart_money` — smart money wallet tracking (netflows, holdings, DEX trades, perp trades)
- `ant_fund_flow` — exchange/miner/whale fund flows
- `ant_address_profile` — deep wallet profiling (balance, PnL, counterparties, labels)
- `ant_token_analytics` — token on-chain metrics, screener, holder analysis, DEX trades
- `ant_protocol_tvl_yields_revenue` — TVL, yields, fees, DEX volume by protocol
- `ant_protocol_ecosystem` — hacks, raises, oracles, treasuries
- `ant_stablecoin` — stablecoin market cap, chain distribution, dominance
- `ant_perp_dex` — on-chain perpetual DEX (Hyperliquid whale positions)
- `ant_bridge_fund_flow` — cross-chain bridge volumes and flows

**CeFi Markets:**
- `ant_spot_market_structure` — spot prices, OHLC, market cap rankings, trending
- `ant_futures_market_structure` — OI, funding rates, long/short ratio, orderbook, CVD
- `ant_futures_liquidation` — liquidation history, heatmap, liquidation map
- `ant_market_indicators` — RSI, MA, EMA, MACD, Bollinger, whale index

**Sentiment & Social:**
- `ant_market_sentiment` — Twitter/social topic posts, coin sentiment, creator tracking

**TradFi:**
- `ant_etf_fund_flow` — BTC/ETH ETF flows, AUM, premium/discount
- `ant_macro_economics` — GDP, CPI, Fed rate, treasury yields, unemployment
- `ant_us_stock_tokens` — tokenized US stocks (TSLAX, NVDAX, etc.)
- `ant_precious_metal_tokens` — gold/silver tokens (XAUT, PAXG)

**MEME:**
- `ant_meme` — trending meme tokens, boost rankings, CTO tracking, pair data

## Skill Trigger Map

| When user asks about... | Invoke skill |
|-------------------------|-------------|
| 聪明钱/smart money 在买什么、动向 | `antpowers:smart-money-analysis` |
| MEME/土狗/这个币能不能买、风险 | `antpowers:meme-risk-check` |
| 今天市场、行情总结、市场概览 | `antpowers:daily-market-briefing` |
| 鲸鱼、大户、巨鲸在动 | `antpowers:whale-alert-analysis` |
| 哪里有收益、DeFi yield、质押收益 | `antpowers:defi-yield-scout` |
| 研究某个代币、深度分析 token | `antpowers:token-deep-dive` |
| 宏观、美联储、ETF 对加密影响 | `antpowers:macro-crypto-outlook` |
| 爆仓、清算、强平风险 | `antpowers:liquidation-radar` |
| Solana/SOL 生态、链上动态、SOL 行情 | `antpowers:solana-ecosystem-pulse` |

## How to Use Skills

**In Claude Code:** Use the `Skill` tool with the skill name (e.g. `antpowers:smart-money-analysis`).

## Rules

1. **Always invoke the matching skill** before responding to any crypto analysis request
2. **Never call ansteer MCP tools ad-hoc** without a skill — skills ensure consistent, complete analysis
3. **Output must be human-readable** — never return raw JSON to the user
4. **If no skill matches**, use the tools directly but follow the output format: summary → key signals → recommendation

## Auto-Expanding

Run `/generate-skill` to mine Twitter signals and auto-generate new skills for emerging analysis needs.
