## What is Anchor Protocol?

Anchor Protocol is a well-known lending/borrowing application on the Terra Blockchain. Since the crash in May '22 the protocol is not maintained anymore by it's original owners. Due to the latest WASM upgrade most of the contracts of the protocol are not even usable anymore. The protocols governance token used to be listed under the symbol ANC. Information about the ANC token contract can be found on the official [documentation](https://docs.anchorprotocol.com/anchor-2/smart-contracts/deployed-contracts#cw20-compliant-token-contracts-4), which is still hosted:

## Why is it Bothering Us?

Despite Anchor Protocol not being used/maintained anymore many users of the Terra Classic blockchain own, use or trade ANC tokens and some exchanges have ANC still listed (one of which is Binance). After the upgrade the interface of the contract cannot be used anymore - which is of course very inconvenient for users and exchanges.

According to the Anchor Protocol README documentation [(here)](https://github.com/Anchor-Protocol/anchor-token-contracts/blob/main/README.md) the code for the ANC token was/is the original Terraswap Token CW20 implementation. Information about the CW20 token implementation from Terraswap can be found in this GitHub repository:

- https://github.com/terraswap/classic-terraswap/tree/main/contracts/terraswap_token

In the above repository you'll notice that the Terraswap project maintainers updated their CW20 token contract implementation to be compatible with the newer version of the on-chain WASM engine (commit hash 7839ad189d5990b5d6e77987f94610fa08e58cd3). The Terraswap team deployed the new code for their CW20 implementation at Code ID 6036 (read [here](https://docs.terraswap.io/docs/resources/contract-addresses/#columbus-5-mainnet))

## Proposal

This Proposal seeks community and validator approval for a contract migration of the ANC token contract (token address [terra14z56l0fp2lsf86zy3hty2z47ezkhnthtr9yq76](https://terra-classic-lcd.publicnode.com/cosmwasm/wasm/v1/contract/terra14z56l0fp2lsf86zy3hty2z47ezkhnthtr9yq76)). Upon passing of this proposal the original Code ID (currently sitting at [153](https://terra-classic-lcd.publicnode.com/cosmwasm/wasm/v1/code/153)) will be automatically replaced with the proposed Code ID [6036](https://terra-classic-lcd.publicnode.com/cosmwasm/wasm/v1/code/6036). The internal execution state of the contract will NOT be touched by this force upgrade.

## Opportunities and Risks

The purpose of this proposal is to make ANC holders liquid again. It is expected that after the upgrade the token is going to work as expected and users will be able to trade their assets again. However This is not an upgrade of *all* contracts that ran the entirety of Anchor Protocol. This means that there might be tokens that are locked in Anchor governance contracts. These contracts are *not* affected by this proposal. Affected tokens will still be locked after upgrading the token contract itself.

In addition to that the L1 team is proposing this force upgrade for the users convenience. We do not provide or maintain the code for the ANC token contract. We do not and/or did not issue ANC tokens at any time. The L1 team also does not possess ANC tokens and has no financial interest in pushing this proposal forward. We also did no research on whether the proposed token contract code is audited or not. However, the L1 teams assessment is that the proposed code is a standard CW20 token production grade implementation that is widely used by other CW20 tokens on the blockchain.

## Effects of Voting

Vote "yes" if you want the blockchain L1 protocol layer to automatically swap the old code for the ANC token contract and replace it with the above proposed code.

Vote "no" if you don't agree to this proposal and want to maintain the outdated code for the ANC token contract.
