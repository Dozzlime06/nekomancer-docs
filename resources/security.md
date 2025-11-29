# Security

How Nekomancer keeps your funds safe.

## Non-Custodial

Nekomancer never holds your funds:
- Swaps execute directly between you and DEX contracts
- Fees are distributed atomically in the same transaction
- No deposit/withdrawal system

## Smart Contract Security

### UUPS Upgradeable
All core contracts use UUPS proxy pattern:
- Owner-only upgrades
- Implementation can be patched for bugs
- Proxy address never changes

### OpenZeppelin
Built with battle-tested OpenZeppelin libraries:
- `OwnableUpgradeable` - access control
- `ReentrancyGuardUpgradeable` - prevents reentrancy
- `SafeERC20` - safe token transfers

### Security Features
- NonReentrant on all swap functions
- Slippage protection with minimum output
- Deadline enforcement on swaps
- No admin functions that can steal funds

## Wallet Security

### Best Practices
1. **Verify URLs**: Always check you're on `nekomancer.fun`
2. **Check Transactions**: Review swap details before confirming
3. **Token Approvals**: Only approve what you need
4. **Revoke Old Approvals**: Clean up unused approvals

### What We Can't Access
- Your private keys
- Your seed phrase
- Your funds without your approval

## Contract Addresses

Only interact with official contracts:

| Contract | Address |
|----------|---------|
| SwapAggregator | `0x6524822e437dcd23d62c77496d7a0ac980fbc81d` |
| ReferralVault | `0x28e123cfd53EA9B39BCec297eba161F0742764F2` |
| StakingVault | `0x448317114cf3017fb8e2686c000b70c6a75735dc` |

## Common Scams to Avoid

### Fake Tokens
- Always verify token addresses
- Scam tokens may have similar names
- Check on block explorer before trading

### Phishing Sites
- Bookmark the official site
- Never enter seed phrase anywhere
- Verify URL before connecting wallet

### Fake Support
- We will never DM you first
- We will never ask for private keys
- Only trust official channels

## Reporting Issues

Found a security issue? Report responsibly to help protect all users.

## Audits

Smart contract audits: Coming soon

## On-Chain Transparency

Everything is verifiable on [monvision.io](https://monvision.io):
- All swap transactions
- Fee distributions
- Contract source code
- Admin transactions
