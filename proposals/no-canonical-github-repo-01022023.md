# No Canonical GitHub Repository

## Introduction
Currently the Terra-Money and Terra-Rebels GitHub organizations contain the only canonical GitHub repositories approved by the Terra Classic governing consensus body. This makes it hard for validators to accept PRs from other people/groups/organizations that might want to upgrade, improve or hotfix our network. Thus to encourage the creation of more development teams that can support our needs for "client diversity" we believe that it would be preferable to implement the solution suggested by Jacob Gadikian and adopt a release strategy that revolves around commit IDs. This combined with increased due dilligence from the validator pillar (related to security audits of the code that is deployed to mainnet), will in our view lead to more decentralization and will ultimately benefit everyone.

## Ammendments
The current proposal consists of two ammendments, one which seeks to repeal proposal #4940 and another that enables validators to recieve client update from anyone providing a commit ID, granted that it works, passed QA testing, contains no malicious code and does not result in halting the chain.

### Ammendment 1/2
Repeal proposal #4940 to enable updates to be sourced from anywhere.

### Ammendment 2/2
Allow any person/group/organization to produce a release for the validator pillar as long as they respect the semantic versioning schema and coordinate with other development teams.

## Acceptance Criteria
Anyone can produce a client release based on a specified commit ID.

## Summary
To summarize, we seek to ensure that we can increase the number of people with access to improving the network client while ensuring the overall stability of our network.

If the Agora proposal is approved we suggest that it is ported directly to a text proposal and submitted for ratification.

### Consequnce of a YES vote
If the vote results in a YES, we will enable validators to take client updates from anyone they believe can create value for the network. This would result in a net productivity gain for developers, granted that teams can agree to synchronize changes between them in a civil manner (no closed source repos & drama).

### Consequnce of a NO vote
If the vote results in a NO, we will be forced to continue pushing upstream PRs to the afformentioned repos which by and large are no longer maintained. We could add the L1 teams current repo to the canonical list, but that would only really push the problem down the road, which overall results in a net productivity loss for the developers until the situation is resolved.
