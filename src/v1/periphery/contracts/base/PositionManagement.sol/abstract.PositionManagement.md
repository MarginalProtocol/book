# PositionManagement
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/6ce65434509972d6f67aeab3e318f9db63a09fe0/contracts/base/PositionManagement.sol)

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
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`OpenParams`|The parameters necessary to open the position on the pool|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`id`|`uint256`|The position ID stored in the pool|
|`size`|`uint256`|The position size on the pool in the margin token|
|`debt`|`uint256`|The position debt owed to the pool in the non-margin token|
|`margin`|`uint256`|The margin backing the position opened on the pool|
|`fees`|`uint256`|The fees paid in margin token to open the position on the pool|
|`rewards`|`uint256`|The rewards escrowed in opened position available to liquidators when position not safe|


### marginalV1OpenCallback


```solidity
function marginalV1OpenCallback(uint256 amount0Owed, uint256 amount1Owed, bytes calldata data) external virtual;
```

### adjust

Adjusts margin backing position on pool


```solidity
function adjust(AdjustParams memory params) internal virtual returns (uint256 margin0, uint256 margin1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`AdjustParams`|The parameters necessary to adjust the position on the pool|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`margin0`|`uint256`|The amount of token0 to be used as the new margin backing the position|
|`margin1`|`uint256`|The amount of token1 to be used as the new margin backing the position|


### marginalV1AdjustCallback


```solidity
function marginalV1AdjustCallback(uint256 amount0Owed, uint256 amount1Owed, bytes calldata data) external virtual;
```

### settle

Settles a position on pool via external payer of debt

*Beware of re-entrancy issues given implicit ETH transfer at end of function*


```solidity
function settle(SettleParams memory params)
    internal
    virtual
    returns (int256 amount0, int256 amount1, uint256 rewards);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`SettleParams`|The parameters necessary to settle the position on the pool|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount0`|`int256`|The delta of the balance of token0 of the pool. Position debt into the pool (> 0) if long token1 (zeroForOne = true), or position size and margin out of the pool (< 0) if long token0 (zeroForOne = false)|
|`amount1`|`int256`|The delta of the balance of token1 of the pool. Position size and margin out of the pool (< 0) if long token1 (zeroForOne = true), or position debt into the pool (> 0) if long token0 (zeroForOne = false)|
|`rewards`|`uint256`|The amount of escrowed native (gas) token sent to `params.recipient`|


### flash

Settles a position by repaying debt with portion of size swapped through spot

*Beware of re-entrancy issues given implicit ETH transfer at end of function*


```solidity
function flash(FlashParams memory params) internal virtual returns (uint256 amountOut, uint256 rewards);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`FlashParams`|The parameters necessary to flash settle the position on the pool|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountOut`|`uint256`|The amount of margin token received from pool less debts repaid via swapping on spot|
|`rewards`|`uint256`|The amount of escrowed native (gas) token released by pool after flash settling the position|


### marginalV1SettleCallback


```solidity
function marginalV1SettleCallback(int256 amount0Delta, int256 amount1Delta, bytes calldata data) external virtual;
```

### uniswapV3SwapCallback


```solidity
function uniswapV3SwapCallback(int256 amount0Delta, int256 amount1Delta, bytes calldata data) external virtual;
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

