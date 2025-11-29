# Changelog

All notable updates to Nekomancer.

## November 29, 2025

### SwapAggregator
- **New**: ReferralVault integration
- **New**: WithReferral swap functions
- **New**: 30/20/50 fee split (platform/referral/staking)
- **Fix**: feeBps storage corruption resolved

### ReferralVault V2
- **New**: Minimum claim amount (~$10 USD)
- **New**: Referral count tracking
- **New**: Emergency withdraw function
- **Improved**: Better error handling

## November 28, 2025

### SwapAggregatorV31
- **Fix**: DEX Router returns native MON, not WMON
- **Improved**: Balance tracking for graduated token sales

### SwapAggregatorV30
- **New**: Multi-hop routing
- **New**: Split routing across DEXes
- **New**: Multi-recipient fee distribution

## November 27, 2025

### SwapAggregatorV27
- **Fix**: InvalidAmountOut on DEX Router
- **Improved**: Pass minOut to router correctly
- **Improved**: Slippage protection after swap

### SwapAggregatorV26
- **New**: DEX Router standard ERC20 approval
- **Improved**: Graduated Nad.Fun token routing

## November 26, 2025

### Initial Deployment
- SwapAggregatorV4 with UUPS proxy
- StakingVault deployed
- Uniswap V2, V3, PancakeSwap support
- Nad.Fun integration
- 1% fee with 50/50 split

---

## Upcoming

### MANCER Token
- Token deployment on Monad
- Staking activation
- Governance features

### Additional DEXes
- More DEX integrations as they launch on Monad

### Mobile App
- Native iOS/Android apps (planned)
