# Augmento Market Indicator — Backtest

Backtest notebooks for [Augmento](https://augmento.ai) market indicators — sentiment-based trading signals for crypto assets.

## Fusion V1 (Bitcoin)

**[fusion_v1_backtest.ipynb](fusion_v1_backtest.ipynb)** — Full backtest of the Fusion V1 indicator on BTC/USDT.

The strategy is simple: **long BTC** when the indicator is bullish, **cash** when neutral. Signals are fetched from the free Augmento API and executed at 01:00 UTC (35 minutes after signal availability). No API key required.

### What's inside

- Signal ingestion from the [Augmento API](https://augmento.ai/api-access)
- Hourly BTC/USDT price data from the Binance public API
- Proper execution timing with no look-ahead bias
- Full [quantstats](https://github.com/ranaroussi/quantstats) tear sheet (50+ metrics, equity curves, drawdowns, monthly heatmaps)
- Annual comparison table: strategy vs buy & hold (returns, Sharpe, max drawdown)
- Signal quality analysis (win rate, avg holding period, return by regime)

### Quick start

```bash
pip install quantstats requests pandas numpy
jupyter notebook fusion_v1_backtest.ipynb
```

Run all cells. The notebook fetches data automatically and caches it locally for faster re-runs.

### Configuration

At the top of the notebook:

| Variable | Default | Description |
|----------|---------|-------------|
| `AUGMENTO_API_KEY` | `"free"` | API key for real-time data, or `"free"` for delayed public access |
| `USE_CACHED_DATA` | `True` | Cache fetched data to CSV for faster subsequent runs |
| `START_DATE` | `"2018-01-01"` | Backtest start date |

### Signal timing

| Step | Time (UTC) | Description |
|------|-----------|-------------|
| Signal available | T+1, 00:25 | Market indicator for day T available via API |
| Execution | T+1, 01:00 | Enter/exit at open of the 01:00 UTC candle |

Returns are measured between consecutive 01:00 UTC execution prices.

## Data Sources

| Source | Endpoint | Auth |
|--------|----------|------|
| Augmento Market Indicator | `GET https://augmento.ai/api/v1/market-indicator/1` | Free (public) |
| Binance BTC/USDT Klines | `GET https://api.binance.com/api/v3/klines` | None (public) |

## Links

- [Augmento](https://augmento.ai) — Crypto Sentiment Intelligence
- [API Documentation](https://augmento.ai/api-access) — Endpoints, authentication, rate limits
- [quantstats](https://github.com/ranaroussi/quantstats) — Portfolio analytics library

## Disclaimer

This repository is for **informational and educational purposes only**. It does not constitute financial advice. Past performance is not indicative of future results. Always do your own research before making investment decisions.

## License

MIT
