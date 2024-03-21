# LiquidityMath
[Git Source](https://github.com/MarginalProtocol/v1-core/blob/4dcf410464dd1b73aaabe9fa06bd3450c672d3b9/contracts/libraries/LiquidityMath.sol)

Facilitates transformations between (L, sqrtP) space and (x, y) token reserves


## Functions
### toAmounts

Transforms (L, sqrtP) values into (x, y) reserve amounts


```solidity
function toAmounts(uint128 liquidity, uint160 sqrtPriceX96) internal pure returns (uint256 amount0, uint256 amount1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`liquidity`|`uint128`|Pool liquidity in (L, sqrtP) space|
|`sqrtPriceX96`|`uint160`|Pool price in (L, sqrtP) space|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount0`|`uint256`|The amount of token0 associated with the given (L, sqrtP) values|
|`amount1`|`uint256`|The amount of token1 associated with the given (L, sqrtP) values|


### toLiquiditySqrtPriceX96

Transforms (x, y) reserve amounts into (L, sqrtP) values

*Reverts on overflow if reserve0 * reserve1 > type(uint256).max as liquidity must fit into uint128*


```solidity
function toLiquiditySqrtPriceX96(uint256 reserve0, uint256 reserve1)
    internal
    pure
    returns (uint128 liquidity, uint160 sqrtPriceX96);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`reserve0`|`uint256`|The amount of token0 in reserves|
|`reserve1`|`uint256`|The amount of token1 in reserves|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`liquidity`|`uint128`|Pool liquidity associated with reserve amounts|
|`sqrtPriceX96`|`uint160`|Pool price associated with reserve amounts|


### liquiditySqrtPriceX96Next

Calculates (L, sqrtP) after adding/removing amounts to/from pool reserves


```solidity
function liquiditySqrtPriceX96Next(uint128 liquidity, uint160 sqrtPriceX96, int256 amount0, int256 amount1)
    internal
    pure
    returns (uint128 liquidityNext, uint160 sqrtPriceX96Next);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`liquidity`|`uint128`|Pool liquidity before adding/removing reserves|
|`sqrtPriceX96`|`uint160`|Pool price before adding/removing reserves|
|`amount0`|`int256`|The amount of token0 to add (positive) or remove (negative)|
|`amount1`|`int256`|The amount of token1 to add (positive) or remove (negative)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`liquidityNext`|`uint128`|Pool liquidity after adding/removing reserves|
|`sqrtPriceX96Next`|`uint160`|Pool price after adding/removing reserves|


