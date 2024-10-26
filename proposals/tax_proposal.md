## Summary

This proposal seeks approval to deploy the "Reverse Charge" mechanism on Terra Classic and replace the tax2gas approach. The Reverse Charge solution simplifies tax handling by automatically deducting tax from the amount sent before it reaches the recipient's wallet, eliminating the need for the sender to pay the tax as an additional fee. The system retains full backward compatibility and offers developers an option to still use sender-side taxation for fund transfers if desired. The approach also solves the double taxation issue on contracts that is present in the current system.

## Motivation

The existing tax system on Terra Classic requires the sender to cover tax fees on top of gas, which has been a significant development burden for dApps, particularly those originating from other ecosystems. To alleviate this, the proposed system was developed, automatically handling tax deductions on the blockchain itself. This eliminates the need for dApp developers to implement complex tax-handling logic in contracts or dApp interfaces.

## Status of Development

The solution has already been fully developed. During testing on a local system and the secondary testnet, the Reverse Charge approach has caused no issues on dApps. Tests were conducted with UIs handling tax and UIs not handling tax as well as using the command line terrad client. The solution provides a significant improvement in usability for both developers and users. Furthermore, it eliminating double taxation on contracts.

The tax2gas proposal, although previously approved, is rendered unnecessary by this new solution.

## Changes

The implementation of Reverse Charge introduces the following key modifications:

* Automatic Tax Deduction:  
  Tax by default is deducted from the sent amount, removing the need for the sender to make sure to send enough fees.
* Backward Compatibility:  
  dApps can still choose to allow the sender to cover the tax on normal fund transfers if desired, ensuring full backward compatibility with existing systems.
* Contract Interaction:
  In case dApps continue to let the sender pay tax when interacting with contracts, these funds are automatically refunded to ensure a consistent and fair taxation process
* Elimination of Double Taxation:  
  Contracts will no longer be taxed when receiving funds; taxation will only occur when funds are sent out to a wallet.
* Tax2Gas Obsolescence:  
  This solution replaces the need for the tax2gas approach, resolving the concerns and complexities associated with that model.
* Whitelisting:
  Existing whitelisting mechanisms remain intact (i.e., for Binance wallets). It is desired to implement a more fine-grained whitelisting feature under governance control via "tax zones" in a future update. The proposed implementation of tax handling is fully compatible with that.
* Wallet Compatibility  
  Wallets like Keplr, Station and others are expected to continue to work without changes. Local tests emulating the process used by these wallets have shown no issues.

## Testing and Deployment

The system was fully developed and has been successfully deployed on the secondary testnet. Tests were conducted on various transaction types, including sending LUNC, NFT collection deployment, and buying NFTs via UI. In all cases, tax deductions worked as intended, with both backward-compatible and new tax query methods functioning seamlessly.

Further testing will focus on additional use cases, e.g. voting on proposals. Participation of users and dApps in these tests is encouraged. If this proposal is approved, the remaining tasks listed below will be completed and the system will be prepared for mainnet deployment through a software upgrade proposal.

The following tasks remain to be completed:

* Deployment on primary rebel-2 testnet
* Further use-case testing on the testnet
* Fixing interchain tests introduced in SDK 0.47
* Preparing the release for mainnet deployment
* Review by another developer or team

## Cast Your Vote

Yes: Approve the implementation of Reverse Charge, simplifying tax handling and replacing tax2gas.  
No: Reject the proposal and maintain the current tax system, with potential for future tax2gas deployment.  
Abstain: You have no strong opinion and will accept the majority's decision.  
Veto: You believe this proposal is harmful and should not be implemented.