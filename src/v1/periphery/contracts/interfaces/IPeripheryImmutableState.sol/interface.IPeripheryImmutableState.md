# IPeripheryImmutableState
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/1d4c6a63a24ea055be056199b2cac6431f68ec06/contracts/interfaces/IPeripheryImmutableState.sol)

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


### deployer


```solidity
function deployer() external view returns (address);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|Returns the address of the Marginal V1 deployer|


### WETH9


```solidity
function WETH9() external view returns (address);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|Returns the address of WETH9|


