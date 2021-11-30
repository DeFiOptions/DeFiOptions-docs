# Making a deposit

In order to make a deposit first approve a compatible stablecoin allowance for the exchange on the amount you wish to deposit, then call the exchange's `depositTokens` function:

```
ERC20 stablecoin = ERC20(0x123...);
OptionsExchange exchange = OptionsExchange(0xABC...);

address to = 0x456...;
uint value = 100e18;
stablecoin.approve(address(exchange), value);
exchange.depositTokens(to, address(stablecoin), value);
```

_Obs: An_ [_EIP-2612 compatible_](https://eips.ethereum.org/EIPS/eip-2612) _ `depositTokens` function is also provided for deposit functions in a single transaction._

After the operation completes check total exchange balance for an address using the `balanceOf` function:

```
address owner = 0x456...;
uint balance = exchange.balanceOf(owner);
```

Balance is returned in dollars considering 18 decimal places.

In case you wish to withdraw funds (ex: profits from an operation) call the `withdrawTokens` function:

```
uint value = 50e18;
exchange.withdrawTokens(value);
```

The function will transfer stablecoin tokens to the `msg.sender` for the requested amount, provided that the caller has enough unallocated balance. Since the exchange accepts multiple stablecoins the withdrawer should expect to receive any of these tokens.

_Obs: If there aren't enough stablecoins available in the exchange the solicitant will receive ERC20 credit tokens issued by the credit provider contract which can later be redeemed for stablecoins at a 1:1 value conversion ratio._

\
