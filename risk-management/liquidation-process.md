# Liquidation Process

Options can be liquidated either individually due to a writer not meeting collateral requirements for covering his open positions, or collectively at the option token contract level upon maturity.

In the first case, when a writer doesn't meet the collateral requirements for covering his open positions, any of his positions will be susceptible to early liquidation for reducing liabilities until the writer starts meeting collateral requirements again.

The effective volume susceptible to early liquidation is calculated using the minimum required volume for the writer to start meeting the collateral requirements again:

![](../.gitbook/assets/early-liq-volume.svg)

Here two constants are employed, k-upper and k-lower, whose difference enables the clearance of the collateral deficit in a simple manner. Once the liquidation volume is found, the liquidation value is calculated as:

![](../.gitbook/assets/early-liq-value.svg)

Funds from early liquidation are transferred to the respective option token contract and held until maturity.

Now in the second scenario, when the option token contract matures, all still active written options are liquidated, cash settled by the credit provider contract and the accumulated capital becomes available for redemption among option holders proportionally to their share of the total token supply. In case any option writer happens to be short on funds during settlement the credit provider will register a debt and cover payment obligations, essentially performing a lending operation.
