**Edit notice (06.03.2024):** Removed PFM from mainnet release... re-tagged release to v2.4.1

### Release v2.4.1

A new release of the `terrad` client has been created on the 1st of March 2024 (re-tagged on 5th of March). The release notes for the new version can be viewed here:

https://github.com/classic-terra/core/releases/tag/v2.4.1

Key changes:

- Introduction of IBC-Hooks (by Genuine Labs and Fragwuerdig)
- E2E and Interchain Testing Suite (by Genuine Labs)
- A fix regarding the processing of `MsgExec` in the Tax Ante Handler (by Fragwuerdig)
- **PFM will _not_ be shipped with this version**

The introduction of IBC-Hooks will enable the onboarding of dApps that depend on this feature - most notably Enterprise DAO.

### Proposal

This proposal seeks validator and community approval to update the `terrad` client to `v2.4.1` (upgrade name `v7`). The chain will be halted at **block height 17309500** which will approximately be processed on **25th of March 2024 14:00 UTC**. Upon passing of this proposal, an automatic chain halt will be scheduled at the specified height. The validators are going to be asked to install the new version of the `terrad` client after the chain halt occured.

### Upgrade Instructions for Validators

As soon as the chain automatically halts at the designated upgrade block height follow the upgrade procedure. Please **don't execute these commands before the chain has halted**:

```
$ git clone https://github.com/classic-terra/core core-v2.4.1
$ cd core-v2.4.1
$ git checkout v2.4.1
$ make build && make install 
```

In case you already have a local copy of the repository inside the local folder `core`:

```
$ cd core
$ git stash
$ git fetch --all --force --tags
$ git checkout v2.4.1
$ make build && make install
```

Check the correct installation:

```
$ terrad version
v2.4.1
```

After that, restart the client with `terrad start` and wait for consensus. During that period, **don't restart the client if not otherwise asked to do so**.

### Infrastructure Providers

Infrastructure providers who run mantlemint accelerated LCDs are asked to build and install the updated mantlemint version from source after the upgrade block height is reached:

https://github.com/classic-terra/mantlemint/releases/tag/v2.4.1

### Testing and Rollback

The newly introduced features IBC-Hooks and PFM have been thoroughly integration tested by Genuine Labs with the introduction of the Interchain Testing Suite. A rehearsal upgrade to `v2.4.1` has been conducted on rebel-2 testnet on the 27th of February 2024. If for some unforeseen (and unlikely) reason the new release will not be able to produce new blocks on mainnet then the upgrade name `v7` can be applied to the previous release `v2.3.3`. In this case validators are going to be asked to roll back to a previous state and apply a patched `v2.3.3` release. 

### Effects of Voting

- **YES** - you agree to schedule an upgrade to v2.4.1
- **NO** - you don't agree to schedule an upgrade to v2.4.1
- **ABSTAIN** - you want the proposal to reach quorum and align with the majority vote
- **VETO** - you strongly disagree and want the prop to fail with a 33,33% veto threshold
