# Collateral Allocation

The options exchange requires options writers to provide collateral for writing options, for making sure writers will be able to cover financial obligations once options mature, and not simply default on payments.

All open positions owned by an address (written or held) are taken into account for allocating collateral regardless of the underlying, option type and maturity, according to the following formula implemented in solidity code:

![](../.gitbook/assets/collateral-formula.svg)

A short position "i" increases required collateral proportionally to the written volume taking into account the period adjusted on-chain historical underlying price volatility and the option intrinsic value ("υ"). A long position "j" decreases required collateral proportionally to the held volume taking into account the option intrinsic value alone. The k-upper constant plays a role in the liquidation process and serves as an additional security factor protecting against the inherent uncertainty of the underlying price volatility (i.e. the volatility-of-volatility risk).
