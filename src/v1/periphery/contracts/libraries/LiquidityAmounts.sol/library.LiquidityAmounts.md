# LiquidityAmounts
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/252206c9465648eefefe7b978f4e865682332b87/contracts/libraries/LiquidityAmounts.sol)


## Functions
### getLiquidityForAmount0


```solidity
function getLiquidityForAmount0(uint160 sqrtPriceX96, uint256 amount0) internal pure returns (uint128);
```

### getLiquidityForAmount1


```solidity
function getLiquidityForAmount1(uint160 sqrtPriceX96, uint256 amount1) internal pure returns (uint128);
```

### getLiquidityForAmounts


```solidity
function getLiquidityForAmounts(uint160 sqrtPriceX96, uint256 amount0, uint256 amount1)
    internal
    pure
    returns (uint128 liquidity);
```

