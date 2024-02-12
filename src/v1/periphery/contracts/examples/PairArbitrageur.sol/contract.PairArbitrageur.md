# PairArbitrageur
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/1d4c6a63a24ea055be056199b2cac6431f68ec06/contracts/examples/PairArbitrageur.sol)

**Inherits:**
IMarginalV1SwapCallback, IUniswapV3SwapCallback, [PeripheryImmutableState](/contracts/base/PeripheryImmutableState.sol/abstract.PeripheryImmutableState.md), [PeripheryPayments](/contracts/base/PeripheryPayments.sol/abstract.PeripheryPayments.md), PeripheryValidation, Multicall

Simple flash arbitrageur between Marginal v1 and their associated Uniswap v3 spot oracle pools

*WARNING: This contract is unaudited. Use at your own risk*


## State Variables
### DEFAULT_SQRT_PRICE_LIMIT_X96_CACHED
*Used as the placeholder value for sqrtPriceLimit1X96*


```solidity
uint160 private constant DEFAULT_SQRT_PRICE_LIMIT_X96_CACHED = 0;
```


### sqrtPriceLimit1X96Cached
*Transient storage variable used for returning the computed amount in for an exact output swap.*


```solidity
uint160 private sqrtPriceLimit1X96Cached = DEFAULT_SQRT_PRICE_LIMIT_X96_CACHED;
```


## Functions
### constructor


```solidity
constructor(address _factory, address _WETH9) PeripheryImmutableState(_factory, _WETH9);
```

### marginalV1SwapCallback


```solidity
function marginalV1SwapCallback(int256 amount0Delta, int256 amount1Delta, bytes calldata _data) external override;
```

### uniswapV3SwapCallback


```solidity
function uniswapV3SwapCallback(int256 amount0Delta, int256 amount1Delta, bytes calldata _data) external override;
```

### execute

Executes the arb between Marginal v1 pool and its associated Uniswap v3 oracle

*Naively assumes x*y=L^2 for both pools, so works for swaps within a tick on Uniswap v3.
Also ignores fees in calculation for size to arb with.*


```solidity
function execute(ExecuteParams calldata params)
    external
    payable
    checkDeadline(params.deadline)
    returns (uint256 amountOut);
```

## Errors
### PoolNotInitialized

```solidity
error PoolNotInitialized();
```

### PoolInvalid

```solidity
error PoolInvalid();
```

### ArbitrageNotAvailable

```solidity
error ArbitrageNotAvailable();
```

### AmountOutLessThanMin

```solidity
error AmountOutLessThanMin(uint256 amountOut);
```

## Structs
### SwapCallbackData

```solidity
struct SwapCallbackData {
    bytes path;
    address payer;
}
```

### ExecuteParams

```solidity
struct ExecuteParams {
    address token0;
    address token1;
    uint24 maintenance;
    address oracle;
    address recipient;
    address tokenOut;
    uint256 amountOutMinimum;
    uint160 sqrtPriceLimit0X96;
    uint160 sqrtPriceLimit1X96;
    uint256 deadline;
    bool sweepAsETH;
}
```

