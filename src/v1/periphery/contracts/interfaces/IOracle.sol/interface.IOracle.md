# IOracle
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/6ce65434509972d6f67aeab3e318f9db63a09fe0/contracts/interfaces/IOracle.sol)

Quotes oracle related quantities for Marginal v1 pools


## Functions
### sqrtPricesX96

Returns the current pool sqrt price, oracle sqrt price, and the funding rate due to difference between the two


```solidity
function sqrtPricesX96(PoolAddress.PoolKey memory poolKey)
    external
    view
    returns (uint160 sqrtPriceX96, uint160 oracleSqrtPriceX96, uint256 fundingRatioX96);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`poolKey`|`PoolAddress.PoolKey`|The identifying key of the Marginal v1 pool|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`sqrtPriceX96`|`uint160`|The Marginal v1 pool current sqrt price|
|`oracleSqrtPriceX96`|`uint160`|The oracle sqrt price averaged over pool constant `secondsAgo`|
|`fundingRatioX96`|`uint256`|The current instantaneous funding rate over next funding period for long positions on the pool (zeroForOne = false)|


### liquidationSqrtPriceX96

Returns the liquidation sqrt price of an existing position


```solidity
function liquidationSqrtPriceX96(uint256 tokenId) external view returns (uint160);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tokenId`|`uint256`|The NFT token id associated with the position|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint160`|The liquidation sqrt price X96 that oracle must reach for position to be unsafe|


### liquidationSqrtPriceX96

Returns the liquidation sqrt price for given position details


```solidity
function liquidationSqrtPriceX96(bool zeroForOne, uint128 size, uint128 debt, uint128 margin, uint24 maintenance)
    external
    view
    returns (uint160);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`zeroForOne`|`bool`|Whether position settlement requires debt in of token0 for size + margin out of token1|
|`size`|`uint128`|The position size on the pool in the margin token|
|`debt`|`uint128`|The position debt owed to the pool in the non-margin token|
|`margin`|`uint128`|The margin backing the position on the pool|
|`maintenance`|`uint24`|The pool minimum maintenance requirement for leverage positions|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint160`|The liquidation sqrt price X96 that oracle must reach for position to be unsafe|


