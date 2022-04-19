# MultiFarm LP Token Vault

Forked from @fubuloubu's reference Vyper ERC4626 implementation

See [EIP-4626](https://eips.ethereum.org/EIPS/eip-4626) for more details.

Implements farming for the same token pair, across multiple DEXes.

Supports arbitraging the prices between supported dexes for additional yield (implementation details TBD)


# How It Works

The vault suppports farming a specific pair of tokens across two or more masterchef farming contracts.

Rather than expecting a specific DEX's LP token, the vault can accept any supported LP token for the given pair, 
and internally perform the necessary liquidity pulls/provisions to farm optimally.
For example, a vault for ETH-USDC would accept either Sushiswap or Uniswap LP tokens. If necessary or optimal, 
it can convert deposited LP tokens from one to the other. The vault will then have a portion of funds farming each supported DEX.

When prices between supported DEXes deviate, the vault should support arbitraging of the price for vault profit.
This profit should be shared with the caller of the arbitrage function to reward them for capitalizing on the opportunity
on behalf of the vault's users. This allows decentralized management of vault assets across DEXes, when profitable.

## Major Points To Be Figured Out

* Virtual LP Price: 1 LP from dex A != 1 LP from dex B, but for liquid enough pairs, we can assume the ratios between these will be mostly constant

