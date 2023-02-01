# Antehandler BurnTax split


## Introduction
In order to avoid the re-minting of "manual burns" during the seigniorage calculation we have worked with DemonMonkey to detail a solution where in the system will collect the burn tax directly in the AnteHandler by altering the NewBurnTaxFeeDecorator code to split the burn taxes into two halves with one going to  the Community Pool directly and another is sent to the burn wallet as per usual. In conjunction with a change to the RewardPolicy this will result in burn taxes being collected as intended while avoiding a re-mint of the "manual burns".

## Ammendments
The current proposal consists of a single ammendment which seeks approval to deploy the altered NewBurnTaxFeeDecorator code. 

### Ammendment 1/1
Approve the release of https://github.com/classic-terra/core/commit/6b8b172615ecf51e3e1fced43284ae3b55d23a0c into mainnet as part of v1.0.6.

## Acceptance Criteria
Stops re-minting "manual burns" and instantly ships burn tax proceeds to the CommunityPool.

## Summary
With this alteration of the system we hope to achieve an  outcome that is desirable for all parties. As such we understand the concern about re-minting "manual burns" and it is our belief that if the code works as  intended it will solve that problem until such a time where the RewardPolicy is altered in a way that would re-enable segniorage re-minting.

### Consequnce of a YES vote
If we vote YES on this proposal we will have a clear path to deploying the new feature which will allow us to collect "burn taxes" without having to rely on the segniorage logic built into the system.

### Consequnce of a NO vote
If we vote NO on this proposal we will either be unable to collect burn taxes or we will have to continue re-minting "manual burns".