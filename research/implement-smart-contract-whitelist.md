# Smart Contract Whitelist Concept

The Terra Classic community expresses its whish to whitelist smart contract execution from the on-chain burn tax. The orignal discussion can be found [here](https://classic-agora.terra.money/t/new-economic-policy-for-terra-classic-set-of-4-proposals-to-align-incentives/50415). The proposal passed as on-chain governance proposal 11516.

## Reuse of Binance Whitelist

In order to implement this feature as efficiently as possible I propose to reuse main parts of the Binance Whitelist logic for this feature. The Binance Whitelist is a governance parameter in the treasury module and it exempts certain addresses from the burn tax using logic in the ante handler. The whitelist can be extended (or shortened) by putting up single addresses (or list of addresses) up for governance vote.

However, the important difference between the original Binance Whitelist feature and the feature proposed by 11516 is that the Binance Whitelist applies only for p2p (`MsgSend`) transfers between addresses that are part of the list whereas the 11516 Whitelist would apply for executes (`MsgExecuteContract`) on the contract addresses.

Currently the treasury keeper contains a Method `HasBurntaxExemptionAddr(addresses ...string)` which checks whether a list of addresses contains only whitelisted addresses. If one of the addresses is not in the whitelist, the method returns false. If all addresses are in the whitelist, it returns true. Gladly, this function can be reused.

## Introducing `HasBurntaxExemptionAddrSmart()`

I propose to add the `HasBurntaxExemptionAddrSmart(address string)` method to the treasury keeper with the following logic:

- Check whether the input address is a contract address by calling `GetContractAddressKey(address)` from the wasm module
- If the address key is nil, the input address is not a smart contract address, return false
- If the address key is not nil, then the input address is a smart contract, proceed
- Return the result of `HasBurnTaxExemptionAddr(address)`

This function would then be used in the corresponding ante handler (specifically in the funtion `FilterMsgsAndComputeTax()`).

## Edge Case

The above mentioned concept is the most efficient I can think of in terms of "amount of coding and changes in the underlying param store". However, the concept has one rare edge case: If the community decides to whitelist execution on two different smart contract addresses then these two smart contracts are *automatically* "binance whitelisted" for `MsgSend` between those two.

## Disclaimer

Note that this feature is consensus breaking and needs coordinated chain halt to be introduced. However, with the above given approach a store migration is not required.
