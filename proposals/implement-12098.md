## Implement Proposal 12098

This is a PPJ proposal asking for approval to implement the tax distribution logic according to proposal 12098 which has passed governance and can be re-read here: https://station.terraclassic.community/proposal/columbus-5/12098

### Implementation Requirements

In order to implement the proposal I am suggesting the following implementation plan:

- Implementation of the new distribution logic in ante handler
- Adjust the split parameters to reflect the new split logic
- Adjust the proposal types and handlers to reflect the new parametrization
- Writing ante handler unit tests to test if the new logic reflects the requirements of proposal 12098
- Non-empty upgrade proposal handler to be able to rollout the changes with coordinated chain halt proposal and set the split/distribution parameters according to proposal 12098

### Cost Assessment
I (me, Frag, as an individual) offer to do the work required by proposal 12098 at an hourly rate of 66$ (including taxes). My personal assessment of the workload includes the following positions:

- 24h (3 workdays) of development, local testing, writing of unit tests
- 16h (2 workdays) of testnet rollout and coordination
- 16h (2 workdays) of mainnet rollout and coordination

This totals to 56h à 66$ = 3696$. For the sake of simplicity I am offering to do the complete job for 3600$.

### Timeline

The work on this proposal would start after the v3 upgrade by Genuine Labs has been deployed successfully. This is going to be beginning of June. Then implementation takes around two weeks. Mainnet rollout (including proposal stage) takes another 2 weeks. So, rollout for this feature can be targeted to be in beginning/mid July.

### PPJ Conditions

This proposal is not a spend proposal. It is a signalling/text proposal that gauges the validators and delegators interest in the proposed feature and asks for approval to start the work under the suggested conditions. After successful rollout of the PPJ feature the proposer is going to put up a spend proposal to claim $3600 from the community pool. The spend proposal will be denominated in LUNC using the market price at that time.

### Effects of Voting

- Vote **YES** if you agree on the proposers conditions/timeline to implement proposal 12098
- Vote **NO** if you disagree with the proposers conditions/timeline to implement proposal 12098
- Vote **ABSTAIN** to align your vote with the majority vote
- Vote **NO WITH VETO** if you think this proposal comprises a governance attack
