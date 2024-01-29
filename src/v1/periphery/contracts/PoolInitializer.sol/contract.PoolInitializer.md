# PoolInitializer
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/252206c9465648eefefe7b978f4e865682332b87/contracts/PoolInitializer.sol)

**Inherits:**
[IPoolInitializer](/contracts/interfaces/IPoolInitializer.sol/interface.IPoolInitializer.md), IMarginalV1SwapCallback, [PeripheryImmutableState](/contracts/base/PeripheryImmutableState.sol/abstract.PeripheryImmutableState.md), [LiquidityManagement](/contracts/base/LiquidityManagement.sol/abstract.LiquidityManagement.md), PeripheryValidation, Multicall

Provides methods for preparing, creating and initializing a Marginal v1 pool and its associated Uniswap v3 oracle


## Functions
### constructor


```solidity
constructor(address _factory, address _WETH9) PeripheryImmutableState(_factory, _WETH9);
```

### marginalV1SwapCallback


```solidity
function marginalV1SwapCallback(int256 amount0Delta, int256 amount1Delta, bytes calldata _data) external override;
```

### createAndInitializePoolIfNecessary

Creates a new pool if it does not exist, then initializes if not initialized


```solidity
function createAndInitializePoolIfNecessary(CreateAndInitializeParams calldata params)
    public
    payable
    override
    checkDeadline(params.deadline)
    returns (address pool, uint256 shares, int256 amount0, int256 amount1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`CreateAndInitializeParams`|The parameters necessary to create and initialize a pool, encoded as `CreateAndInitializeParams` in calldata|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`pool`|`address`|Returns the pool address based on the pair of tokens, Uniswap v3 fee, and maintenance, will return the newly created pool address if necessary|
|`shares`|`uint256`|The amount of shares minted to `params.recipient` after initializing pool with liquidity|
|`amount0`|`int256`|The amount of the input token0 to create and initialize pool|
|`amount1`|`int256`|The amount of the input token1 to create and initialize pool|


### initializePoolSqrtPriceX96

Swaps through pool to set the pool price

*Intended for pools with dust amounts of liquidity as otherwise amount in will be substantial
Ignores effect on pool price of adding fee to liquidity for simplicity. Results in difference of < 1 bps in practice vs desired price*


```solidity
function initializePoolSqrtPriceX96(InitializePoolSqrtPriceX96Params memory params)
    public
    payable
    override
    checkDeadline(params.deadline)
    returns (int256 amount0, int256 amount1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`InitializePoolSqrtPriceX96Params`|The parameters necessary to initialize pool with `params.sqrtPriceX96`|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount0`|`int256`|The amount of the input token0 to set the price|
|`amount1`|`int256`|The amount of the input token1 to set the price|


### initializeOracleIfNecessary

Increases observationCardinalityNext on oracle Uniswap v3 pool, if necessary, to prepare for Marginal v1 pool creation.

*There will be a time lag between increasing observationCardinalityNext on the oracle pool and when observationCardinality on slot0 changes.*


```solidity
function initializeOracleIfNecessary(InitializeOracleParams calldata params) external override;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`InitializeOracleParams`|The parameters necessary to initialize oracle for pool, encoded as `InitializeOracleParams` in calldata|


## Events
### PoolInitialize

```solidity
event PoolInitialize(address indexed sender, address pool, uint256 shares, int256 amount0, int256 amount1);
```

## Errors
### InvalidOracle

```solidity
error InvalidOracle();
```

### PoolNotInitialized

```solidity
error PoolNotInitialized();
```

### AmountInGreaterThanMax

```solidity
error AmountInGreaterThanMax(uint256 amountIn);
```

### AmountOutLessThanMin

```solidity
error AmountOutLessThanMin(uint256 amountOut);
```

### LiquidityBurnedLessThanMin

```solidity
error LiquidityBurnedLessThanMin();
```

### Amount0BurnedGreaterThanMax

```solidity
error Amount0BurnedGreaterThanMax(int256 amount0Burned);
```

### Amount1BurnedGreaterThanMax

```solidity
error Amount1BurnedGreaterThanMax(int256 amount1Burned);
```

## Structs
### SwapCallbackData

```solidity
struct SwapCallbackData {
    bytes path;
    address payer;
}
```

