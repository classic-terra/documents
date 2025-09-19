# Proposal: Re-Enable Legacy Contract Execution

## Summary

This proposal seeks approval for a patch to the chain core that will re-introduce support for legacy CosmWasm contract execution. The change consists of a small fix (\~30–50 lines of code) that restores functionality broken during the v2.1.0 upgrade in 2022.

Affected contracts include not only a number of Astroport pools and potentially some remaining Terraswap pools. While re-enabling these contracts would make currently locked liquidity accessible again without requiring contract migration, the fix would also allow a lot more legacy contracts that include tax handling on chain to work again.

## Context

During the v2.1.0 upgrade, custom Terra query support was changed, which caused contracts to stop working, which query the tax rate on chain or exchange rates from the oracle module. This affected several liquidity pools holding significant amounts of LUNC and USTC (besides other tokens).

Key findings from a node-level patch test:

* The patch allows transactions against these contracts to succeed again.
* Pools currently contain large amounts of locked liquidity.
* Example balances (rounded):
  * LUNC/USTC pool: \~700M LUNC, \~6M USTC
  * bLUNA/LUNC pool: \~150M LUNC
  * MIR/USTC pool: \~6M USTC
  * ASTRO/USTC pool: \~3.9M USTC
  * kUST/USTC pool: \~2.9M USTC
* Across 465 identified Astroport contracts:
  * \~27.4M USTC
  * \~959M LUNC

These tokens are currently unreachable due to the broken execution path. That means, traders can not use those pools at all (native ↔ native) or only in one direction (cw20 ← native).

## Implications

Re-enabling execution is expected to instantly “re-open” these pools. This has two sides:

* **Positive:** The chain and its users regain access to their liquidity. Tokens that should be in circulation become usable again. Further, there will be a lot more contracts that will start working again without the need of contract migration.
* **Negative:** The affected pools are highly imbalanced. Immediately after activation, users and most likely arbitrage bots will drain the obvious opportunities. Example: the LUNC/USTC pool trades at roughly 2× the fair market ratio. This means large swings will happen within minutes of the fix going live. This could affect the price of LUNC and USTC both positive or negative on other DEXes/CEXes, too, in the short term.

## Risks

* **Arbitrage drain:** First movers (mostly bots) will capture outsized profits, not long-term holders.
* **Public perception:** Can be framed as “unlocking” large amounts of USTC/LUNC supply, which may be viewed negatively, although these coins where always meant to be unlocked. The “locking” happened due to a core upgrade side-effect.
* **Timing:** Liquidity providers in affected and currently disfunctional pools cannot “exit early” before the patch is applied.
* **Precedent:** Some may argue this sets a precedent for L1 patches to support dApps. However, the breakage was originally caused by an L1 upgrade, and the fix is small and contained.

## Conclusion

The patch restores functionality that was unintentionally broken. It unlocks liquidity for affected users and contracts, and will restore contract functionality for legacy contracts on chain.

**Voting Options:**

* **YES** – Approve the patch to re-enable legacy contract execution.
* **NO** – Do not apply the patch, legacy contracts remain unusable.
* **NO WITH VETO** – Strong opposition.
* **ABSTAIN** – No opinion.

