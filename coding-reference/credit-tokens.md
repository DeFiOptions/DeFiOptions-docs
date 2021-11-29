# Credit tokens

A [credit token](https://github.com/DeFiOptions/DeFiOptions-core/blob/master/contracts/finance/CreditToken.sol) can be viewed as a proxy for any of the exchange's compatible stablecoin tokens, since it can be redeemed for the stablecoin at a 1:1 value conversion ratio. In this sense the credit token is also a stablecoin, one with less liquidity nonetheless.

Credit tokens are issued when there aren't enough stablecoin tokens available in the exchange to cover a withdraw operation. Holders of credit tokens receive interest on their balance (hourly accrued) to compensate for the time they have to wait to finally redeem (burn) these credit tokens for stablecoins once the exchange ensures funds again. To redeem credit tokens call the `requestWithdraw` function, and expect to receive the requested value in any of the exchange's compatible stablecoin tokens:

```
CreditToken ct = CreditToken(0xABC...);
ct.requestWithdraw(value);
```

In case there aren't sufficient stablecoin tokens available to fulfil the request it'll be FIFO-queued for processing when the exchange ensures enough funds.

The exchange will ensure funds for burning credit tokens when debtors repay their debts (for instance when an option token contract is liquidated and the debtor receives profits, which are instantly discounted for pending debts before becoming available to the debtor) or through options settlement processing fees, which by default are not charged, but can be configured upon demand.
