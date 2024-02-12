# PeripheryImmutableState
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/1d4c6a63a24ea055be056199b2cac6431f68ec06/contracts/base/PeripheryImmutableState.sol)

**Inherits:**
[IPeripheryImmutableState](/contracts/interfaces/IPeripheryImmutableState.sol/interface.IPeripheryImmutableState.md)

Immutable state used by periphery contracts


## State Variables
### factory

```solidity
address public immutable factory;
```


### deployer

```solidity
address public immutable deployer;
```


### uniswapV3Factory

```solidity
address public immutable uniswapV3Factory;
```


### WETH9

```solidity
address public immutable WETH9;
```


## Functions
### constructor


```solidity
constructor(address _factory, address _WETH9);
```

