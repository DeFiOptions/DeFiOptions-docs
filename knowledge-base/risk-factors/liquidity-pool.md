# Liquidity Pool

Becoming a liquidity provider by depositing funds in a liquidity pool that writes and sells options is **exceptionally risky**, and you shouldn't in any circumstance deposit more funds in a pool than you're willing to lose completely.

As we've seen in the Risk Factors [options.md](options.md "mention") page, call/put writers take the highest amounts of risk in the context of options trading, and in a sense the pool acts as a crowdfunded options writer agent. Liquidity providers then are exposed to the same risk profile as the liquidity pool, proportional to their stake in the pool.

In addition to the aforementioned risks of trading options liquidity providers are also subject to risks related to:

* **Pricing Model Performance**: The pool prices options according to a specific pricing model, determined by the pool operator. If the pricing model prices options too cheap then the liquidity pool will, on average, lose money.
* **Smart Contract Vulnerabilities**: The liquidity pool smart contract is decoupled from the options exchange. It has been audited by PeckShield, along with all other protocol contracts. Nonetheless it's particularly complex and hasn't been battle tested yet, so interact with it with caution.
