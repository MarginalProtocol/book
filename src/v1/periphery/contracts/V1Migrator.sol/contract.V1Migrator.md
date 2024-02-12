# V1Migrator
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/1d4c6a63a24ea055be056199b2cac6431f68ec06/contracts/V1Migrator.sol)

**Inherits:**
[IV1Migrator](/contracts/interfaces/IV1Migrator.sol/interface.IV1Migrator.md), [PeripheryImmutableState](/contracts/base/PeripheryImmutableState.sol/abstract.PeripheryImmutableState.md), Multicall

Migrates liquidity from Uniswap v3-compatible pairs into Marginal v1 pools

*Fork of Uniswap v3 migrator adapted to Marginal v1*


## State Variables
### marginalV1Router

```solidity
address public immutable marginalV1Router;
```


### uniswapV3NonfungiblePositionManager

```solidity
address public immutable uniswapV3NonfungiblePositionManager;
```


## Functions
### constructor


```solidity
constructor(address _factory, address _WETH9, address _marginalV1Router, address _uniswapV3NonfungiblePositionManager)
    PeripheryImmutableState(_factory, _WETH9);
```

### receive


```solidity
receive() external payable;
```

### migrate

Migrates liquidity to Marginal v1 by removing liquidity from Uniswap v3

*Slippage protection is enforced via `amount{0,1}MinToRemove` on Uniswap v3 decrease liquidity
and `amount{0,1}MinToMigrate` on Marginal v1 add liquidity.
Must approve `IV1Migrator` as spender of `params.tokenId` or set approval for all prior to calling migrate.*


```solidity
function migrate(MigrateParams calldata params) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`MigrateParams`|The params necessary to migrate liquidity, encoded as `MigrateParams` in calldata|


## Errors
### LiquidityDeltaGreaterThanMax

```solidity
error LiquidityDeltaGreaterThanMax();
```

