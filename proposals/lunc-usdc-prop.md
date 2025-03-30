## Phased Approach to Establish On-Chain Liquidity for USDC on Terra Classic

### Motivation

Currently, **Terra Classic lacks a direct on-chain stablecoin trading pair for LUNC**, forcing users to rely on centralized exchanges (CEXs) for stable conversions. This reliance introduces **liquidity fragmentation, higher slippage, and centralized risks**, limiting the efficiency of on-chain trading and DeFi applications. Without a stable LUNC pair, users face difficulty executing trades with predictable pricing, affecting traders, liquidity providers, and developers building on Terra Classic. The lack of on-chain liquidity also **inhibits the development of DeFi infrastructure**, which typically relies on the availability of on-chain stablecoins.

The introduction of a USDC/LUNC liquidity pool will address these challenges by:

- **Enhancing market depth and liquidity**: Matching Binance’s ±2% market depth of \~\$50K–\$100K ensures smoother on-chain trading.

- **Providing DeFi utility**: A stable LUNC pair enables lending, borrowing, and yield farming applications, attracting more users and increasing TVL (Total Value Locked) in the ecosystem.

- **Reducing dependence on CEXs**: On-chain liquidity removes the need to use off-chain platforms for stablecoin conversions, improving decentralization and reducing counterparty risks. Furthermore, on-chain DeFi applications *cannot* interoperate with CEXs and therefore depend on DEX liquidity.

- **Minimizing market impact**: By splitting the funding request into multiple proposals, this plan ensures a controlled and strategic deployment that avoids major price fluctuations and minimizes exposure to the risk of a total-loss event.

- **Creating arbitrage opportunities with CEX stable pairs**: A liquid on-chain USDC/LUNC market allows traders to exploit price differences between Terra Classic and CEXs, fostering increased on-chain activity and organic trading volume.

- **Supporting existing DEX platforms**: Injecting liquidity into Terraport helps these platforms increase their trading volume, attracting more users and improving overall ecosystem efficiency.

### Execution Plan

1. Split the spending request into multiple proposals to control the flow of LUNC into the market without creating excessive volatility. The proposer recommends requesting and deploying the liquidity in three equal installments and applying steps 2 to 8 for each installment.

2. The spend proposal will transfer the requested allocation of LUNC into a multisig account to ensure secure and transparent execution. The multisig will be an **8-out-of-12 cw3 fixed multisig**, meaning a smart contract-managed multisig account with 12 voting parties, requiring 8 voters to agree on a multisig action.

3. Multisig owners will agree on a selected trusted multisig member to transfer funds into a centralized exchange. After that, 50% of the dollar-denominated funds will be transferred to that CEX and then swapped for USDC.

4. Transfer the acquired USDC to Coinbase. This step is necessary because Coinbase has a withdrawal function to transfer USDC to the native issuance chain of USDC for the Cosmos ecosystem (see next step).

5. From Coinbase, withdraw USDC to Noble.

6. Bridge USDC from Noble to Terra Classic via the IBC network. The receiving wallet for this transaction will be the original multisig wallet from step 2.

7. Deploy the allocated liquidity in equal parity to a newly created LUNC/USDC pair on Terraport. The multisig wallet will acquire LP tokens from the transaction as a receipt for the liquidity.

8. The multisig will send the acquired LP tokens to the Terra Classic governance account. From there, the LP tokens can be managed in a **fully decentralized** manner.

### Funding Request

800M LUNC, split into three spend proposals, each funding a portion of the liquidity initiative. 400M LUNC will be used to acquire USDC. At current market rates, this will provide roughly \$45K in liquidity (or \$22.5K single-sided).

### Multisig Signers

We propose the following list of multisig signers. These are individuals and validators who have demonstrated strong support for the LUNC ecosystem over the long run:

- LuncGoblins
- LuncLive
- Jacob Gadikian
- JurisProtocol
- LVS
- Hexxagon
- Vegas
- Rexyz
- Nicolas Boulay
- Garuda
- Jesus is Lord
- Allnodes

This is a large, broad, and diverse group of respected community members. This initiative aims to unite different factions and create a valuable effort for the chain.

### High-Risk CEX Trades

This proposal involves using centralized exchanges to acquire USDC, which can only be undertaken by a single entity or individual due to the nature of CEXs. We acknowledge that this approach goes against the decentralized practices traditionally followed on Terra Classic. However, USDC cannot currently be acquired on the DEX market due to insufficient on-chain liquidity—precisely the problem this proposal aims to solve.

We nominate **LuncGoblins** aka **Fragwuerdig** (real name: Till Ziegler) to handle these high-risk trades. He is a well-respected and trusted community member with KYC certification through SolidProof ([SolidProof KYC](https://github.com/solidproof/projects/tree/main/2024/Fragwuerdig)). He has no reason or incentive to embezzle this grant.

The risk of partial or full loss of funds due to human or technical error can be mitigated by splitting the spending proposal into multiple installments. Internally, these installments will be further divided into three equal parts, ensuring that each trade only involves approximately \$2.5K.

### Price Impact and Acquisition Strategy

This proposal seeks to minimize the price impact on LUNC by matching the ±2% depth of the centralized market on Binance. This means that when a single trade with 50% of the two-sided target liquidity is executed, the price is expected to move only 2% downward. However, to further mitigate negative price movements, the acquisition will occur in several trades. The swaps will only be executed during an upward market movement on the 4-hour timeframe. Additionally, trades will not be initiated using a Market Order but rather with a Limit Order at the current market price (Stop Limit) to minimize exposure to slippage.

### Summary

This proposal aims to establish a liquid and stable trading environment for LUNC, bringing Terra Classic closer to a robust DeFi ecosystem while reducing reliance on centralized exchanges. By splitting the funding request into multiple spend proposals and using a multisig account, we ensure a controlled, strategic approach that minimizes market disruption while achieving our liquidity goals in a relatively decentralized manner. After deployment, the liquidity will be managed entirely through Terra Classic governance.

### Voting Options

**YES** – Approve the phased allocation of LUNC from the community pool for this liquidity initiative.

**NO** – Reject the proposal and maintain the current liquidity structure.
