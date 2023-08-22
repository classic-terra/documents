# Core v2.2.0 migration guide

## Frontend

| removed endpoints                           | substituted endpoints                                               |
| ------------------------------------------- | ------------------------------------------------------------------- |
| /txs/estimate_fee                           | /terra/tx/v1beta1/compute_tax                                       |
| /txs/encode                                 |                                                                     |
| /txs                                        | /cosmos/tx/v1beta1/txs                                              |
| /bank/accounts/{address}/transfers          | MsgSend -> /cosmos/tx/v1beta1/txs                                   |
| /wasm/contract/{contractAddr}/admin         | MsgUpdateAdmin -> /cosmos/tx/v1beta1/txs                            |
| /wasm/contract/{contractAddr}/code          | MsgMigrateContract -> /cosmos/tx/v1beta1/txs                        |
| /wasm/code (GET)                            | /cosmwasm/wasm/v1/code                                              |
| /wasm/code/{codeID}                         | /cosmwasm/wasm/v1/code/{code_id}                                    |
| /wasm/code/{codeID}/contracts               | /cosmwasm/wasm/v1/code/{code_id}/contracts                          |
| /wasm/contract/{contractAddr}               | /cosmwasm/wasm/v1/contract/{address}                                |
| /wasm/contract/{contractAddr}/state         | /cosmwasm/wasm/v1/contract/{address}/state                          |
| /wasm/contract/{contractAddr}/history       | /cosmwasm/wasm/v1/contract/{address}/history                        |
| /wasm/contract/{contractAddr}/smart/{query} | /cosmwasm/wasm/v1/contract/{address}/smart/{query_data}             |
| /wasm/contract/{contractAddr}/raw/{key}     | /cosmwasm/wasm/v1/contract/{address}/raw/{query_data}               |
| /wasm/code (POST)                           | MsgStoreCode -> /cosmos/tx/v1beta1/txs                              |
| /wasm/code/{codeId} (POST)                  | MsgInstantiateContract -> /cosmos/tx/v1beta1/txs                    |
| /wasm/contract/{contractAddr}               | MsgExecuteContract -> /cosmos/tx/v1beta1/txs                        |
| /market/swap (GET)                          | /terra/market/v1beta1/swap                                          |
| /market/terra_pool_delta                    | /terra/market/v1beta1/terra_pool_delta                              |
| /market/parameters                          | /terra/market/v1beta1/params                                        |
| /market/swap (POST)                         | MsgSwap, MsgSwapSend -> /cosmos/tx/v1beta1/txs                      |
| /oracle/denoms/{%s}/exchange_rate           | /terra/oracle/v1beta1/denoms/{denom}/exchange_rate                  |
| /oracle/denoms/{%s}/tobin_tax               | /terra/oracle/v1beta1/denoms/{denom}/tobin_tax                      |
| /oracle/denoms/actives                      | /terra/oracle/v1beta1/denoms/actives                                |
| /oracle/denoms/exchange_rates               | /terra/oracle/v1beta1/denoms/exchange_rates                         |
| /oracle/denoms/vote_targets                 | /terra/oracle/v1beta1/denoms/vote_targets                           |
| /oracle/denoms/tobin_taxes                  | /terra/oracle/v1beta1/denoms/tobin_taxes                            |
| /oracle/voters/{%s}/feeder                  | /terra/oracle/v1beta1/validators/{validator_addr}/feeder            |
| /oracle/voters/{%s}/miss                    | /terra/oracle/v1beta1/validators/{validator_addr}/miss              |
| /oracle/voters/{%s}/aggregate_prevote       | /terra/oracle/v1beta1/validators/{validator_addr}/aggregate_prevote |
| /oracle/voters/{%s}/aggregate_vote          | /terra/oracle/v1beta1/valdiators/{validator_addr}/aggregate_vote    |
| /oracle/voters/aggregate_prevotes           | /terra/oracle/v1beta1/validators/aggregate_prevotes                 |
| /oracle/voters/aggregate_votes              | /terra/oracle/v1beta1/validators/aggregate_votes                    |
| /oracle/parameters                          | /terra/oracle/v1beta1/params                                        |
| /oracle/voters/{%s}/feeder                  | MsgDelegateFeedConsent -> /cosmos/tx/v1beta1/txs                    |
| /oracle/voters/{%s}/aggregate_prevote       | MsgAggregateExchangeRatePrevote -> /cosmos/tx/v1beta1/txs           |
| /oracle/voters/{%s}/aggregate_vote          | MsgAggregateExchangeRateVote -> /cosmos/tx/v1beta1/txs              |
| /treasury/tax_rate                          | /terra/treasury/v1beta1/tax_rate                                    |
| /treasury/tax_cap/{%s}                      | /terra/treasury/v1beta1/tax_caps/{denom}                            |
| /treasury/tax_caps                          | /terra/treasury/v1beta1/tax_caps                                    |
| /treasury/reward_weight                     | /terra/treasury/v1beta1/reward_weight                               |
| /treasury/tax_proceeds                      | /terra/treasury/v1beta1/tax_proceeds                                |
| /treasury/seigniorage_proceeds              | /terra/treasury/v1beta1/seigniorage_proceeds                        |
| /treasury/parameters                        | /terra/treasury/v1beta1/params                                      |
| /treasury/indicators                        | /terra/treasury/v1beta1/indicators                                  |
| /treasury/burn_tax_exemption_list           | /terra/treasury/v1beta1/burn_tax_exemption_list                     |
| /node_info                                  | /cosmos/base/tendermint/v1beta1/node_info                           |

## CosmWasm
1. Enable StargateQuerier which allows DApps to query from Terra Classic without the need to declare *`<TerraQuery>`*. This will allow greater compatibility with `Deps<Empty>` and cw-multi-test.

	Please refer to: https://github.com/classic-terra/classic-bindings/blob/main/contracts/stargate-tester/README.md for usage example

	The feature is available on classic-bindings >= 0.2.0: https://crates.io/crates/classic-bindings/0.2.0

2. Include FundCommunityPool for Distribution Msg. The feature is available on cosmwasm-std >= 1.3.0 (https://crates.io/crates/cosmwasm-std/1.3.0)