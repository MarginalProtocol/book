# IMarginalV1Factory
[Git Source](https://github.com/MarginalProtocol/v1-core/blob/4dcf410464dd1b73aaabe9fa06bd3450c672d3b9/contracts/interfaces/IMarginalV1Factory.sol)

The Marginal v1 factory creates pools and enables leverage tiers


## Functions
### marginalV1Deployer

Returns the Marginal v1 pool deployer to use when creating pools


```solidity
function marginalV1Deployer() external view returns (address);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the Marginal v1 pool deployer|


### uniswapV3Factory

Returns the Uniswap v3 factory to reference for pool oracles


```solidity
function uniswapV3Factory() external view returns (address);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the Uniswap v3 factory|


### observationCardinalityMinimum

Returns the minimum observation cardinality the Uniswap v3 oracle must have

*Used as a check that averaging over `secondsAgo` in the Marginal v1 pool is likely to succeed*


```solidity
function observationCardinalityMinimum() external view returns (uint16);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint16`|The minimum observation cardinality the Uniswap v3 oracle must have|


### owner

Returns the current owner of the Marginal v1 factory contract

*Changed via permissioned `setOwner` function on the factory*


```solidity
function owner() external view returns (address);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the current owner of the Marginal v1 factory|


### getPool

Returns the pool address for the given unique Marginal v1 pool key

*tokenA and tokenB may be passed in either token0/token1 or token1/token0 order*


```solidity
function getPool(address tokenA, address tokenB, uint24 maintenance, address oracle) external view returns (address);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tokenA`|`address`|The address of either token0/token1|
|`tokenB`|`address`|The address of the other token token1/token0|
|`maintenance`|`uint24`|The minimum maintenance requirement for the pool|
|`oracle`|`address`|The address of the Uniswap v3 oracle used by the pool|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the Marginal v1 pool|


### isPool

Returns whether given address is a Marginal v1 pool deployed by the factory


```solidity
function isPool(address pool) external view returns (bool);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether address is a pool|


### getLeverage

Returns the maximum leverage associated with the pool maintenance if pool exists


```solidity
function getLeverage(uint24 maintenance) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`maintenance`|`uint24`|The minimum maintenance margin requirement for the pool|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The maximum leverage for the pool maintenance if pool exists|


### createPool

Creates a new Marginal v1 pool for the given unique pool key

*tokenA and tokenB may be passed in either token0/token1 or token1/token0 order*


```solidity
function createPool(address tokenA, address tokenB, uint24 maintenance, uint24 uniswapV3Fee)
    external
    returns (address pool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tokenA`|`address`|The address of either token0/token1|
|`tokenB`|`address`|The address of the other token token1/token0|
|`maintenance`|`uint24`|The minimum maintenance requirement for the pool|
|`uniswapV3Fee`|`uint24`|The fee tier of the Uniswap v3 oracle used by the Marginal v1 pool|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`pool`|`address`|The address of the created Marginal v1 pool|


### setOwner

Sets the owner of the Marginal v1 factory contract

*Can only be called by the current factory owner*


```solidity
function setOwner(address _owner) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`_owner`|`address`|The new owner of the factory|


### enableLeverage

Enables a new leverage tier for Marginal v1 pool deployments

*Can only be called by the current factory owner*

*Set leverage tier obeys: l = 1 + 1/M; M = maintenance*


```solidity
function enableLeverage(uint24 maintenance) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`maintenance`|`uint24`|The minimum maintenance requirement associated with the leverage tier|


