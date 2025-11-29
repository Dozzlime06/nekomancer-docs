# Contract Addresses

All Nekomancer smart contracts deployed on Monad Mainnet (Chain 143).

## Core Contracts

### SwapAggregator
The main swap routing contract.

| Property | Value |
|----------|-------|
| Proxy Address | `0x6524822e437dcd23d62c77496d7a0ac980fbc81d` |
| Implementation | `0x19332B438Da14Ac5537d499d7e279f45C8A476c6` |
| Type | UUPS Upgradeable |

### ReferralVault V2
Stores and distributes referral earnings.

| Property | Value |
|----------|-------|
| Proxy Address | `0x28e123cfd53EA9B39BCec297eba161F0742764F2` |
| Implementation | `0x141e636B8601e40c74f02b17114FB54A5030E706` |
| Type | UUPS Upgradeable |

### StakingVault
Manages MANCER staking and reward distribution.

| Property | Value |
|----------|-------|
| Proxy Address | `0x448317114cf3017fb8e2686c000b70c6a75735dc` |
| Implementation | `0x5a232badd59963ddd5d2fcdbe93fd275c565dbb7` |
| Type | UUPS Upgradeable |
| Status | Awaiting MANCER token |

## Fee Recipients

| Recipient | Address | Share |
|-----------|---------|-------|
| Platform | `0xE9059B5f1C60ecf9C1F07ac2bBa148A75394f56e` | 30% |
| Staking Vault | `0x448317114cf3017fb8e2686c000b70c6a75735dc` | 50% |
| Referral Vault | `0x28e123cfd53EA9B39BCec297eba161F0742764F2` | 20% |

## External DEX Routers

| DEX | Router Address |
|-----|----------------|
| Uniswap V2 | `0x4B2ab38DBF28D31D467aA8993f6c2585981D6804` |
| Uniswap V3 SwapRouter02 | `0xfE31F71C1b106EAc32F1A19239c9a9A72ddfb900` |
| Uniswap V3 QuoterV2 | `0x661E93cca42AfacB172121EF892830cA3b70F08d` |
| PancakeSwap V2 | `0xB1Bc24c34e88f7D43D5923034E3a14B24DaACfF9` |
| Nad.Fun Bonding Router | `0x6F6B8F1a20703309951a5127c45B49b1CD981A22` |
| Nad.Fun DEX Router | `0x0B79d71AE99528D1dB24A4148b5f4F865cc2b137` |
| Nad.Fun Lens | `0x7e78A8DE94f21804F7a17F4E8BF9EC2c872187ea` |

## Token Addresses

| Token | Address |
|-------|---------|
| WMON | `0x3bd359C1119dA7Da1D913D1C4D2B7c461115433A` |
| WETH | `0xEE8c0E9f1BFFb4Eb878d8f15f368A02a35481242` |
| USDC | `0x754704Bc059F8C67012fEd69BC8A327a5aafb603` |

## Verifying Contracts

All contracts can be verified on [Monvision Explorer](https://monvision.io):

1. Go to monvision.io
2. Search for the contract address
3. View transactions, code, and events

## Upgrade History

### SwapAggregator
| Version | Implementation | Date |
|---------|---------------|------|
| V32 | `0x19332B438Da14Ac5537d499d7e279f45C8A476c6` | Nov 29, 2025 |
| V31 | `0x831Db236603F0b4c34c47aFc634782D6C5362C50` | Nov 29, 2025 |
| V30 | Previous | Nov 28, 2025 |

### ReferralVault
| Version | Implementation | Date |
|---------|---------------|------|
| V2 | `0x141e636B8601e40c74f02b17114FB54A5030E706` | Nov 29, 2025 |
| V1 | Previous | Nov 29, 2025 |
