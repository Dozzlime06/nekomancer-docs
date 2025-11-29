# Staking Rewards

> **Status: Coming Soon** - Awaiting MANCER token launch

Stake MANCER tokens to earn 50% of all platform swap fees.

## Overview

The Staking system allows MANCER token holders to:
- Stake tokens to earn passive income
- Receive 50% of all swap fees in MON
- Participate in platform governance (future)

## How It Will Work

### Staking Process
1. Acquire MANCER tokens
2. Go to the Staking page
3. Approve MANCER for staking
4. Stake your tokens
5. Earn rewards automatically

### Unstaking
- **Standard Unstake**: 3-day waiting period
  - Request unstake
  - Wait 3 days
  - Withdraw tokens + rewards
  
- **Emergency Unstake**: Immediate but with penalty
  - 20% of staked tokens burned
  - No waiting period
  - Forfeit pending rewards

## Reward Distribution

### Fee Split
| Recipient | Share |
|-----------|-------|
| Platform | 30% |
| Referrals | 20% |
| **Stakers** | **50%** |

### Reward Calculation
Rewards are distributed proportionally based on:
- Your staked amount ÷ Total staked = Your share
- Distributed in MON (native Monad token)

### Example
- Total staked: 10,000,000 MANCER
- Your stake: 100,000 MANCER (1%)
- Daily swap volume: 1,000,000 MON
- Daily fees: 10,000 MON (1%)
- Staking pool: 5,000 MON (50%)
- Your daily reward: 50 MON (1% of pool)

## Requirements

### Minimum Stake
- 100,000 MANCER tokens

### Lock Period
- No lock period for staking
- 3-day delay for standard unstaking

## StakingVault Contract

| Property | Value |
|----------|-------|
| Address | `0x448317114cf3017fb8e2686c000b70c6a75735dc` |
| Type | UUPS Upgradeable |
| Status | Deployed, awaiting MANCER token |

### Contract Functions
- `stake(amount)` - Stake MANCER tokens
- `requestUnstake(amount)` - Start 3-day unstake
- `withdraw()` - Complete unstake after delay
- `emergencyUnstake()` - Immediate unstake with 20% burn
- `claimRewards()` - Claim pending MON rewards
- `pendingRewards(address)` - View pending rewards

## FAQ

**Q: When will staking launch?**
A: After the MANCER token is deployed on Monad.

**Q: What token do I stake?**
A: MANCER token (address TBA).

**Q: What do I earn?**
A: MON (native Monad token) from swap fees.

**Q: Is there a lock period?**
A: No lock, but 3-day delay when unstaking.

**Q: Can I lose my staked tokens?**
A: Only if you use emergency unstake (20% burn).

## Stay Updated

Staking launch will be announced on our official channels.
