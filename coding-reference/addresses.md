# Addresses

### Polygon

DeFi Options has been deployed to Polygon mainnet. Find the verified contracts addresses in the table below:

| Contract                                                                                                                     | Address                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| [OptionsExchange](https://github.com/DeFiOptions/DeFiOptions-core/blob/master/contracts/finance/OptionsExchange.sol)         | [0x69b38e5cd783cbeeb06e11b4ad29a95af14dbcc9](https://polygonscan.com/address/0x69b38e5cd783cbeeb06e11b4ad29a95af14dbcc9) |
| [CreditToken](https://github.com/DeFiOptions/DeFiOptions-core/blob/master/contracts/finance/CreditToken.sol)                 | [0x045f70e2e63907000c0ff511862c936fc0857979](https://polygonscan.com/address/0x045f70e2e63907000c0ff511862c936fc0857979) |
| [Linear Liquidity Pool](https://github.com/DeFiOptions/DeFiOptions-core/blob/master/contracts/pools/LinearLiquidityPool.sol) | [0xa8353943cd1b9572d46ff927c8cfe89ba0b06b19](https://polygonscan.com/address/0xa8353943cd1b9572d46ff927c8cfe89ba0b06b19) |
| [ETH/USD feed](https://github.com/DeFiOptions/DeFiOptions-core/blob/master/contracts/interfaces/UnderlyingFeed.sol)          | [0xc6538cec5ca383217efe2c10b447d8d48453874a](https://polygonscan.com/address/0xc6538cec5ca383217efe2c10b447d8d48453874a) |
| [BTC/USD feed](https://github.com/DeFiOptions/DeFiOptions-core/blob/master/contracts/interfaces/UnderlyingFeed.sol)          | [0x2205c21d04adc4a9d6a5f55e76aec39010bb5e72](https://polygonscan.com/address/0x2205c21d04adc4a9d6a5f55e76aec39010bb5e72) |
| [MATIC/USD feed](https://github.com/DeFiOptions/DeFiOptions-core/blob/master/contracts/interfaces/UnderlyingFeed.sol)        | [0x822a5D26a5A8F881BF4C515E51cF00fC063C6C3C](https://polygonscan.com/address/0x822a5D26a5A8F881BF4C515E51cF00fC063C6C3C) |
| [SOL/USD feed](https://github.com/DeFiOptions/DeFiOptions-core/blob/master/contracts/interfaces/UnderlyingFeed.sol)          | [0x2863E94bEBa09F53888887F9d647bd406a593b43](https://polygonscan.com/address/0x2863E94bEBa09F53888887F9d647bd406a593b43) |

### Kovan

DeFi Options is available on kovan testnet for testing. Contract addresses are provided in the table below:

| Contract                                                                                                                     | Address                                                                                                                     |
| ---------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| [OptionsExchange](https://github.com/DeFiOptions/DeFiOptions-core/blob/master/contracts/finance/OptionsExchange.sol)         | [0x1233a9d9a02eef1bc24675332684d4bfdd866f8a](https://kovan.etherscan.io/address/0x1233a9d9a02eef1bc24675332684d4bfdd866f8a) |
| [CreditToken](https://github.com/DeFiOptions/DeFiOptions-core/blob/master/contracts/finance/CreditToken.sol)                 | [0xae7512c5d996b12830a282eeb9eecb4cf01207d2](https://kovan.etherscan.io/address/0xae7512c5d996b12830a282eeb9eecb4cf01207d2) |
| [Linear Liquidity Pool](https://github.com/DeFiOptions/DeFiOptions-core/blob/master/contracts/pools/LinearLiquidityPool.sol) | [0xb0be2a679632f028edb4a3e29bb82ac6ed6d84d9](https://kovan.etherscan.io/address/0xb0be2a679632f028edb4a3e29bb82ac6ed6d84d9) |
| [ETH/USD feed](https://github.com/DeFiOptions/DeFiOptions-core/blob/master/contracts/interfaces/UnderlyingFeed.sol)          | [0xF6DF43F27d51289703C2A93289D53C4D5AC79b7d](https://kovan.etherscan.io/address/0xF6DF43F27d51289703C2A93289D53C4D5AC79b7d) |
| [BTC/USD feed](https://github.com/DeFiOptions/DeFiOptions-core/blob/master/contracts/interfaces/UnderlyingFeed.sol)          | [0x261E05174813A0a6dafE208830410768b709E6ca](https://kovan.etherscan.io/address/0x261E05174813A0a6dafE208830410768b709E6ca) |
| [Fakecoin](https://github.com/DeFiOptions/DeFiOptions-core/blob/master/test/common/mock/ERC20Mock.sol)                       | [0xB51E93aA4B4B411A36De9343128299B483DBA133](https://kovan.etherscan.io/address/0xB51E93aA4B4B411A36De9343128299B483DBA133) |

A freely issuable ERC20 fake stablecoin ("fakecoin") is provided for convenience. Simply issue fakecoin tokens for an address you own to be able to interact with the exchange for depositing funds, writing options and evaluate its functionality:

```
ERC20Mock fakecoin = ERC20Mock(0xdd8...);
address to = 0xABC
uint value = 1500e18;
fakecoin.issue(to, value);
```
