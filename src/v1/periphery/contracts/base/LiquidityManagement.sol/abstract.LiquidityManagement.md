# LiquidityManagement
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/252206c9465648eefefe7b978f4e865682332b87/contracts/base/LiquidityManagement.sol)

**Inherits:**
IMarginalV1MintCallback, [PeripheryImmutableState](/contracts/base/PeripheryImmutableState.sol/abstract.PeripheryImmutableState.md), [PeripheryPayments](/contracts/base/PeripheryPayments.sol/abstract.PeripheryPayments.md)


## Functions
### getPool

*Returns the pool for the given token pair and maintenance. The pool contract may or may not exist.*


```solidity
function getPool(PoolAddress.PoolKey memory poolKey) internal view returns (IMarginalV1Pool);
```

### mint

Mints liquidity on pool


```solidity
function mint(MintParams memory params) internal virtual returns (uint256 shares, uint256 amount0, uint256 amount1);
```

### marginalV1MintCallback


```solidity
function marginalV1MintCallback(uint256 amount0Owed, uint256 amount1Owed, bytes calldata data) external virtual;
```

### burn

Burns liquidity on pool


```solidity
function burn(BurnParams memory params)
    internal
    virtual
    returns (uint128 liquidityDelta, uint256 amount0, uint256 amount1);
```

## Errors
### Amount0LessThanMin

```solidity
error Amount0LessThanMin(uint256 amount0);
```

### Amount1LessThanMin

```solidity
error Amount1LessThanMin(uint256 amount1);
```

## Structs
### LiquidityCallbackData

```solidity
struct LiquidityCallbackData {
    PoolAddress.PoolKey poolKey;
    address payer;
}
```

### MintParams

```solidity
struct MintParams {
    address token0;
    address token1;
    uint24 maintenance;
    address oracle;
    address recipient;
    uint128 liquidityDelta;
    uint256 amount0Min;
    uint256 amount1Min;
}
```

### BurnParams

```solidity
struct BurnParams {
    address token0;
    address token1;
    uint24 maintenance;
    address oracle;
    address recipient;
    uint256 shares;
    uint256 amount0Min;
    uint256 amount1Min;
}
```

