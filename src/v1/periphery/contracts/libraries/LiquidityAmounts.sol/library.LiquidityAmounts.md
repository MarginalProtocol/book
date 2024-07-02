# LiquidityAmounts
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/d846d56fa6d1e439306e60a85e98fc298babb2f7/contracts/libraries/LiquidityAmounts.sol)

Calculates liquidity from desired reserve amounts


## Functions
### getLiquidityForAmount0

Gets the pool liquidity contribution for a given amount of token0


```solidity
function getLiquidityForAmount0(uint160 sqrtPriceX96, uint256 amount0) internal pure returns (uint128);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sqrtPriceX96`|`uint160`|The sqrt price of the pool|
|`amount0`|`uint256`|The amount of token0|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint128`|The liquidity contribution|


### getLiquidityForAmount1

Gets the pool liquidity contribution for a given amount of token1


```solidity
function getLiquidityForAmount1(uint160 sqrtPriceX96, uint256 amount1) internal pure returns (uint128);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sqrtPriceX96`|`uint160`|The sqrt price of the pool|
|`amount1`|`uint256`|The amount of token1|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint128`|The liquidity contribution|


### getLiquidityForAmounts

Gets the pool liquidity contribution for given amounts of token0 and token1

*Takes the minimum of contributions from either token0 or token1*


```solidity
function getLiquidityForAmounts(uint160 sqrtPriceX96, uint256 amount0, uint256 amount1)
    internal
    pure
    returns (uint128 liquidity);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sqrtPriceX96`|`uint160`|The sqrt price of the pool|
|`amount0`|`uint256`|The amount of token0|
|`amount1`|`uint256`|The amount of token1|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`liquidity`|`uint128`|The liquidity contribution|


