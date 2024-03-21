# IPoolInitializer
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/de728cd3d633f080a3fd40108fe8de3ab4edd595/contracts/interfaces/IPoolInitializer.sol)

Provides methods for preparing, creating and initializing a Marginal v1 pool


## Functions
### createAndInitializePoolIfNecessary

Creates a new pool if it does not exist, then initializes if not initialized


```solidity
function createAndInitializePoolIfNecessary(CreateAndInitializeParams calldata params)
    external
    payable
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
    external
    payable
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
function initializeOracleIfNecessary(InitializeOracleParams calldata params) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`InitializeOracleParams`|The parameters necessary to initialize oracle for pool, encoded as `InitializeOracleParams` in calldata|


## Structs
### CreateAndInitializeParams

```solidity
struct CreateAndInitializeParams {
    address token0;
    address token1;
    uint24 maintenance;
    uint24 uniswapV3Fee;
    address recipient;
    uint160 sqrtPriceX96;
    uint160 sqrtPriceLimitX96;
    uint128 liquidityBurned;
    int256 amount0BurnedMax;
    int256 amount1BurnedMax;
    uint256 amount0Desired;
    uint256 amount1Desired;
    uint256 amount0Min;
    uint256 amount1Min;
    uint256 deadline;
}
```

### InitializePoolSqrtPriceX96Params

```solidity
struct InitializePoolSqrtPriceX96Params {
    address token0;
    address token1;
    uint24 maintenance;
    address oracle;
    address recipient;
    uint160 sqrtPriceX96;
    uint256 amountInMaximum;
    uint256 amountOutMinimum;
    uint160 sqrtPriceLimitX96;
    uint256 deadline;
}
```

### InitializeOracleParams

```solidity
struct InitializeOracleParams {
    address token0;
    address token1;
    uint24 uniswapV3Fee;
    uint16 observationCardinalityNext;
}
```

