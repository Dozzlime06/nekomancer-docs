# Referral Program

Earn passive income by sharing Nekomancer with others.

## How It Works

1. **Generate Your Code**: Get a unique referral code
2. **Share Your Link**: Send your link to friends
3. **Earn 20%**: When they swap, you earn 20% of the platform fee
4. **Claim Anytime**: Withdraw your earnings to your wallet

## Getting Started

### Step 1: Generate Your Code

1. Go to [nekomancer.fun/referral](https://www.nekomancer.fun/referral)
2. Connect your wallet
3. Click "Generate Referral Code"
4. You'll receive a unique 8-character code (e.g., `NEKOZM3J`)

### Step 2: Share Your Link

Your referral link format:
```
https://www.nekomancer.fun/swap?ref=YOUR_CODE
```

Example:
```
https://www.nekomancer.fun/swap?ref=NEKOZM3J
```

Share this link on:
- Social media (Twitter, Discord, Telegram)
- Your community
- Friends and family

### Step 3: Track Your Earnings

On the Referral page, you can see:
- **Referrals**: Number of unique wallets that swapped using your code
- **Total Earned**: Lifetime earnings in MON
- **Claimable**: Current balance ready to withdraw

### Step 4: Claim Your Earnings

1. Go to [nekomancer.fun/referral](https://www.nekomancer.fun/referral)
2. View your claimable balance
3. Click "Claim Earnings"
4. Confirm the transaction in your wallet
5. MON will be sent to your wallet

## Earnings Calculation

### Fee Structure
- Total platform fee: **1%** per swap
- Your share: **20%** of the 1% fee

### Example
If someone swaps 1000 MON using your link:
- Platform fee: 10 MON (1%)
- Your earnings: 2 MON (20% of 10 MON)

### Minimum Claim
- Minimum claim amount: ~$10 USD worth of MON
- Earnings accumulate until you reach the minimum
- No maximum limit on earnings

## Important Rules

### What Counts as a Referral
- User must click your referral link
- User must complete a swap (not just visit)
- Only actual token swaps count (not MON↔WMON wraps)

### What Doesn't Count
- Your own swaps
- MON to WMON wraps/unwraps
- Failed transactions
- Users who already have a referrer

### One Referrer Per User
- Each wallet can only have one referrer
- The first referral link used is permanent

## ReferralVault Contract

Your earnings are stored in the ReferralVault smart contract:

| Property | Value |
|----------|-------|
| Address | `0x28e123cfd53EA9B39BCec297eba161F0742764F2` |
| Type | UUPS Upgradeable |
| Minimum Claim | ~$10 USD in MON |

### Contract Functions
- `claim()` - Claim all pending earnings
- `claimAmount(amount)` - Claim specific amount
- `getReferrerStats(address)` - View your stats

## Tips for Success

1. **Target Active Traders**: Share with people who trade frequently
2. **Explain the Benefits**: They get the same prices, you earn rewards
3. **Be Authentic**: Share your own experience with Nekomancer
4. **Use Multiple Channels**: Twitter, Discord, Telegram, etc.

## FAQ

**Q: Is there a limit to how much I can earn?**
A: No! Earn unlimited rewards from your referrals.

**Q: How long do referral rewards last?**
A: Forever. Once someone uses your code, you earn from all their future swaps.

**Q: Can I see who used my referral?**
A: You can see the count, but individual wallets are private.

**Q: What if someone clears their browser?**
A: The referral is stored on-chain. Once linked, it's permanent.
