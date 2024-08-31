# Crypto Funding Rate Arbitrage Scanner
*A funding rate arbitrage bot created to scan crypto markets for changes in premiums across exchanges, looking for arbitrage trades. Can be used for educational purposes or as part of your own funding rate arbitrage system. Built in TypeScript, based on our Crypto Market Scanner.*

---

### Usage (WIP)
**Note: this bot does not manage arbitrage trades on its own, only locates opportunities to do so. Use your own orderbook manager (Complete arbitrage bot with order management coming Q1 2025)**

Supply a list of supported exchanges and markets to the constructor to initialize.
```js
import { FundingArbitrageScanner } from 'funding-arbitrage-scanner';
const exchanges = ['binance', 'kucoin'];
const markets = ['BTC-USDT', 'KAS-USDT'];
const Scanner = new FundingArbitrageScanner(exchanges, markets);
```

Starting the scan involves two parts:
1) Fetching latest market data from input markets. This could take a couple of seconds or more depending on workload.
2) Comparing markets across the result dataset to look for combinations of hedged market orders on different exchanges that have a positive net funding rate. This is potentially a resource intensive task depending on dataset size. *(Initially a simple brute-force reduction of the dataset will be used, but more complex search algorithms may be added if needed.)*
This process returns a list of all possible combined funding rates in `results.all`, with positive results in `results.profitable` - you can opt to reduce the resulting dataset by filtering out non-profitable results.
```js
const profitableOnly = false;
const data = await Scanner.getMarketData();
const results = await Scanner.getArbitragePairs(profitableOnly);

// Results
{
  'all': [
            {
              'market': 'KAS-USDT',
              'long': 'binance',
              'short': 'kucoin',
              'premium': -0.001
            },
            ...
        ],
    'profitable': [...]
}
```
You can save these results for later analysis or pass them to your own orderbook manager bot to create orders. Alternatively, you can use our full **Funding Rate Arbitrage Bot (Coming Q1 2025)** if you need order management functionality but don't have your own.
