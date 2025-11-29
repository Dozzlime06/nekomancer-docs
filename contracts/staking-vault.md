# StakingVault

Smart contract for MANCER token staking and reward distribution.

> **Status**: Deployed and awaiting MANCER token launch

## Overview

StakingVault is a UUPS upgradeable contract that:
- Accepts MANCER token stakes
- Receives 50% of swap fees as rewards
- Distributes rewards proportionally to stakers
- Enforces unstaking delays and burn penalties

## Contract Details

| Property | Value |
|----------|-------|
| Proxy | `0x448317114cf3017fb8e2686c000b70c6a75735dc` |
| Implementation | `0x5a232badd59963ddd5d2fcdbe93fd275c565dbb7` |
| Network | Monad Mainnet (Chain 143) |
| Status | Awaiting MANCER token |

## Configuration

| Parameter | Value |
|-----------|-------|
| Minimum Stake | 100,000 MANCER |
| Unstake Delay | 3 days |
| Emergency Burn | 20% |
| Reward Token | MON (native) |

## How It Works

### Staking Flow
1. User approves MANCER tokens
2. User calls `stake(amount)`
3. Tokens transferred to vault
4. User starts earning rewards

### Reward Distribution
1. Swap fees sent to vault (50% of total)
2. Rewards accumulate in vault
3. Users claim proportional share
4. Rewards paid in MON

### Unstaking (Standard)
1. User calls `requestUnstake(amount)`
2. Wait 3 days
3. Call `withdraw()` to receive tokens + rewards

### Unstaking (Emergency)
1. User calls `emergencyUnstake()`
2. Receive 80% of tokens immediately
3. 20% burned to dead address
4. Forfeit pending rewards

## Functions

### User Functions

#### stake
```solidity
function stake(uint256 amount) external
```
Stake MANCER tokens. Minimum 100,000 tokens.

#### requestUnstake
```solidity
function requestUnstake(uint256 amount) external
```
Request to unstake. Starts 3-day countdown.

#### withdraw
```solidity
function withdraw() external
```
Complete unstake after delay. Receive tokens + rewards.

#### emergencyUnstake
```solidity
function emergencyUnstake() external
```
Immediate unstake with 20% burn penalty.

#### claimRewards
```solidity
function claimRewards() external
```
Claim pending MON rewards without unstaking.

### View Functions

#### stakedBalance
```solidity
function stakedBalance(address user) external view returns (uint256)
```
Get staked amount for user.

#### pendingRewards
```solidity
function pendingRewards(address user) external view returns (uint256)
```
Get claimable MON rewards.

#### totalStaked
```solidity
function totalStaked() external view returns (uint256)
```
Total MANCER staked in vault.

#### unstakeRequest
```solidity
function unstakeRequest(address user) external view returns (
    uint256 amount,
    uint256 unlockTime
)
```
Get pending unstake request details.

### Admin Functions

#### setStakingToken
```solidity
function setStakingToken(address token) external onlyOwner
```
Set MANCER token address (one-time setup).

#### setMinimumStake
```solidity
function setMinimumStake(uint256 amount) external onlyOwner
```
Update minimum stake requirement.

## Events

```solidity
event Staked(address indexed user, uint256 amount);
event UnstakeRequested(address indexed user, uint256 amount, uint256 unlockTime);
event Withdrawn(address indexed user, uint256 amount, uint256 rewards);
event EmergencyUnstake(address indexed user, uint256 received, uint256 burned);
event RewardsClaimed(address indexed user, uint256 amount);
event RewardsReceived(uint256 amount);
```

## Reward Calculation

```
userReward = (userStake / totalStaked) * rewardPool
```

Example:
- Total staked: 10,000,000 MANCER
- Your stake: 100,000 MANCER (1%)
- Reward pool: 1,000 MON
- Your reward: 10 MON

## Integration

### Receiving Fees
The vault has a `receive()` function that accepts MON from SwapAggregator.

```solidity
receive() external payable {
    emit RewardsReceived(msg.value);
}
```

### From Frontend
```javascript
// Stake tokens
await mancerToken.approve(stakingVault, amount);
await stakingVault.stake(amount);

// Check rewards
const pending = await stakingVault.pendingRewards(address);

// Claim rewards
await stakingVault.claimRewards();
```

## Security

- Reentrancy guards on all state-changing functions
- 3-day delay prevents flash loan attacks
- 20% emergency burn discourages gaming
- Owner-only admin functions
