# IV1Migrator
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/252206c9465648eefefe7b978f4e865682332b87/contracts/interfaces/IV1Migrator.sol)

Migrates liquidity from Uniswap v3-compatible pairs into Marginal v1 pools


## Functions
### migrate

Migrates liquidity to Marginal v1 by removing liquidity from Uniswap v3

*Slippage protection is enforced via `amount{0,1}Min`, which should be a discount of the expected values of
the maximum amount of Marginal v1 liquidity that the Uniswap v3 liquidity can get.*


```solidity
function migrate(MigrateParams calldata params) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`MigrateParams`|The params necessary to migrate liquidity, encoded as `MigrateParams` in calldata|


## Structs
### MigrateParams

```solidity
struct MigrateParams {
    uint256 tokenId;
    uint128 liquidityToMigrate;
    address token0;
    address token1;
    uint24 maintenance;
    address oracle;
    uint256 amount0Min;
    uint256 amount1Min;
    address recipient;
    uint256 deadline;
    bool refundAsETH;
}
```

