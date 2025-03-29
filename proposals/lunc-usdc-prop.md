## Phased Approach to Establish On-Chain Liquidity for USDC on Terra Classic

### Motivation

Currently, **Terra Classic lacks a direct on-chain stablecoin trading pair for LUNC**, forcing users to rely on centralized exchanges (CEXs) for stable conversions. This reliance introduces **liquidity fragmentation, higher slippage, and centralized risks**, limiting the efficiency of on-chain trading and DeFi applications. Without a stable LUNC pair, users face difficulty in executing trades with predictable pricing, affecting traders, liquidity providers, and developers building on Terra Classic. The lack of on chain liquidity also **inhibits the development of DeFi infrastructure** that usually relies on the availability of on-chain availability of stables.

The introduction of a USDC/LUNC liquidity pool will address these challenges by:

- **Enhancing market depth and liquidity**: Matching Binance’s ±2% market depth of ~$50K–$100K ensures smoother on-chain trading.

- **Providing DeFi utility**: A stable LUNC pair enables lending, borrowing, and yield farming applications, attracting more users and TVL (Total Value Locked) to the ecosystem.

- **Reducing dependence on CEXs**: On-chain liquidity removes the need to use off-chain platforms for stablecoin conversions, improving decentralization and reducing counterparty risks. Furthermore, on chain DeFi applications _can't_ interoperate with CEXs and therefore depend on DEX liquidity.

- **Minimizing market impact**: By splitting the funding request into multiple proposals, this proposal ensures a controlled and strategic deployment that avoids major price fluctuations and minimizes the exposure to the risk of a total-loss event.

- **Creating arbitrage opportunities with CEX stable pairs**: A liquid on-chain USDC/LUNC market allows traders to exploit price differences between Terra Classic and CEXs, fostering increased on-chain activity and organic trading volume.

- **Supporting existing DEX platform**: Injecting liquidity into Terraport  helps these platforms increase their trading volume, attracting more users and improving overall ecosystem efficiency.

### Execution Plan:

1. Split the spend request into multiple proposals to control the flow of LUNC into the market without creating too much volatility. The proposer recommends to request and deploy the liquidity in three equal installments and pply steps 2 to 8 for each of these installments.

2. The spend proposal is going to transfer the requested allocation of LUNC into a multisig account to ensure secure and transparent execution. The multisig will be a 6/9 cw3 fixed multisig. Meaning: A smart contract managed multisig account with 9 voting parties. 6 voters to agree on a multisig action.

3. Multisig owners agree on a selected trusted multisig member to transfer funds into a centralized exchange. After that 50% of the dollar denominated funds will be transferred to that CEX and then swapped out to USDC.

4. Transfer the acquired USDC to Coinbase. This step is needed, because Coinbase has a withdrawal function to transfer the USDC to the native issuance chain of USDC for the Cosmos Ecosystem. See next step.

5. From Coinbase, withdraw USDC to Noble. 

6. Bridge USDC from Noble to Terra Classic via the IBC network. The receiving wallet of this transaction will be the original multisig wallet from step 2.

7. Deploy the allocated liquidity in equal parity to a newly created LUNC/USDC pair on Terraport. The multisig wallet will acquire LP tokens from the transaction as receipt for the liquidity..

8. The multisig will send the acquired LP tokens to the Terra Classic governance account. From there the LP tokens can be managed in a **fully decentralized** way.

### Funding Request:

800M LUNC, split into three spend proposals, each funding a portion of the liquidity initiative. 400M LUNC will be used to acquire USDC. At current market rates this will provide roughly $45k liquidity (or 22.5k single-sided).

### Summary 

This proposal aims to establish a liquid and stable trading environment for LUNC, bringing Terra Classic closer to a robust DeFi ecosystem and more independence from centralized exchanges. By splitting the funding request into multiple spend proposals and using a multisig account, we ensure a controlled, strategic approach that minimizes market disruption while achieving our liquidity goals and maintaining a  relatively decentralized deployment approach. After deployment the liquidity will be managed completely decentralized via Terra Classic Governance.

### Voting Options:

**YES** – Approve the phased allocation of LUNC from the community pool for this liquidity initiative.

**NO** – Reject the proposal and maintain the current liquidity structure.

We welcome community feedback and support in making this a successful initiative!
