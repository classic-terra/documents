
### Testnet Upgrade Guide

The L1 team is about to release the v2.0.0 of the terrad validator client software. The upgrade contains the bump to Cosmos-SDK v.0.45.x. This is a rather big upgrade the Terra Classic network is facing here. In order to be sure that the upgrade on the **columbus-5** mainnet goes as smoothly as possible, we would request all validators to join the `rebel-2` testnet. The Terra Classic L1 team will lay out an on-chain governance upgrade plan for this network. Background info: The `rebel-2` network was originally created by Dr. Edward Kim. As it contains some on-chain state (as opposed to a newly created one that the L1 team would set up solely for the upgrade tests) it's an ideal candidate for this initiative.

#### Please, Join the Testnet

Please use the following network parameters to join the `rebel-2` network:

- [genesis.json](https://network-rebel-2.s3.amazonaws.com/rebel-2/genesis.json)
- [addrbook.json](https://network-rebel-2.s3.amazonaws.com/rebel-2/addrbook.json)
- [archive snapshot (21.04.2023)](https://network-rebel-2.s3.amazonaws.com/rebel-2/archive-snapshot-21-04-2023.tar)
- [v1.1.0](https://github.com/classic-terra/core/archive/refs/tags/v1.1.0.tar.gz) of the `terrad` client

NOTE: We cannot exactly give you a guide how to join the testnet or what your local setup has to be in order to join the net. The purpose of this initiative is to test the upgrade with an validatorset and in an environment that is as close as possible to the `columbus-5` mainnet. We would prefer that the validators would join the `rebel-2` network with a setup that is similar to the one that they use for the `columbus-5`.

If validators need larger amount of testnet tokens, then they can reach out to Edward Kim or the L1 team in the Validator Discord channel. Please tag @ek826#9351 or @fragwuerdig#4755. These two persons can send testnet tokens. Smaller amounts of testnet tokens can be received from the [faucet](https://faucet.terrac.dev/).

#### Software Upgrade Proposal on the Testnet

The L1 team is going to make an software upgrade proposal. The exact date of when the upgrade proposal is going to be submitted will be announced here. We are planning to lay out a 3 day voting period so that validators have enough time to prepare their environment. We kindly ask validators to vote "yes" on this proposal when they are asked to. The proposal contains a upgrade plan. After it passes the chain is going to halt in a controlled manner. Validators are then asked to upgrade their `terrad` binary and restart the chain.

The chain state should accept the upgrade name `v3`. The current pre-release binary can be found at the following location:

- [https://github.com/classic-terra/core/archive/refs/tags/v2.0.0-alpha.tar.gz](https://github.com/classic-terra/core/archive/refs/tags/v2.0.0-alpha.tar.gz)

#### Backup Existing Store

At the time when the chain comes to a halt it is **highly adviced** to make a backup of the existing `data` folder (depending on the validators setup usually located at `${HOME}/.terra/data`). In the case that the new binary is not able to restart the chain, this gives validators quick access to a backup snapshot after a fix of the `terrad` binary has been delivered.

### Timeline

This timeline may be refined as the initiative goes on:

- **22nd of April**: The announcement an Invitation in the Validators Discord Channel.
- **22nd ~ 5th of May**: Onboarding period for validators. In this time the L1 team will give out testnet tokens to validators so they can self-bond and join the testnet
- **5th May ~ 8th of May**: Delivery of the chain halt upgrade proposal. Voting period.
- **9th of May**: Chain halt and test upgrade process.
