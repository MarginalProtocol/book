# IRouter
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/2ce1df3e90c9d2b47899fece944f04a7d78d5b16/contracts/interfaces/IRouter.sol)

Facilitates swaps and liquidity provision on Marginal v1 pools


## Functions
### exactInputSingle

Swaps `amountIn` of one token for as much as possible of another token


```solidity
function exactInputSingle(ExactInputSingleParams calldata params) external payable returns (uint256 amountOut);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`ExactInputSingleParams`|The parameters necessary for the swap, encoded as `ExactInputSingleParams` in calldata|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountOut`|`uint256`|The amount of the received token|


### exactInput

Swaps `amountIn` of one token for as much as possible of another along the specified path


```solidity
function exactInput(ExactInputParams calldata params) external payable returns (uint256 amountOut);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`ExactInputParams`|The parameters necessary for the multi-hop swap, encoded as `ExactInputParams` in calldata|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountOut`|`uint256`|The amount of the received token|


### exactOutputSingle

Swaps as little as possible of one token for `amountOut` of another token

*If a contract sending in native (gas) token, `msg.sender` must implement a `receive()` function to receive any refunded unspent amount in.*


```solidity
function exactOutputSingle(ExactOutputSingleParams calldata params) external payable returns (uint256 amountIn);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`ExactOutputSingleParams`|The parameters necessary for the swap, encoded as `ExactOutputSingleParams` in calldata|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountIn`|`uint256`|The amount of the input token|


### exactOutput

Swaps as little as possible of one token for `amountOut` of another along the specified path (reversed)

*If a contract sending in native (gas) token, `msg.sender` must implement a `receive()` function to receive any refunded unspent amount in.*


```solidity
function exactOutput(ExactOutputParams calldata params) external payable returns (uint256 amountIn);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`ExactOutputParams`|The parameters necessary for the multi-hop swap, encoded as `ExactOutputParams` in calldata|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountIn`|`uint256`|The amount of the input token|


### addLiquidity

Adds liquidity, minting on pool

*If a contract sending in native (gas) token, `msg.sender` must implement a `receive()` function to receive any refunded unspent amount in.*


```solidity
function addLiquidity(AddLiquidityParams calldata params)
    external
    payable
    returns (uint256 shares, uint256 amount0, uint256 amount1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`AddLiquidityParams`|The parameters necessary for adding liquidity, encoded as `AddLiquidityParams` in calldata|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`shares`|`uint256`|The amount of shares minted|
|`amount0`|`uint256`|The amount of the input token0|
|`amount1`|`uint256`|The amount of the input token1|


### removeLiquidity

Removes liquidity, burning on pool


```solidity
function removeLiquidity(RemoveLiquidityParams calldata params)
    external
    payable
    returns (uint128 liquidityDelta, uint256 amount0, uint256 amount1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`RemoveLiquidityParams`|The parameters necessary for removing liquidity, encoded as `RemoveLiquidityParams` in calldata|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`liquidityDelta`|`uint128`|The amount of liquidity removed|
|`amount0`|`uint256`|The amount of the output token0|
|`amount1`|`uint256`|The amount of the output token1|


## Events
### IncreaseLiquidity

```solidity
event IncreaseLiquidity(uint256 shares, uint128 liquidityDelta, uint256 amount0, uint256 amount1);
```

### DecreaseLiquidity

```solidity
event DecreaseLiquidity(uint256 shares, uint128 liquidityDelta, uint256 amount0, uint256 amount1);
```

## Structs
### ExactInputSingleParams

```solidity
struct ExactInputSingleParams {
    address tokenIn;
    address tokenOut;
    uint24 maintenance;
    address oracle;
    address recipient;
    uint256 deadline;
    uint256 amountIn;
    uint256 amountOutMinimum;
    uint160 sqrtPriceLimitX96;
}
```

### ExactInputParams

```solidity
struct ExactInputParams {
    bytes path;
    address recipient;
    uint256 deadline;
    uint256 amountIn;
    uint256 amountOutMinimum;
}
```

### ExactOutputSingleParams

```solidity
struct ExactOutputSingleParams {
    address tokenIn;
    address tokenOut;
    uint24 maintenance;
    address oracle;
    address recipient;
    uint256 deadline;
    uint256 amountOut;
    uint256 amountInMaximum;
    uint160 sqrtPriceLimitX96;
}
```

### ExactOutputParams

```solidity
struct ExactOutputParams {
    bytes path;
    address recipient;
    uint256 deadline;
    uint256 amountOut;
    uint256 amountInMaximum;
}
```

### AddLiquidityParams

```solidity
struct AddLiquidityParams {
    address token0;
    address token1;
    uint24 maintenance;
    address oracle;
    address recipient;
    uint256 amount0Desired;
    uint256 amount1Desired;
    uint256 amount0Min;
    uint256 amount1Min;
    uint256 deadline;
}
```

### RemoveLiquidityParams

```solidity
struct RemoveLiquidityParams {
    address token0;
    address token1;
    uint24 maintenance;
    address oracle;
    address recipient;
    uint256 shares;
    uint256 amount0Min;
    uint256 amount1Min;
    uint256 deadline;
}
```

