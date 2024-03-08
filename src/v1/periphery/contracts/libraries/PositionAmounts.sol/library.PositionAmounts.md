# PositionAmounts
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/6ce65434509972d6f67aeab3e318f9db63a09fe0/contracts/libraries/PositionAmounts.sol)

Calculates liquidity from desired size amounts


## Functions
### getLiquidityForSize

Gets the pool liquidity to be utilized for a given position size


```solidity
function getLiquidityForSize(uint128 liquidity, uint160 sqrtPriceX96, uint24 maintenance, bool zeroForOne, uint128 size)
    internal
    pure
    returns (uint128 liquidityDelta);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`liquidity`|`uint128`|The available liquidity of the pool|
|`sqrtPriceX96`|`uint160`|The sqrt price of the pool|
|`maintenance`|`uint24`|The minimum maintenance requirement of the pool|
|`zeroForOne`|`bool`|Whether long token1 and short token0 (true), or long token0 and short token1 (false)|
|`size`|`uint128`|The desired size of the position in token1 if zeroForOne = true, or token0 if zeroForOne = false|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`liquidityDelta`|`uint128`|The pool liquidity to be utilized|


## Errors
### SizeGreaterThanReserve

```solidity
error SizeGreaterThanReserve(uint256 reserve);
```

