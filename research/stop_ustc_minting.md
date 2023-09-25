# USTC minting 

Passed proposal: https://station.terraclassic.community/proposal/columbus-5/11784

## Current mechanism
https://github.com/classic-terra/core/blob/main/x/market/keeper/swap.go#L72

Terra => Terra swap is currently being implemented here. I am wondering if it is good idea to disable it?

A parameter can be coded into it to limit USTC swap instead of outright stopping, that should give community more control in the event that they want to re - enable it.

Currently, min stability spread is used to cap swap between LUNC and USTC. The same mechanism can be applied for Terra swap (Specifically USTC)

## Design goals
1. Min stability spread for Terra swap should specifically target USTC instead of other denoms
2. Min stability spread will be applied to swapping to USTC. Swap to USTC will mint, swap from USTC will burn