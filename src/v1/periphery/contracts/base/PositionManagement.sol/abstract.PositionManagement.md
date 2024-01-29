# PositionManagement
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/252206c9465648eefefe7b978f4e865682332b87/contracts/base/PositionManagement.sol)

**Inherits:**
IMarginalV1AdjustCallback, IMarginalV1OpenCallback, IMarginalV1SettleCallback, IUniswapV3SwapCallback, [PeripheryImmutableState](/contracts/base/PeripheryImmutableState.sol/abstract.PeripheryImmutableState.md), [PeripheryPayments](/contracts/base/PeripheryPayments.sol/abstract.PeripheryPayments.md)


## Functions
### getPool

*Returns the pool for the given token pair and maintenance. The pool contract may or may not exist.*


```solidity
function getPool(PoolAddress.PoolKey memory poolKey) internal view returns (IMarginalV1Pool);
```

### open

Opens a new position on pool


```solidity
function open(OpenParams memory params)
    internal
    virtual
    returns (uint256 id, uint256 size, uint256 debt, uint256 margin, uint256 fees, uint256 rewards);
```

### marginalV1OpenCallback


```solidity
function marginalV1OpenCallback(uint256 amount0Owed, uint256 amount1Owed, bytes calldata data) external virtual;
```

### adjust

Adjusts margin backing position on pool


```solidity
function adjust(AdjustParams memory params) internal virtual returns (uint256 margin0, uint256 margin1);
```

### marginalV1AdjustCallback


```solidity
function marginalV1AdjustCallback(uint256 amount0Owed, uint256 amount1Owed, bytes calldata data) external virtual;
```

### settle

Settles a position on pool via external payer of debt


```solidity
function settle(SettleParams memory params)
    internal
    virtual
    returns (int256 amount0, int256 amount1, uint256 rewards);
```

### flash

Settles a position by repaying debt with portion of size swapped through spot


```solidity
function flash(FlashParams memory params) internal virtual returns (uint256 amountOut, uint256 rewards);
```

### marginalV1SettleCallback


```solidity
function marginalV1SettleCallback(int256 amount0Delta, int256 amount1Delta, bytes calldata data) external virtual;
```

### uniswapV3SwapCallback


```solidity
function uniswapV3SwapCallback(int256 amount0Delta, int256 amount1Delta, bytes calldata data) external virtual;
```

### liquidate

Liquidates a position on pool


```solidity
function liquidate(LiquidateParams memory params) internal virtual returns (uint256 rewards);
```

## Errors
### SizeLessThanMin

```solidity
error SizeLessThanMin(uint256 size);
```

### DebtGreaterThanMax

```solidity
error DebtGreaterThanMax(uint256 debt);
```

### AmountInGreaterThanMax

```solidity
error AmountInGreaterThanMax(uint256 amountIn);
```

### AmountOutLessThanMin

```solidity
error AmountOutLessThanMin(uint256 amountOut);
```

### RewardsLessThanMin

```solidity
error RewardsLessThanMin(uint256 rewardsMinimum);
```

## Structs
### PositionCallbackData

```solidity
struct PositionCallbackData {
    PoolAddress.PoolKey poolKey;
    address payer;
}
```

### OpenParams

```solidity
struct OpenParams {
    address token0;
    address token1;
    uint24 maintenance;
    address oracle;
    address recipient;
    bool zeroForOne;
    uint128 liquidityDelta;
    uint160 sqrtPriceLimitX96;
    uint128 margin;
    uint128 sizeMinimum;
    uint128 debtMaximum;
    uint256 amountInMaximum;
}
```

### AdjustParams

```solidity
struct AdjustParams {
    address token0;
    address token1;
    uint24 maintenance;
    address oracle;
    address recipient;
    uint96 id;
    int128 marginDelta;
}
```

### SettleParams

```solidity
struct SettleParams {
    address token0;
    address token1;
    uint24 maintenance;
    address oracle;
    address recipient;
    uint96 id;
}
```

### FlashParams

```solidity
struct FlashParams {
    address token0;
    address token1;
    uint24 maintenance;
    address oracle;
    address recipient;
    uint96 id;
    uint256 amountOutMinimum;
}
```

### LiquidateParams

```solidity
struct LiquidateParams {
    address token0;
    address token1;
    uint24 maintenance;
    address oracle;
    address recipient;
    address owner;
    uint96 id;
}
```

