# Frequently Asked Questions

## General

### What is Nekomancer?
Nekomancer is a DEX aggregator on Monad that finds the best swap prices across multiple decentralized exchanges.

### What is Monad?
Monad is a high-performance EVM-compatible blockchain with fast transactions and low fees.

### Is Nekomancer safe to use?
Yes. All swaps happen through audited smart contracts. We never have custody of your funds.

### What wallets work with Nekomancer?
Any EVM-compatible wallet: MetaMask, OKX Wallet, Rabby, Trust Wallet, etc.

## Swapping

### Why is Nekomancer better than using a DEX directly?
We compare prices across all DEXes and find the best route. Large trades may be split across multiple DEXes for better execution.

### What tokens can I swap?
Any ERC-20 token on Monad with liquidity on our supported DEXes.

### What's the fee?
1% platform fee on each swap. This includes routing through multiple DEXes and supports referral/staking rewards.

### Why did my swap fail?
Common reasons:
- Slippage too low (price moved)
- Insufficient balance
- Token approval needed
- Price impact too high

Try increasing slippage or reducing swap size.

### What's slippage?
Slippage is the maximum price change you'll accept. Default is 0.5%. Increase for volatile tokens.

### Why do I need to approve tokens?
ERC-20 tokens require approval before a contract can spend them. This is a one-time setup per token.

## Referrals

### How do I create a referral link?
Go to [nekomancer.fun/referral](https://www.nekomancer.fun/referral), connect wallet, and click "Generate Code".

### How much do I earn per referral?
20% of the 1% platform fee. If someone swaps 1000 MON, you earn 2 MON.

### When can I claim my earnings?
When your balance reaches ~$10 USD worth of MON.

### Are referral earnings permanent?
Yes! Once someone uses your code, you earn from all their future swaps forever.

### Can I use my own referral code?
No, you cannot refer yourself.

## Staking

### When does staking launch?
After the MANCER token is deployed on Monad.

### What do I earn from staking?
50% of all platform swap fees, paid in MON.

### What's the minimum stake?
100,000 MANCER tokens.

### Can I unstake anytime?
Yes, but there's a 3-day waiting period. Emergency unstake is instant but burns 20%.

## Technical

### What chain is this on?
Monad Mainnet (Chain ID: 143)

### What's the RPC URL?
`https://rpc3.monad.xyz/`

### Where can I see my transactions?
[monvision.io](https://monvision.io)

### Are the contracts upgradeable?
Yes, using UUPS proxy pattern. Only the owner can upgrade.

## Troubleshooting

### "Network not supported"
Switch to Monad Mainnet in your wallet.

### "Insufficient balance"
Make sure you have enough tokens + gas (MON).

### "Transaction pending forever"
Monad transactions are usually instant. If stuck, check the explorer or try again.

### "Price impact too high"
Try a smaller swap amount or wait for more liquidity.

### Wallet won't connect
1. Refresh the page
2. Make sure wallet extension is unlocked
3. Try a different browser
4. Clear cache and try again

## Contact

Need more help? Join our community channels for support.
