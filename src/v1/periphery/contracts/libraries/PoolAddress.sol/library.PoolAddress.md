# PoolAddress
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/3831eb0dc9ad872eeb8a0eb98bd8566331443136/contracts/libraries/PoolAddress.sol)

*Fork of Uniswap V3 periphery PoolAddress.sol*


## Functions
### getPoolKey

Returns PoolKey: the ordered tokens with the matched fee levels


```solidity
function getPoolKey(address tokenA, address tokenB, uint24 maintenance, address oracle)
    internal
    pure
    returns (PoolKey memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tokenA`|`address`|The first token of a pool, unsorted|
|`tokenB`|`address`|The second token of a pool, unsorted|
|`maintenance`|`uint24`|The maintenance level of the pool|
|`oracle`|`address`|The contract address of the oracle referenced by the pool|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`PoolKey`|PoolKey The pool details with ordered token0 and token1 assignments|


### getAddress

Gets the pool address from factory given pool key

*Reverts if pool not created yet*


```solidity
function getAddress(address factory, PoolKey memory key) internal view returns (address pool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`factory`|`address`|The factory contract address|
|`key`|`PoolKey`|The pool key|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`pool`|`address`|The contract address of the pool|


### isPool

Checks factory for whether `pool` is a valid pool


```solidity
function isPool(address factory, address pool) internal view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`factory`|`address`|The factory contract address|
|`pool`|`address`|The contract address to check whether is a pool|


## Errors
### PoolInactive

```solidity
error PoolInactive();
```

## Structs
### PoolKey
The identifying key of the pool


```solidity
struct PoolKey {
    address token0;
    address token1;
    uint24 maintenance;
    address oracle;
}
```

