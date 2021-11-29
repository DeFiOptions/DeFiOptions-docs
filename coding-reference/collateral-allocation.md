# Collateral allocation

All open positions owned by an address (written or held) are taken into account for allocating collateral regardless of the underlying, option type and maturity, according to the following formula implemented in solidity code:

![](../.gitbook/assets/collateral-formula.svg)

A short position "i" increases required collateral proportionally to the written volume taking into account the period adjusted on-chain historical underlying price volatility and the option intrinsic value ("υ"). A long position "j" decreases required collateral proportionally to the held volume taking into account the option intrinsic value alone. The kupper constant plays a role in the liquidation process and serves as an additional security factor protecting against the inherent uncertainty of the underlying price volatility (i.e. the volatility-of-volatility risk).

Call the `calcCollateral` function to perform this calculation and obtain the collateral requirements for a specific address:

```
uint collateral = exchange.calcCollateral(owner);
```

The difference between the address balance and its collateral requirements is the address surplus. The `calcSurplus` function is conveniently provided to perform this calculation:

```
uint surplus = exchange.calcSurplus(owner);
```

The surplus effectively represents the amount of funds available for writing new options and for covering required collateral variations due to underlying price jumps. If it returns zero it means that the specified address is lacking enough collateral and at risk of having its positions liquidated.
