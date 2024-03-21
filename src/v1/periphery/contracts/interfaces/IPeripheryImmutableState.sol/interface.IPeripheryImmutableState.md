# IPeripheryImmutableState
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/de728cd3d633f080a3fd40108fe8de3ab4edd595/contracts/interfaces/IPeripheryImmutableState.sol)

Functions that return immutable state of the router


## Functions
### factory


```solidity
function factory() external view returns (address);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|Returns the address of the Marginal V1 factory|


### uniswapV3Factory


```solidity
function uniswapV3Factory() external view returns (address);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|Returns the address of the Uniswap V3 factory|


### WETH9


```solidity
function WETH9() external view returns (address);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|Returns the address of WETH9|


