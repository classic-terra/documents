### Release v3.3.0

A new release of the `terrad` client has been created on the 3rd of December 2024. The release notes for the new version can be viewed here:

https://github.com/classic-terra/core/releases/tag/v3.4.0-rc.0

This release introduces implmentation for fork modules removal. 
Details for the changes can be found here at  https://station.terraclassic.community/proposal/columbus-5/12142, 

The upgrade should cause no changes to the chain's state, interface, or functionality. 


The details of the unform removal can be found here: https://github.com/orbitorg/core/issues

### Proposal

This proposal seeks validator and community approval to update the `terrad` client to `v3.4.0-rc.0` (upgrade name `v11_1`). The chain will be halted at **block height {tobedecided}**  which will approximately be processed on **Jan 10, 2025, 12:57:47 UTC**. The actual halt time is an early estimate, can vary and depends on the chain's block speed until the specified height is reached. Upon passing of this proposal, an automatic chain halt will be scheduled at the specified height. The validators are going to be asked to install the new version of the `terrad` client after the chain halt occured.

### Upgrade Instructions for Validators

As soon as the chain automatically halts at the designated upgrade block height follow the upgrade procedure. Please **don't execute these commands before the chain has halted**:

```bash
$ git clone https://github.com/classic-terra/core core-v3.4.0-rc.0
$ cd core-v3.4.0-rc.0
$ git checkout v3.4.0-rc.0
$ make build && make install 
```

In case you already have a local copy of the repository inside the local folder `core`:

```bash
$ cd core
$ git stash
$ git fetch --all
$ git fetch --tags
$ git checkout v3.4.0-rc.0
$ make build && make install
```

Check the correct installation:

```bash
$ terrad version
v3.4.0-rc.0
```

After that, restart the client with `terrad start` or your system service and wait for consensus. During that period, **don't restart the client if not otherwise asked to do so**.

### Infrastructure Providers

Infrastructure providers who run mantlemint accelerated LCDs are asked to build and install the updated mantlemint version from source after the upgrade block height is reached:

https://github.com/classic-terra/mantlemint/releases/tag/v3.4.0-rc.0

### Testing and Rollback

An upgrade to `v3.4.0-rc.0` release candidate was conducted on rebel-2 testnet on 7th of November 2024 and the changes were tested extensively. If for some unforeseen (and unlikely) reason the new release will not be able to produce new blocks on mainnet then the upgrade name `v11_1` can be applied to the previous release `v3.1.6`. In this case validators are going to be asked to roll back to a previous state and apply a patched `v3.1.6` release.

### Effects of Voting

- **YES** - you agree to schedule an upgrade to v3.4.0-rc.0
- **NO** - you don't agree to schedule an upgrade to v3.4.0-rc.0
- **ABSTAIN** - you want the proposal to reach quorum and align with the majority vote
- **VETO** - you strongly disagree and want the prop to fail with a 33,33% veto threshold
