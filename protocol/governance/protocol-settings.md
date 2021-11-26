# Protocol Settings

Below is a short list of protocol settings that are managed by the governance process:

| Setting             | Description                                                                                                             |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| minShareForProposal | Minimum share of the total governance tokens supply for being able to submit a proposal                                 |
| debtInterestRate    | Interest rate charged to outstanding debts by the "CreditProvider" contract                                             |
| creditInterestRate  | Interest rate applied to credit tokens balances                                                                         |
| processingFee       | Options cash settling fee charged by the "CreditProvider" contract                                                      |
| volatilityPeriod    | Period in days for calculating the onchain volatility of underlying assets, required in the collateral allocation model |

The list of accepted stablecoins is also stored in the protocol settings contract along with each stablecoin conversion parameters, for converting values to the protocol's decimals base ("18" decimals).
