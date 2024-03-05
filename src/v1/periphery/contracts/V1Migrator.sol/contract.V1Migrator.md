# V1Migrator
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/2ce1df3e90c9d2b47899fece944f04a7d78d5b16/contracts/V1Migrator.sol)

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
### onlyApprovedOrOwner


```solidity
modifier onlyApprovedOrOwner(uint256 tokenId);
```

### constructor


```solidity
constructor(address _factory, address _WETH9, address _marginalV1Router, address _uniswapV3NonfungiblePositionManager)
    PeripheryImmutableState(_factory, _WETH9);
```

### receive


```solidity
receive() external payable;
```

### _isApprovedOrOwner

Checks whether spender authorized to migrate Uniswap v3 liquidity to Marginal v1

*Ref @openzeppelin/v3.4.2-solc-0.7/contracts/token/ERC721/ERC721.sol#L292*


```solidity
function _isApprovedOrOwner(address spender, uint256 tokenId) internal view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`spender`|`address`|The account looking to migrate the Uniswap v3 LP position|
|`tokenId`|`uint256`|The tokenId of the Uniswap v3 LP position to migrate|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether the spender is authorized|


### migrate

Migrates liquidity to Marginal v1 by removing liquidity from Uniswap v3

*Slippage protection is enforced via `amount{0,1}MinToRemove` on Uniswap v3 decrease liquidity
and `amount{0,1}MinToMigrate` on Marginal v1 add liquidity.
Must approve `IV1Migrator` as spender of `params.tokenId` or set approval for all prior to calling migrate.*


```solidity
function migrate(MigrateParams calldata params) external onlyApprovedOrOwner(params.tokenId);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`MigrateParams`|The params necessary to migrate liquidity, encoded as `MigrateParams` in calldata|


## Errors
### Unauthorized

```solidity
error Unauthorized();
```

### LiquidityDeltaGreaterThanMax

```solidity
error LiquidityDeltaGreaterThanMax();
```

