# Unique_Auditing_Chacklist

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
- A corner case can be something like someone trying to claim a reward, but having nothing staked. This is valid, we should just give them zero reward. Similarly, we generally want to divide up rewards evenly, but what if there is only one recipient, and technically no division should happen?
  [] https://www.rareskills.io/post/smart-contract-security#:~:text=Corner%20Cases%2C%20Edge%20Cases%2C%20and%20Off%20By%20One%20Errors

There is a “money entrance” vulnerability to look for too.

- Can users who have a right to participate in staking assets in the protocol be improperly prevented from doing so?

## Vote system
- Is there any check to prevent a user from voting again in the same Epoch?

## Liquidation 
- The buyer’s collateral cannot be liquidated when the loan is not paid back or the collateral drops below the threshold.
- If collateral is drained from the protocol, then both the lender and borrower lose out, since the borrower has no incentive to pay back the loan, and the borrower loses the principal.

## create function
- is it already created?
- 
