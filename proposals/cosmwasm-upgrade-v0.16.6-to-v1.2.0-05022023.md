# Wasmvm v0.16.6 => v1.2.0

## Introduction
This proposal seeks approval for the upgrade of Wasmd to version v0.31 in order to deploy the latests wasmvm v1.2.0 so we can push our network closer to parity with other Cosmos chains, while offering L2 developers access to any new features that have been added to the "smart contract execution layer" over the last couple of years. 

We expect this upgrade to have a high impact on the L2 dapp developers and users, which make up roughly 6 - 8% of the total network. This has prompted us to parition the workload into its own release (v2.0.5) to avoid dealing with too many breaking changes when the v2.0.4 release is published, which primarily focuses on updating other core dependencies such as Tendermint, Cosmos-SDK and TM-DB.

## Ammendments
The proposal consists of a two ammendments which seeks approval to update our Wasmd dependency to v0.31 and another which seeks a mandate to push L2 developers to begin the process of migrating their smart contracts to wasmvm v1.2.0.

### Ammendment 1/2
Update Wasmd to v0.31 & Wasmvm to v1.2.0.

### Ammendment 2/2
Approve the mandatory migration of smart contracts from wasmvm v0.16.6 to wasmvm v1.2.0. 

## Acceptance Criteria
2.0.5 is deployed with the new Wasmd v0.31 dependency and all active smart contracts are migrated to wasmvm v1.2.0.

## Summary
As such it will be feasible for the L1 team to release the v2.0.5 client for download at the end of Q1. However depending on the success of v1.0.6 and v2.0.4 respectively this milestone is subject to change and given the nature of the wasmvm upgrade we do not feel this is something that can or should be rushed. However as such it can not be understated how important this milestone is for the future of our network, as the release of v2.0.5 into mainnet will mark the conclusion of our upgrade efforts and begin our pivot towards focusing on building new features.

### Consequnce of a YES vote
If the vote is YES we will be able to upgrade wasmd to v0.31 and begin the process of migrating smart contracts to wasmvm v1.2.0.

### Consequnce of a NO vote
If the vote is NO we will be unable to upgrade wasmd to v0.31 and thus cannot migrate smart contracts to wasmvm v1.2.0. It worth noting that the v2.0.4 release will not suffer any significant consequences from this outcome.