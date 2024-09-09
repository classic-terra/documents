### Release v3.1.5

A new release of the `terrad` client has been created on the 5th of September 2024. The release notes for the new version can be viewed here:

https://github.com/classic-terra/core/releases/tag/v3.1.5

This release applies the wasmd security patch from Genuine Labs' PR #512 on v3.1.4. This update bumps wasmd to 0.46 and wasmvm to 1.5.4. This update also includes the changes from v3.1.4. The previous version v3.1.4 containing a fix for gas estimation of taxable transactions was only released to endpoint providers as it did not contain consensus-relevant changes.

### Proposal

This proposal seeks validator and community approval to update the `terrad` client to `v3.1.5` (upgrade name `v8_2`). The chain will be halted at **block height 19850000**  which will approximately be processed on **18th of September 2024 11:15am UTC**. Upon passing of this proposal, an automatic chain halt will be scheduled at the specified height. The validators are going to be asked to install the new version of the `terrad` client after the chain halt occured.

### Upgrade Instructions for Validators

As soon as the chain automatically halts at the designated upgrade block height follow the upgrade procedure. Please **don't execute these commands before the chain has halted**:

```bash
$ git clone https://github.com/classic-terra/core core-v3.1.5
$ cd core-v3.1.5
$ git checkout v3.1.5
$ make build && make install 
```

In case you already have a local copy of the repository inside the local folder `core`:

```bash
$ cd core
$ git stash
$ git fetch --all
$ git fetch --tags
$ git checkout v3.1.5
$ make build && make install
```

Check the correct installation:

```bash
$ terrad version
v3.1.5
```

After that, restart the client with `terrad start` or your system service and wait for consensus. During that period, **don't restart the client if not otherwise asked to do so**.

### Infrastructure Providers

Infrastructure providers who run mantlemint accelerated LCDs are asked to build and install the updated mantlemint version from source after the upgrade block height is reached:

https://github.com/classic-terra/mantlemint/releases/tag/v3.1.5

### Testing and Rollback

A rehearsal upgrade to `v3.1.5` was conducted on rebel-2 testnet on 8th of September 2024. If for some unforeseen (and unlikely) reason the new release will not be able to produce new blocks on mainnet then the upgrade name `v8_2` can be applied to the previous release `v3.1.3`. In this case validators are going to be asked to roll back to a previous state and apply a patched `v3.1.3` release.

### Effects of Voting

- **YES** - you agree to schedule an upgrade to v3.1.5
- **NO** - you don't agree to schedule an upgrade to v3.1.5
- **ABSTAIN** - you want the proposal to reach quorum and align with the majority vote
- **VETO** - you strongly disagree and want the prop to fail with a 33,33% veto threshold
