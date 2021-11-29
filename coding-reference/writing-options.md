# Writing options

Before writing an option calculate the amount of collateral needed by calling the `calcCollateral` function providing the option parameters:

```
address eth_usd_feed = address(0x987...);
uint volumeBase = 1e18;
uint strikePrice = 1300e18;
uint maturity = now + 30 days;

uint collateral = exchange.calcCollateral(
    eth_usd_feed, 
    10 * volumeBase, 
    OptionsExchange.OptionType.CALL, 
    strikePrice, 
    maturity
);
```

The snippet above calculates the collateral needed for writing ten ETH call options at the strike price of US$ 1300 per ETH maturing in 30 days from the current date.

After checking that the writer has enough unallocated balance to provide as collateral, proceed to write options by calling the `writeOptions` function:

```
address holder = 0xDEF...;

address tkAddr = exchange.writeOptions(
    eth_usd_feed, 
    10 * volumeBase, 
    OptionsExchange.OptionType.CALL, 
    strikePrice, 
    maturity,
    holder
);
```

Options are issued as ERC20 tokens and sent to the specified `holder` address. The `writeOptions` function returns the option token contract address for convenience:

```
ERC20 token = ERC20(tkAddr);
uint balance = token.balanceOf(holder); // equal to written volume

address to = 0x567...;
token.transfer(to, 5 * volumeBase); // considering 'msg.sender == owner'
```

Options are aggregated by their underlying, strike price and maturity, each of which will resolve to a specific ERC20 token contract address. Take advantage of already existent option token contracts when writing options for increased liquidity.

The `calcIntrinsicValue` allows callers to check the updated intrinsict value for an option, specified by its token contract address `tkAddr`:

```
uint iv = exchange.calcIntrinsicValue(tkAddr);
```

Suppose the ETH price has gone up to US$ 1400, and considering that the strike price was set to US$ 1300, then the intrinsic value returned would be `100e18`, i.e., US$ 100. Multiply this value by the held volume to obtain the position's aggregated intrinsic value.
