# v14_2 Proposal — Software Upgrade (Patch Release v4.0.1)

### Release v4.0.1

A new release of the `terrad` client has been created. The release notes for this version can be viewed here:
https://github.com/classic-terra/core/releases/tag/v4.0.1

This release is a patch update following the previously prepared `v4.0.0` release and should be read together with the original `v4.0.0` upgrade documentation.

Technical release notes for the incremental changes in `v4.0.1`:
https://github.com/classic-terra/documents/blob/main/chain-updates/v4_0_1.md

Baseline `v4.0.0` upgrade notes:
https://github.com/classic-terra/documents/blob/main/chain-updates/v4_0_0.md

### Proposal

This proposal seeks validator and community approval to update the `terrad` client to `v4.0.1` (upgrade name `v14_2`). The chain will be halted at **28486158** which will approximately be processed on **Wed May 6 2026 14:30 UTC**. The actual halt time is an early estimate, can vary, and depends on the chain's block speed until the specified height is reached.

Upon passing of this proposal, an automatic chain halt will be scheduled at the specified height. Validators are asked to install the new version of the `terrad` client after the chain halt occured.

Compared with `v4.0.0`, this patch release mainly includes:
- fixes for **legacy historical queries**
- fixes for **legacy staking / validator delegation query behavior**
- fixes for **IBC handling in wasm**, including registration of missing raw IBC wasm packet handling
- follow-up **Swagger / API documentation** updates

### Upgrade Instructions for Validators

As soon as the chain automatically halts at the designated upgrade block height, follow the upgrade procedure. Please **don't execute these commands before the chain has halted**:

```bash
$ git clone https://github.com/classic-terra/core core-v4.0.1
$ cd core-v4.0.1
$ git checkout v4.0.1
$ make build && make install
```

In case you already have a local copy of the repository inside the local folder `core`:

```bash
$ cd core
$ git stash
$ git fetch --all
$ git fetch --tags
$ git checkout v4.0.1
$ make build && make install
```

Check the correct installation:

```bash
$ terrad version
v4.0.1
```

After that, restart the client with `terrad start` or your system service and wait for consensus. During that period, **don't restart the client if not otherwise asked to do so**.

### Infrastructure Providers

Infrastructure providers (e.g. RPC/LCD/API providers and indexers) are advised to plan their own upgrade procedure around the same upgrade height and should rebuild any dependent services against the new `terrad` version where required.

Providers should validate:
- legacy historical queries
- validator delegation / staking queries at archive heights
- wasm / IBC-related integrations
- any Swagger / API-documentation-dependent tooling

### Testing and Rollback

The `v4.0.0` upgrade path and related changes were previously tested on rebel-2 testnet and in mainnet-fork/state-upgrade testing. `v4.0.1` is intended as a follow-up patch release addressing issues identified during final review of the `v4.0.0` line.

If, for any unforeseen reason, the new release is unable to resume block production on mainnet, validators may be asked to roll back to the previous state and temporarily run the prior release under the same upgrade name `v14_2` until a patched replacement release is provided.

### Effects of Voting

- **YES** - you agree to schedule an upgrade to v4.0.1
- **NO** - you don't agree to schedule an upgrade to v4.0.1
- **ABSTAIN** - you want the proposal to reach quorum and align with the majority vote
- **VETO** - you strongly disagree and want the prop to fail with a 33,33% veto threshold
