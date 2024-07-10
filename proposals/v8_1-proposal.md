### Release v3.1.0

A new release of the `terrad` client has been created on the 10th of July 2024. The release notes for the new version can be viewed here:

https://github.com/classic-terra/core/releases/tag/v3.1.0

The key change in this version is the introduction of the Oracle Split logic according to proposals 12098 and 12114. The logic will divert Community Pool rewards (originated from the Tax Split) to the Oracle Pool (OP) and therefore slow down it's depletion rate. 

### Proposal

This proposal seeks validator and community approval to update the `terrad` client to `v3.1.0` (upgrade name `v8_1`). The chain will be halted at **block height 19060800** (the exact height may be subject to change to fit to the anticipated upgrade time) which will approximately be processed on **26th of July 2024 06:30am UTC**. Upon passing of this proposal, an automatic chain halt will be scheduled at the specified height. The validators are going to be asked to install the new version of the `terrad` client after the chain halt occured.

### Upgrade Instructions for Validators

As soon as the chain automatically halts at the designated upgrade block height follow the upgrade procedure. Please **don't execute these commands before the chain has halted**:

```
$ git clone https://github.com/classic-terra/core core-v3.1.0
$ cd core-v3.1.0
$ git checkout v3.1.0
$ make build && make install 
```

In case you already have a local copy of the repository inside the local folder `core`:

```
$ cd core
$ git stash
$ git fetch --all --force --tags
$ git checkout v3.1.0
$ make build && make install
```

Check the correct installation:

```
$ terrad version
v3.1.0
```

After that, restart the client with `terrad start` and wait for consensus. During that period, **don't restart the client if not otherwise asked to do so**.

### Infrastructure Providers

Infrastructure providers who run mantlemint accelerated LCDs are asked to build and install the updated mantlemint version from source after the upgrade block height is reached:

https://github.com/classic-terra/mantlemint/releases/tag/v3.1.0

### Testing and Rollback

A rehearsal upgrade to `v3.1.0` is going to be conducted on rebel-2 testnet on the 11th of July 2024. Results will be shared accordingly. If for some unforeseen (and unlikely) reason the new release will not be able to produce new blocks on mainnet then the upgrade name `v8_1` can be applied to the previous release `v3.0.3`. In this case validators are going to be asked to roll back to a previous state and apply a patched `v3.0.3` release. 

### Effects of Voting

- **YES** - you agree to schedule an upgrade to v3.1.0
- **NO** - you don't agree to schedule an upgrade to v3.1.0
- **ABSTAIN** - you want the proposal to reach quorum and align with the majority vote
- **VETO** - you strongly disagree and want the prop to fail with a 33,33% veto threshold
