# Quoter
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/d846d56fa6d1e439306e60a85e98fc298babb2f7/contracts/lens/Quoter.sol)

**Inherits:**
[IQuoter](/contracts/interfaces/IQuoter.sol/interface.IQuoter.md), [PeripheryImmutableState](/contracts/base/PeripheryImmutableState.sol/abstract.PeripheryImmutableState.md), PeripheryValidation, [PositionState](/contracts/base/PositionState.sol/abstract.PositionState.md), Multicall

Quotes the result of leverage trades and swaps on Marginal v1 pools


## State Variables
### manager

```solidity
INonfungiblePositionManager public immutable manager;
```


### uniswapV3Quoter

```solidity
IUniswapV3StaticQuoter public immutable uniswapV3Quoter;
```


## Functions
### constructor


```solidity
constructor(address _factory, address _WETH9, address _manager, address _uniswapV3Quoter)
    PeripheryImmutableState(_factory, _WETH9);
```

### getPool

*Returns the pool for the given token pair and maintenance. The pool contract may or may not exist.*


```solidity
function getPool(PoolAddress.PoolKey memory poolKey) internal view returns (IMarginalV1Pool);
```

### quoteMint

Quotes the position result of NonfungiblePositionManager::mint

*Reverts if mint would revert*


```solidity
function quoteMint(INonfungiblePositionManager.MintParams calldata params)
    external
    view
    checkDeadline(params.deadline)
    returns (
        uint256 size,
        uint256 debt,
        uint256 margin,
        uint256 safeMarginMinimum,
        uint256 fees,
        bool safe,
        uint128 liquidityAfter,
        uint160 sqrtPriceX96After,
        uint128 liquidityLockedAfter
    );
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`INonfungiblePositionManager.MintParams`|Param inputs to NonfungiblePositionManager::mint|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`size`|`uint256`|Position size in units of amount1 if zeroForOne == true else units of amount0|
|`debt`|`uint256`|Position debt in units of amount0 if zeroForOne == true else units of amount1|
|`margin`|`uint256`|Amount of margin token in required to open position|
|`safeMarginMinimum`|`uint256`|The minimum margin requirements necessary to open position on pool while also being safe from liquidation|
|`fees`|`uint256`|Amount of fees in margin token paid to open the position|
|`safe`|`bool`|Whether the position will be safe given current oracle price averaged over seconds ago|
|`liquidityAfter`|`uint128`|Pool liquidity after mint|
|`sqrtPriceX96After`|`uint160`|Pool sqrt price after mint|
|`liquidityLockedAfter`|`uint128`|Pool locked liquidity after mint|


### _getPositionInfoSynced

Gets the pool position info synced for funding


```solidity
function _getPositionInfoSynced(
    address pool,
    uint96 positionId,
    uint32 blockTimestampLast,
    int56 tickCumulativeLast,
    int56 oracleTickCumulativeLast
) internal view returns (PositionLibrary.Info memory position);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`pool`|`address`|The address of the pool position is on|
|`positionId`|`uint96`|The ID of the pool position|
|`blockTimestampLast`|`uint32`|The last synced Marginal v1 pool timestamp|
|`tickCumulativeLast`|`int56`|The last synced Marginal v1 pool tick cumulative|
|`oracleTickCumulativeLast`|`int56`|The last synced Uniswap v3 oracle pool tick cumulative|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`position`|`PositionLibrary.Info`|The synced pool position info|


### quoteBurn

Quotes the result of calling NonfungiblePositionManager::burn

*Reverts if burn would revert*


```solidity
function quoteBurn(INonfungiblePositionManager.BurnParams calldata params)
    external
    view
    checkDeadline(params.deadline)
    returns (
        uint256 amountIn,
        uint256 amountOut,
        uint256 rewards,
        uint128 liquidityAfter,
        uint160 sqrtPriceX96After,
        uint128 liquidityLockedAfter
    );
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`INonfungiblePositionManager.BurnParams`|Param inputs to NonfungiblePositionManager::burn|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountIn`|`uint256`|Amount of debt token in needed to burn the position|
|`amountOut`|`uint256`|Amount of margin token out after burning the position|
|`rewards`|`uint256`|Amount of escrowed liquidation rewards out after burning the position|
|`liquidityAfter`|`uint128`|Pool liquidity after burn|
|`sqrtPriceX96After`|`uint160`|Pool sqrt price after burn|
|`liquidityLockedAfter`|`uint128`|Pool locked liquidity after burn|


### quoteIgnite

Quotes the result of calling NonfungiblePositionManager::ignite

*Reverts if ignite would revert*


```solidity
function quoteIgnite(INonfungiblePositionManager.IgniteParams calldata params)
    external
    view
    checkDeadline(params.deadline)
    returns (
        uint256 amountOut,
        uint256 rewards,
        uint128 liquidityAfter,
        uint160 sqrtPriceX96After,
        uint128 liquidityLockedAfter
    );
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`INonfungiblePositionManager.IgniteParams`|Param inputs to NonfungiblePositionManager::ignite|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountOut`|`uint256`|Amount of margin token out after igniting the position|
|`rewards`|`uint256`|Amount of escrowed liquidation rewards out after igniting the position|
|`liquidityAfter`|`uint128`|Pool liquidity after ignite|
|`sqrtPriceX96After`|`uint160`|Pool sqrt price after ignite|
|`liquidityLockedAfter`|`uint128`|Pool locked liquidity after ignite|


### quoteExactInputSingle

Quotes the amountOut result of Router::exactInputSingle

*Reverts if exactInputSingle would revert*


```solidity
function quoteExactInputSingle(IRouter.ExactInputSingleParams memory params)
    public
    view
    checkDeadline(params.deadline)
    returns (uint256 amountOut, uint128 liquidityAfter, uint160 sqrtPriceX96After);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`IRouter.ExactInputSingleParams`|Param inputs to Router::exactInputSingle|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountOut`|`uint256`|Amount of token received from pool after swap|
|`liquidityAfter`|`uint128`|Pool liquidity after swap|
|`sqrtPriceX96After`|`uint160`|Pool sqrt price after swap|


### quoteExactInput

Quotes the amountOut result of Router::exactInput

*Reverts if exactInput would revert*


```solidity
function quoteExactInput(IRouter.ExactInputParams memory params)
    external
    view
    returns (uint256 amountOut, uint128[] memory liquiditiesAfter, uint160[] memory sqrtPricesX96After);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`IRouter.ExactInputParams`|Param inputs to Router::exactInput|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountOut`|`uint256`|Amount of token received from pool after swap|
|`liquiditiesAfter`|`uint128[]`|Pool liquidities after swap|
|`sqrtPricesX96After`|`uint160[]`|Pool sqrt prices after swap|


### quoteExactOutputSingle

Quotes the amountIn result of Router::exactOutputSingle

*Reverts if exactOutputSingle would revert*


```solidity
function quoteExactOutputSingle(IRouter.ExactOutputSingleParams memory params)
    public
    view
    checkDeadline(params.deadline)
    returns (uint256 amountIn, uint128 liquidityAfter, uint160 sqrtPriceX96After);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`IRouter.ExactOutputSingleParams`|Param inputs to Router::exactOutputSingle|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountIn`|`uint256`|Amount of token sent to pool for swap|
|`liquidityAfter`|`uint128`|Pool liquidity after swap|
|`sqrtPriceX96After`|`uint160`|Pool sqrt price after swap|


### quoteExactOutput

Quotes the amountIn result of Router::exactOutput

*Reverts if exactOutput would revert*


```solidity
function quoteExactOutput(IRouter.ExactOutputParams memory params)
    external
    view
    returns (uint256 amountIn, uint128[] memory liquiditiesAfter, uint160[] memory sqrtPricesX96After);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`IRouter.ExactOutputParams`|Param inputs to Router::exactOutput|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountIn`|`uint256`|Amount of token sent to pool for swap|
|`liquiditiesAfter`|`uint128[]`|Pool liquidities after swap|
|`sqrtPricesX96After`|`uint160[]`|Pool sqrt prices after swap|


### quoteAddLiquidity

Quotes the amounts in result of Router::addLiquidity

*Reverts if addLiquidity would revert*


```solidity
function quoteAddLiquidity(IRouter.AddLiquidityParams memory params)
    external
    view
    checkDeadline(params.deadline)
    returns (uint256 shares, uint256 amount0, uint256 amount1, uint128 liquidityAfter);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`IRouter.AddLiquidityParams`|Param inputs to Router::addLiquidity|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`shares`|`uint256`|Amount of lp token minted by pool|
|`amount0`|`uint256`|Amount of token0 sent to pool for adding liquidity|
|`amount1`|`uint256`|Amount of token1 sent to pool for adding liquidity|
|`liquidityAfter`|`uint128`|Pool liquidity after adding liquidity|


### quoteRemoveLiquidity

Quotes the amounts in result of Router::removeLiquidity

*Reverts if removeLiquidity would revert*


```solidity
function quoteRemoveLiquidity(IRouter.RemoveLiquidityParams memory params)
    external
    view
    checkDeadline(params.deadline)
    returns (uint128 liquidityDelta, uint256 amount0, uint256 amount1, uint128 liquidityAfter);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`params`|`IRouter.RemoveLiquidityParams`|Param inputs to Router::removeLiquidity|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`liquidityDelta`|`uint128`|Amount of liquidity removed from pool|
|`amount0`|`uint256`|Amount of token0 received from pool for removing liquidity|
|`amount1`|`uint256`|Amount of token1 received from pool for removing liquidity|
|`liquidityAfter`|`uint128`|Pool liquidity after removing liquidity|


