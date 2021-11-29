# Liquidating positions

Options can be liquidated either individually due to a writer not meeting collateral requirements for covering his open positions, or collectively at the option token contract level upon maturity.

In the first case, when a writer doesn't meet the collateral requirements for covering his open positions, any of his positions will be susceptible to liquidation for reducing liabilities until the writer starts meeting collateral requirements again.

To liquidate a specific writer option in this situation call the `liquidateOptions` function providing both the option token contract address and the writer address:

```
uint value = exchange.liquidateOptions(tkAddr, owner);
```

The function returns the value resulting from liquidating the position (either partially or fully), which is transferred to the respective option token contract and held until maturity, whereupon the contract is fully liquidated and profits are distributed to option holders proportionally to their share of the total supply.

The effective volume liquidated by this function call is calculated using the minimum required volume for the writer to start meeting the collateral requirements again:

![](../.gitbook/assets/early-liq-volume.svg)

Here two constants are employed, kupper and klower, whose difference enables the clearance of the collateral deficit in a simple manner. Once the liquidation volume is found, the liquidation value is calculated as:

![](../.gitbook/assets/early-liq-value.svg)

Now in the second case, when the option matures, all option token contract written positions can be liquidated for their intrinsic value. The exchange offers a function overload that accpets an array of options writers addresses for liquidating their positions in a more gas usage efficient way:

```
address[] memory owners = new address[](length);
// initialize array (...)
exchange.liquidateOptions(tkAddr, owners);
```

Liquidated options are cash settled by the credit provider contract and the accumulated capital becomes available for redemption among option holders proportionally to their share of the total token supply:

```
OptionToken optionToken = OptionToken(tkAddr);
optionToken.redeem(holder);
```

In case any option writer happens to be short on funds during settlement the credit provider will register a debt and cover payment obligations, essentially performing a lending operation.
