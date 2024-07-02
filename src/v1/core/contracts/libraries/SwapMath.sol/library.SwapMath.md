# SwapMath
[Git Source](https://github.com/MarginalProtocol/v1-core/blob/2d246e9b4f6e970321a0f235176b47b340c9a03b/contracts/libraries/SwapMath.sol)

Determines amounts involved in swaps


## Functions
### swapAmounts

Computes amounts in and out on swap without fees

*amount > 0 is amountIn, amount < 0 is amountOut*


```solidity
function swapAmounts(uint128 liquidity, uint160 sqrtPriceX96, uint160 sqrtPriceX96Next)
    internal
    pure
    returns (int256 amount0Delta, int256 amount1Delta);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`liquidity`|`uint128`|Pool liquidity before the swap|
|`sqrtPriceX96`|`uint160`|Pool price at the start of the swap|
|`sqrtPriceX96Next`|`uint160`|Pool price at the end of the swap|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount0Delta`|`int256`|The delta in token0 balance for the pool|
|`amount1Delta`|`int256`|The delta in token1 balance for the pool|


### swapFees

Computes swap fee on amount in

*Can revert when amount > type(uint232).max, but irrelevant for SwapMath.sol::swapAmounts output and pool fee rate constant*


```solidity
function swapFees(uint256 amount, uint24 fee, bool lessFee) internal pure returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amount`|`uint256`|Amount in to calculate swap fees off of|
|`fee`|`uint24`|Fee rate applied on amount in to pool|
|`lessFee`|`bool`|Whether `amount` excludes swap fee amount|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|Total swap fees taken from amount in to pool|


