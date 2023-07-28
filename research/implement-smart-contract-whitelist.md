# Smart Contract Whitelist Concept

The Terra Classic community expresses its whish to whitelist smart contract execution from the on-chain burn tax. The orignal discussion can be found [here](https://classic-agora.terra.money/t/new-economic-policy-for-terra-classic-set-of-4-proposals-to-align-incentives/50415). The proposal passed as on-chain governance proposal 11516.

After conversation with dfunk - who initially brought up the smart contract whitelist proposal - the following behavior needs to be implemented:

- Smart contract addresses can be whitelisted via on-chain gov proposal (this is already possible using the so called "Binance Whitelist")
- If smart contracts are whitelisted, then users of thesese contracts don't pay taxes to execute `MsgExecuteContract` on them.
- The whitelisted contracts themselves are NOT whitelisted from tax. It's solely the user invocation that is exempted.

Example: Let's assume we have a smart contract which accepts a `MsgExecuteContract` message. This type of message can carry along a given amount of coins that the users assigns to it. The contract will be implemented such that it receives the coins and forwards the received amount to another account. Let's say the user executes the contract and sends along 100,000 LUNC to be send to another account. Given the above mentioned requirements two things will happen:

- The user executes the contract using `MsgExecuteContract` and puts 100,000 LUNC into the execution message. If the contract is NOT whitelisted, then the user will have to pay 500 LUNC in taxes to execute the contract (+ gas fees). However, if the contract is whitelisted, then the user will pay ONLY gas fees, but NO taxes.
- During contract execution the contract gets the amount of coins and executes `MsgSend` to forward the received amounts to the other account. No matter whether the contract is whitelisted or not: The blockchain will deduct 500 LUNC from its contract balance to execute the `MsgSend`.

## Reuse of Binance Whitelist

In order to implement this feature as efficiently as possible I propose to reuse main parts of the Binance Whitelist logic. The Binance Whitelist is a governance parameter in the treasury module and it exempts certain addresses from the burn tax using logic in the ante handler. The whitelist can be extended (or shortened) by putting up single addresses (or list of addresses) up for governance vote.

However, the important difference between the original Binance Whitelist feature and the feature proposed by 11516 is that the Binance Whitelist applies only for p2p (`MsgSend`) transfers between addresses that are part of the list whereas the 11516 whitelist would apply for executes (`MsgExecuteContract`) on the contract addresses.

Currently the treasury keeper contains a Method `HasBurntaxExemptionAddr(addresses ...string)` which checks whether a list of addresses contains only whitelisted addresses. If one of the addresses is not in the whitelist, the method returns false. If all addresses are in the whitelist, it returns true. Gladly, this function can be reused.

## Introducing `HasBurntaxExemptionAddrSmart()`

I propose to add the `HasBurntaxExemptionAddrSmart(address string)` method to the treasury keeper with the following logic:

- Check whether the input address is a contract address by calling `GetContractAddressKey(address)` from the wasm module
- If the address key is nil, the input address is not a smart contract address, return false
- If the address key is not nil, then the input address is a smart contract, proceed
- Return the result of `HasBurnTaxExemptionAddr(address)`

This function would then be used in the corresponding ante handler (specifically in the funtion `FilterMsgsAndComputeTax()`). The proposed logic:

- Check whether the given Message is a `MsgExecuteContract`
- Check the execution address (the contract address) using `HasBurntaxExemptionAddrSmart()`
- If `HasBurntaxExemptionAddrSmart()` returns `false`, then deduct tax from the transaction and continue
- Otherwise don't deduct tax from the transaction and continue

## Disclaimer

Note that this feature is consensus breaking and needs coordinated chain halt to be introduced. However, with the above given approach a store migration is not required.
