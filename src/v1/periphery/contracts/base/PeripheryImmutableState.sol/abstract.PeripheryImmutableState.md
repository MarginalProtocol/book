# PeripheryImmutableState
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/2ce1df3e90c9d2b47899fece944f04a7d78d5b16/contracts/base/PeripheryImmutableState.sol)

**Inherits:**
[IPeripheryImmutableState](/contracts/interfaces/IPeripheryImmutableState.sol/interface.IPeripheryImmutableState.md)

Immutable state used by periphery contracts


## State Variables
### factory

```solidity
address public immutable factory;
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

