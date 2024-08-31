# Crypto Funding Rate Arbitrage Scanner
*A funding rate arbitrage bot created to scan crypto markets for changes in premiums across exchanges, looking for arbitrage trades. This bot cannot create trades on its own, only locates opportunities to do so. Can be used for educational purposes or as part of your own funding rate arbitrage system.*

---

### Usage (WIP)
Supply a list of supported exchanges and markets to the constructor to initialize.

Starting the scan involves two parts:
1) Fetching latest market data from input markets. This could take a couple of seconds or more depending on workload.
2) Comparing markets across the result dataset to look for combinations of hedged market orders on different exchanges that have a positive net funding rate. This is potentially a resource intensive task depending on dataset size. *(Initially a simple brute-force reduction of the dataset will be used, but more complex search algorithms may be added if needed.)*
This process returns a list of all possible combined funding rates in `results.all`, with positive results in `results.profitable`.

You can save these results for later analysis or pass them to your own orderbook manager bot to create orders. Alternatively, you can use our full **Funding Rate Arbitrage Bot (Coming Q1 2025)** if you need order management functionality but don't have your own.
