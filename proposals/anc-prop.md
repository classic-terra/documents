## What is Anchor Protocol?

Anchor Protocol is a well-known lending/borrowing application on the Terra Blockchain. Since the crash in May '22 the protocol is not maintained anymore by it's original owners. Due to the latest WASM upgrade most of the contracts of the protocol are not even usable anymore. The protocols governance token used to be listed under the symbol ANC. Information about the ANC token contract can be found on the official documentation, which is still hosted:

- https://docs.anchorprotocol.com/anchor-2/smart-contracts/deployed-contracts#cw20-compliant-token-contracts-4

## Why is it Bothering Us?

Despite Anchor Protocol not being used/maintained anymore many users of the Terra Classic blockchain own, use or trade ANC tokens and some exchanges have ANC still listed (one of which is Binance). After the upgrade the interface of the contract cannot be used anymore - which is of course very inconvenient for users and exchanges.

According to the Anchor Protocol README documentation [(here)](https://github.com/Anchor-Protocol/anchor-token-contracts/blob/main/README.md) the code for the ANC token was/is the original Terraswap Token CW20 implementation. Information about the CW20 token implementation from Terraswap can be found in this GitHub repository:

- https://github.com/terraswap/classic-terraswap/tree/main/contracts/terraswap_token

In the above repository you'll notice that the Terraswap project maintainers updated their CW20 token contract implementation to be compatible with the newer version of the on-chain WASM engine (commit hash 7839ad189d5990b5d6e77987f94610fa08e58cd3). The Terraswap team deployed the new code for their CW20 implementation at Code ID 6036 (reade (here)[https://docs.terraswap.io/docs/resources/contract-addresses/#columbus-5-mainnet]

## Proposal

This
