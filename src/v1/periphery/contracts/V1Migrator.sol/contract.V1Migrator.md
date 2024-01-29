# V1Migrator
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/252206c9465648eefefe7b978f4e865682332b87/contracts/V1Migrator.sol)

**Inherits:**
[IV1Migrator](/contracts/interfaces/IV1Migrator.sol/interface.IV1Migrator.md), [PeripheryImmutableState](/contracts/base/PeripheryImmutableState.sol/abstract.PeripheryImmutableState.md), Multicall, SelfPermit

Migrates liquidity from Uniswap v3-compatible pairs into Marginal v1 pools


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


```solidity
function _isApprovedOrOwner(address spender, uint256 tokenId) internal view returns (bool);
```

### migrate


```solidity
function migrate(MigrateParams calldata params) external onlyApprovedOrOwner(params.tokenId);
```

## Errors
### Unauthorized

```solidity
error Unauthorized();
```

