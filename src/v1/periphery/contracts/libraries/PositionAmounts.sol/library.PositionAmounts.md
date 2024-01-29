# PositionAmounts
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/252206c9465648eefefe7b978f4e865682332b87/contracts/libraries/PositionAmounts.sol)


## Functions
### getLiquidityForSize


```solidity
function getLiquidityForSize(uint128 liquidity, uint160 sqrtPriceX96, uint24 maintenance, bool zeroForOne, uint128 size)
    internal
    pure
    returns (uint128 liquidityDelta);
```

## Errors
### SizeGreaterThanReserve

```solidity
error SizeGreaterThanReserve(uint256 reserve);
```

