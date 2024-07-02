# Oracle
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/d846d56fa6d1e439306e60a85e98fc298babb2f7/contracts/lens/Oracle.sol)

**Inherits:**
[IOracle](/contracts/interfaces/IOracle.sol/interface.IOracle.md), [PeripheryImmutableState](/contracts/base/PeripheryImmutableState.sol/abstract.PeripheryImmutableState.md), [PositionState](/contracts/base/PositionState.sol/abstract.PositionState.md), Multicall

Quotes oracle related quantities for Marginal v1 pools


## State Variables
### manager

```solidity
INonfungiblePositionManager public immutable manager;
```


## Functions
### constructor


```solidity
constructor(address _factory, address _WETH9, address _manager) PeripheryImmutableState(_factory, _WETH9);
```

### getPool

*Returns the pool for the given token pair and maintenance. The pool contract may or may not exist.*


```solidity
function getPool(PoolAddress.PoolKey memory poolKey) internal view returns (IMarginalV1Pool);
```

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

Returns the liquidation sqrt price of an existing position


```solidity
function liquidationSqrtPriceX96(bool zeroForOne, uint128 size, uint128 debt, uint128 margin, uint24 maintenance)
    public
    pure
    returns (uint160);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`zeroForOne`|`bool`||
|`size`|`uint128`||
|`debt`|`uint128`||
|`margin`|`uint128`||
|`maintenance`|`uint24`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint160`|The liquidation sqrt price X96 that oracle must reach for position to be unsafe|


