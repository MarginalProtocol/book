# Router
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/d846d56fa6d1e439306e60a85e98fc298babb2f7/contracts/Router.sol)

**Inherits:**
[IRouter](/contracts/interfaces/IRouter.sol/interface.IRouter.md), IMarginalV1SwapCallback, [PeripheryImmutableState](/contracts/base/PeripheryImmutableState.sol/abstract.PeripheryImmutableState.md), [LiquidityManagement](/contracts/base/LiquidityManagement.sol/abstract.LiquidityManagement.md), PeripheryValidation, Multicall, SelfPermit

Facilitates swaps and liquidity provision on Marginal v1 pools

*Fork of the Uniswap v3 periphery SwapRouter*


## State Variables
### DEFAULT_AMOUNT_IN_CACHED
*Used as the placeholder value for amountInCached, because the computed amount in for an exact output swap
can never actually be this value*


```solidity
uint256 private constant DEFAULT_AMOUNT_IN_CACHED = type(uint256).max;
```


### amountInCached
*Transient storage variable used for returning the computed amount in for an exact output swap.*


```solidity
uint256 private amountInCached = DEFAULT_AMOUNT_IN_CACHED;
```


## Functions
### constructor


```solidity
constructor(address _factory, address _WETH9) PeripheryImmutableState(_factory, _WETH9);
```

### getPool

*Returns the pool for the given token pair, maintenance, and oracle. The pool contract may or may not exist.*


```solidity
function getPool(address tokenA, address tokenB, uint24 maintenance, address oracle)
    private
    view
    returns (IMarginalV1Pool);
```

### marginalV1SwapCallback


```solidity
function marginalV1SwapCallback(int256 amount0Delta, int256 amount1Delta, bytes calldata _data) external override;
```

### exactInputInternal

*Performs a single exact input swap*


```solidity
function exactInputInternal(
    uint256 amountIn,
    address recipient,
    uint160 sqrtPriceLimitX96,
    SwapCallbackData memory data
) private returns (uint256 amountOut);
```

### exactInputSingle

Swaps `amountIn` of one token for as much as possible of another token


```solidity
function exactInputSingle(ExactInputSingleParams calldata params)
    external
    payable
    override
    checkDeadline(params.deadline)
    returns (uint256 amountOut);
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
function exactInput(ExactInputParams memory params)
    external
    payable
    override
    checkDeadline(params.deadline)
    returns (uint256 amountOut);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`ExactInputParams`|The parameters necessary for the multi-hop swap, encoded as `ExactInputParams` in calldata|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountOut`|`uint256`|The amount of the received token|


### exactOutputInternal

*Performs a single exact output swap*


```solidity
function exactOutputInternal(
    uint256 amountOut,
    address recipient,
    uint160 sqrtPriceLimitX96,
    SwapCallbackData memory data
) private returns (uint256 amountIn);
```

### exactOutputSingle

Swaps as little as possible of one token for `amountOut` of another token

*If a contract sending in native (gas) token, `msg.sender` must implement a `receive()` function to receive any refunded unspent amount in.*


```solidity
function exactOutputSingle(ExactOutputSingleParams calldata params)
    external
    payable
    override
    checkDeadline(params.deadline)
    returns (uint256 amountIn);
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
function exactOutput(ExactOutputParams calldata params)
    external
    payable
    override
    checkDeadline(params.deadline)
    returns (uint256 amountIn);
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
    checkDeadline(params.deadline)
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
    checkDeadline(params.deadline)
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


## Structs
### SwapCallbackData

```solidity
struct SwapCallbackData {
    bytes path;
    address payer;
}
```

