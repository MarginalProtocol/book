# SqrtPriceMath
[Git Source](https://github.com/MarginalProtocol/v1-core/blob/2d246e9b4f6e970321a0f235176b47b340c9a03b/contracts/libraries/SqrtPriceMath.sol)

Determines sqrt price changes after a opening leverage position and swapping on the pool


## State Variables
### MIN_SQRT_RATIO
*Adopts Uni V3 tick limits of (-887272, 887272)*


```solidity
uint160 internal constant MIN_SQRT_RATIO = 4295128739;
```


### MAX_SQRT_RATIO

```solidity
uint160 internal constant MAX_SQRT_RATIO = 1461446703485210103287273052203988822378723970342;
```


## Functions
### sqrtPriceX96NextOpen

Calculates sqrtP after opening a leverage position

*Choice of insurance function made in this function*


```solidity
function sqrtPriceX96NextOpen(
    uint128 liquidity,
    uint160 sqrtPriceX96,
    uint128 liquidityDelta,
    bool zeroForOne,
    uint24 maintenance
) internal pure returns (uint160);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`liquidity`|`uint128`|Pool liquidity before opening the position|
|`sqrtPriceX96`|`uint160`|Pool price before opening the position|
|`liquidityDelta`|`uint128`|Liquidity removed from pool to collateralize position|
|`zeroForOne`|`bool`|Whether long token1 and short token0 (true), or long token0 and short token1 (false)|
|`maintenance`|`uint24`|Minimum maintenance margin for the pool|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint160`|The price after opening the position|


### sqrtPriceX96NextSwap

Calculates sqrtP after swapping tokens

*Assumes amountSpecified != 0*


```solidity
function sqrtPriceX96NextSwap(uint128 liquidity, uint160 sqrtPriceX96, bool zeroForOne, int256 amountSpecified)
    internal
    pure
    returns (uint160);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`liquidity`|`uint128`|Pool liquidity before swapping|
|`sqrtPriceX96`|`uint160`|Pool price before swapping|
|`zeroForOne`|`bool`|Whether swapping token0 for token1 (true), or token1 for token0 (false)|
|`amountSpecified`|`int256`|The amount of the swap, which implicitly configures the swap as exact input (positive), or exact output (negative)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint160`|The price after swapping|


## Errors
### InvalidSqrtPriceX96

```solidity
error InvalidSqrtPriceX96();
```

### Amount0ExceedsReserve0

```solidity
error Amount0ExceedsReserve0();
```

### Amount1ExceedsReserve1

```solidity
error Amount1ExceedsReserve1();
```

