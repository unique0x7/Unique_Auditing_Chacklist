# Unique_Auditing_Chacklist

## version 
- 0.8.3 dosn't have custome error
- 0.8.25 have `MCopy` opcode which most of the chain not support that like [Mantle](https://docs.mantle.xyz/network/for-developers/the-differences-between-mantle-op-stack-and-ethereum#unsupported-opcodes)
- `push0` is not supported by all chains
- https://www.evmdiff.com/features?feature=opcodes

## Vulnerabilities in staking protocols
- Can rewards be delayed in payout, or claimed too early?
- Can rewards be improperly reduced or increased? In the worse case, can the user be prevented from receiving any reward?
- Can people claim principal or rewards that don’t belong to them, in the worst case draining the protocol?
- Can deposited assets get stuck in the protocol (partially or fully) or be improperly delayed in withdrawal?
- Conversely, if staking requires a time commitment, can users withdraw before the commitment time?
- If the payout is in a different asset or currency, can the value of it be manipulated within the scope of the smart contract in question? This is relevant if the protocol mints its own tokens to reward liquidity providers or stakers.
- If there is an expected and disclosed element of risk of losing principal staking, can that risk be improperly manipulated?
- Do key parameters of the protocol have admin, centralization, or governance risk?
- The key areas to look are the areas of the code that touch the “money exit” portions of the code.
-  There is a “money entrance” vulnerability to look for too.
- A corner case can be something like someone trying to claim a reward, but having nothing staked. This is valid, we should just give them zero reward. Similarly, we generally want to divide up rewards evenly, but what if there is only one recipient, and technically no division should happen?
  > https://www.rareskills.io/post/smart-contract-security#:~:text=Corner%20Cases%2C%20Edge%20Cases%2C%20and%20Off%20By%20One%20Errors

- Can users who have a right to participate in staking assets in the protocol be improperly prevented from doing so?

## Vote system
- Is there any check to prevent a user from voting again in the same Epoch?

## Swap
- while swap ETH the swap router may return some ETH so their shold be a reciver/callback funciton to store that other wise rever will happen [Link](https://github.com/sherlock-audit/2025-08-usg-tangent-judging/issues/150)



## Liquidation 
- The buyer’s collateral cannot be liquidated when the loan is not paid back or the collateral drops below the threshold.
- If collateral is drained from the protocol, then both the lender and borrower lose out, since the borrower has no incentive to pay back the loan, and the borrower loses the principal.
- Lack of slippage protection in liquidations exposes liquidators to losses [Link](https://github.com/sherlock-audit/2025-08-usg-tangent-judging/issues/263)
- 5% is not enough incintive for liquidator [Link](https://github.com/sherlock-audit/2025-08-usg-tangent-judging/issues/73)


## Fees
-   [pool can be non-profitable by specific Uniswap governance](https://code4rena.com/reports/2024-04-panoptic#m-05-panoptic-pool-can-be-non-profitable-by-specific-uniswap-governance)
  ## create2 
- if they using the new address for a pool attacker can create a pool in uniswap and prevent that from creating
- [CREATE2 address collision during pool deployment allows for complete draining of the pool](https://code4rena.com/reports/2024-04-panoptic#m-03-create2-address-collision-during-pool-deployment-allows-for-complete-draining-of-the-pool)

## LIbrary
- `LibClone` library, is incompatible with ZKsync. [link to a report ](https://solodit.cyfrin.io/issues/factory-deployments-wont-work-correctly-on-the-zksync-chain-codehawks-biconomy-nexus-git)
- [L-06] Protocol is using a vulnerable library version [link to a report](https://solodit.cyfrin.io/issues/l-06-protocol-is-using-a-vulnerable-library-version-pashov-none-yhairvesting-markdown)


## create function
- is it already created?

## FlashLoan function 
- Is it possible to give a flashloan and then call the deposit function to increase the balance mapping

## abi.encodePacked
- [when abi.encodepacked is using for hashing is have Sparator ?](https://github.com/orbit-chain/bridge-contract/blob/master/audit/Theori_OrbitBridge_2022_1Q.pdf)
  > when abi.encodePacked dosn't have spaarator it can produce same hash with diffrient value
  > fromChain = 123,  chain = 456
  > fromChain = 123456,  chain = 0
  > both are same so use `abi.encode` instead
  >
## ChainLink
- getPriceUSD() will return the wrong price when outside of min/max range [link](https://github.com/sherlock-audit/2023-05-USSD-judging/issues/112) , [Link](https://github.com/sherlock-audit/2023-05-USSD-judging/issues/197)

## forked
- AaveV2 forked projects often have a price manipulation vulnerability when the pool are deployed with empty liquidity.

