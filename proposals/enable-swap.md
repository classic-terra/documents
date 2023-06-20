### Preface

This document is going to outline an implementation strategy to re-enable the Terra Classic market module. First of all we would like to emphasize the following statement: Enabling the market module cannot be viewed as the ultimate way to repeg USTC. Buyback and repeg strategies have to be carefully worked out by a professional team of financial quantitative analysts. However, we think that the market module is a key piece in the puzzle in order to maintain an *on-chain* mechanism to provide liquidity for the LUNC/USTC pair, stabilize USTC and providing a functioning arbitrage mechanism - where the latter ultimately provides an important usecase for LUNC.

### Swaps

Let' recap how traditional swap pools in crypto work. We assume the following setup:

- *Liquidity Providers* (LPs) provide a coin pair (say coin $A$ and $B$) and throw them into a (liquidity) pool
- *Traders* throw one coin (say $A$) into the pool and therefore are eligible to with withdraw a certain amount of $B$

This setup is usually implemented using a smart contract deployed on a blockchain. We define the exchange rate $E_{BA}$ as the amount of B that the trader is eligible to withdraw per unit amount of provided A. Now, traditional Uniswap v2 pools determine the exchange rate by adhering to the following curve:

$$ k = A \cdot B $$

Here, $k$ is a constant called *liquidity*. Traders can come into the pool and swap around as much as they want: The balance of $A$ vs. $B$ would certainly change. But the fundamental liquidity of the pool would not. In contrast to that: If more LPs came in and provided more liquidity (threw more coins into the pool), the $k$ constant would be considered to be subject to change.

How would this so called *constant product* curve determine the exchange rate? Let's work out what would happen if a trader came in and provided $\Delta A$ of coins and is eligible to withdraw $\Delta B$ of coins. We assumed the liquidity to be constant. So before the swap we had $k = A \cdot B$ and after the swap we would have:

$$ k = (A + \Delta A)\cdot (B - \Delta B) $$

$$ k = A \cdot B  - A \cdot \Delta B + B \cdot \Delta A - \Delta A \cdot \Delta B$$

Using the fact that $A \cdot B = k$ we arrive at:

$$ E_{BA} := \frac{\Delta B}{\Delta A} = \frac{B}{ A + \Delta A}$$

So we worked out what exchange rate that the trader gets. Let's assume that $\Delta A$ is extremely small in comparison to $A$ and $B$. This is the equivalent of saying that the liquidity in the pool is *deep* in comparison to the swap volume. In this case we can even further simplify:

$$ E_{BA,\infty} = \frac{B}{A}$$

And here we also see immediately why the constant product curve was a good choice to determine the exchange rate in the first place: It simply makes the exchange rate ending up as being proportional to the balance of $B$ versus $A$ in the pool. This reflects two fundamental aspects of pricing: Demand and Supply. Many traders swapping $A$ against $B$? This means the pool tends to have excess balance towards $B$. This in turn means $E_{BA,\infty}$ rises, which means "I can get more $B$ out of the same amount of $A$". Which is the equivalent of saying: "The coin $B$ is less valuable compared to $A$" or "The price of $B$ falls".

You may have noticed that of course $E_{BA} \le E_{BA,\infty}$
