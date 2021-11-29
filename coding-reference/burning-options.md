# Burning options

he exchange keeps track of all option writers and holders. Option writers are addresses that create option tokens. Option holders in turn are addresses to whom option tokens are transferred to. On calling the `writeOptions` exchange function an address becomes both writer and holder of the newly issued option tokens, until it decides to transfer them to a third-party.

In order to burn options, for instance to close a position before maturity and release allocated collateral, writers can call the `burn` function from the option token contract:

```
OptionToken token = OptionToken(tokenAddress);
uint amount = 5 * volumeBase;
token.burn(amount);
```

The calling address must be both writer and holder of the specified volume of options that are to be burned, otherwise the function will revert. If the calling address happens to be short biased (written volume > held volume) it will have to purchase option tokens in the market up to the volume it wishes to burn.

#### Underlying feeds

Both the `calcCollateral` and the `writeOptions` exchange functions receive the address of the option underlying price feed contract as a parameter. The feed contract implements the following interface:

```
interface UnderlyingFeed {

    function symbol() external view returns (string memory);

    function getLatestPrice() external view returns (uint timestamp, int price);

    function getPrice(uint position) external view returns (uint timestamp, int price);

    function getDailyVolatility(uint timespan) external view returns (uint vol);

    function calcLowerVolatility(uint vol) external view returns (uint lowerVol);

    function calcUpperVolatility(uint vol) external view returns (uint upperVol);
}
```

The exchange depends on these functions to calculate options intrinsic value, collateral requirements and to liquidate positions.

* The `symbol` function is used to create option token contracts identifiers, such as `ETH/USD-EC-13e20-1611964800` which represents an ETH european call option with strike price US$ 1300 and maturity at timestamp `1611964800`.
* The `getLatestPrice` function retrieves the latest quote for the option underlying, for calculating its intrinsic value.
* The `getPrice` function on the other hand retrieves the first price for the underlying registered in the blockchain after a specific timestamp position, and is used to liquidate the option token contract at maturity.
* The `getDailyVolatility` function is used to calculate collateral requirements as described in the [collateral allocation](https://github.com/DeFiOptions/DeFiOptions-core#collateral-allocation) section.
* The `calcLowerVolatility` and `calcUpperVolatility` apply, respectively, the klower and kupper constants to the volatility passed as a parameter, also used for calculating collateral requirements, and for liquidating positions as well.

This repository provides a [Chainlink](https://chain.link) based implementation of the `UnderlyingFeed` interface which allows any Chainlink USD fiat paired currency (ex: ETH, BTC, LINK, EUR) to be used as underlying for issuing options:

* [contracts/feeds/ChainlinkFeed.sol](https://github.com/DeFiOptions/DeFiOptions-core/blob/master/contracts/feeds/ChainlinkFeed.sol)

Notice that this implementation provides prefetching functions (`prefetchSample`, `prefetchDailyPrice` and `prefetchDailyVolatility`) which should be called periodically and are used to lock-in underlying prices for liquidation and to optimize gas usage while performing volatility calculations.
