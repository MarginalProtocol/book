# PositionAmounts
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/2ce1df3e90c9d2b47899fece944f04a7d78d5b16/contracts/libraries/PositionAmounts.sol)


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

