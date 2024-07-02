# CallbackValidation
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/d846d56fa6d1e439306e60a85e98fc298babb2f7/contracts/libraries/CallbackValidation.sol)

Provides validation for callbacks from Marginal V1 Pools

*Fork of Uniswap V3 periphery CallbackValidation.sol*


## Functions
### verifyCallback

Returns the address of a valid Marginal V1 Pool


```solidity
function verifyCallback(address factory, address tokenA, address tokenB, uint24 maintenance, address oracle)
    internal
    view
    returns (IMarginalV1Pool pool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`factory`|`address`|The contract address of the Marginal V1 factory|
|`tokenA`|`address`|The contract address of either token0 or token1|
|`tokenB`|`address`|The contract address of the other token|
|`maintenance`|`uint24`|The maintenance requirements of the pool|
|`oracle`|`address`|The contract address of the oracle referenced by the pool|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`pool`|`IMarginalV1Pool`|The V1 pool contract address|


### verifyCallback

Returns the address of a valid Marginal V1 Pool


```solidity
function verifyCallback(address factory, PoolAddress.PoolKey memory poolKey)
    internal
    view
    returns (IMarginalV1Pool pool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`factory`|`address`|The contract address of the Marginal V1 factory|
|`poolKey`|`PoolAddress.PoolKey`|The identifying key of the V1 pool|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`pool`|`IMarginalV1Pool`|The V1 pool contract address|


### verifyUniswapV3Callback

Returns the address of a valid Uniswap V3 Pool


```solidity
function verifyUniswapV3Callback(address factory, PoolAddress.PoolKey memory poolKey)
    internal
    view
    returns (IUniswapV3Pool uniswapV3Pool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`factory`|`address`|The contract address of the Marginal V1 factory|
|`poolKey`|`PoolAddress.PoolKey`|The identifying key of the V1 pool|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`uniswapV3Pool`|`IUniswapV3Pool`|The Uniswap V3 pool oracle address associated with the V1 pool|


## Errors
### PoolNotSender

```solidity
error PoolNotSender();
```

### OracleNotSender

```solidity
error OracleNotSender();
```

