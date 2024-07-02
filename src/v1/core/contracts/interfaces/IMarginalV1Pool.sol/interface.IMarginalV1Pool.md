# IMarginalV1Pool
[Git Source](https://github.com/MarginalProtocol/v1-core/blob/2d246e9b4f6e970321a0f235176b47b340c9a03b/contracts/interfaces/IMarginalV1Pool.sol)

**Inherits:**
[IERC20](/contracts/.cache/openzeppelin/v4.8.3/token/ERC20/IERC20.sol/interface.IERC20.md)

A Marginal v1 pool facilitates leverage trading, swapping, and automated market making between any two assets that strictly conform
to the ERC20 specification

*Inherits from IERC20 as liquidity providers are minted fungible pool tokens*


## Functions
### factory

The Marginal v1 factory that created the pool


```solidity
function factory() external view returns (address);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the Marginal v1 factory|


### oracle

The Uniswap v3 oracle referenced by the pool for funding and position safety


```solidity
function oracle() external view returns (address);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the Uniswap v3 oracle referenced by the pool|


### token0

The first of the two tokens of the pool, sorted by address


```solidity
function token0() external view returns (address);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the token0 contract|


### token1

The second of the two tokens of the pool, sorted by address


```solidity
function token1() external view returns (address);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the token1 contract|


### maintenance

The minimum maintenance requirement for leverage positions on the pool


```solidity
function maintenance() external view returns (uint24);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint24`|The minimum maintenance requirement|


### fee

The pool's fee in hundredths of a bip, i.e. 1e-6


```solidity
function fee() external view returns (uint24);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint24`|The fee|


### rewardPremium

The premium multiplier on liquidation rewards in hundredths of a bip, i.e. 1e-6

*Liquidation rewards set aside in native (gas) token.
Premium acts as an incentive above the expected gas cost to call IMarginalV1Pool#liquidate.*


```solidity
function rewardPremium() external view returns (uint24);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint24`|The premium multiplier|


### tickCumulativeRateMax

The maximum rate of change in tick cumulative between the Marginal v1 pool and the Uniswap v3 oracle

*Puts a ceiling on funding paid per second*


```solidity
function tickCumulativeRateMax() external view returns (uint24);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint24`|The maximum tick cumulative rate per second|


### secondsAgo

The amount of time in seconds to average the Uniswap v3 oracle TWAP over to assess position safety


```solidity
function secondsAgo() external view returns (uint32);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint32`|The averaging time for the Uniswap v3 oracle TWAP in seconds|


### fundingPeriod

The period in seconds to benchmark funding payments with respect to

*Acts as an averaging period on tick cumulative changes between the Marginal v1 pool and the Uniswap v3 oracle*


```solidity
function fundingPeriod() external view returns (uint32);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint32`|The funding period in seconds|


### state

The pool state represented in (L, sqrt(P)) space


```solidity
function state()
    external
    view
    returns (
        uint160 sqrtPriceX96,
        uint96 totalPositions,
        uint128 liquidity,
        int24 tick,
        uint32 blockTimestamp,
        int56 tickCumulative,
        uint8 feeProtocol,
        bool initialized
    );
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`sqrtPriceX96`|`uint160`|The current price of the pool as a sqrt(token1/token0) Q64.96 value totalPositions The total number of leverage positions that have ever been taken out on the pool liquidity The currently available liquidity offered by the pool for swaps and leverage positions tick The current tick of the pool, i.e. according to the last tick transition that was run. blockTimestamp The last `block.timestamp` at which state was synced tickCumulative The tick cumulative running sum of the pool, used in funding calculations feeProtocol The protocol fee for both tokens of the pool initialized Whether the pool has been initialized|
|`totalPositions`|`uint96`||
|`liquidity`|`uint128`||
|`tick`|`int24`||
|`blockTimestamp`|`uint32`||
|`tickCumulative`|`int56`||
|`feeProtocol`|`uint8`||
|`initialized`|`bool`||


### liquidityLocked

The liquidity used to capitalize outstanding leverage positions


```solidity
function liquidityLocked() external view returns (uint128);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint128`|The liquidity locked for outstanding leverage positions|


### protocolFees

The amounts of token0 and token1 that are owed to the protocol

*Protocol fees will never exceed uint128 max in either token*


```solidity
function protocolFees() external view returns (uint128 protocolFees0, uint128 protocolFees1);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`protocolFees0`|`uint128`|The amount of token0 owed to the protocol|
|`protocolFees1`|`uint128`|The amount of token1 owed to the protocol|


### positions

Returns information about a leverage position by the position's key

*Either debt0 (zeroForOne = true) or debt1 (zeroForOne = false) will be updated each funding sync*


```solidity
function positions(bytes32 key)
    external
    view
    returns (
        uint128 size,
        uint128 debt0,
        uint128 debt1,
        uint128 insurance0,
        uint128 insurance1,
        bool zeroForOne,
        bool liquidated,
        int24 tick,
        uint32 blockTimestamp,
        int56 tickCumulativeDelta,
        uint128 margin,
        uint128 liquidityLocked,
        uint256 rewards
    );
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`key`|`bytes32`|The position's key is a hash of the packed encoding of the owner and the position ID|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`size`|`uint128`|The position size in the token the owner is long debt0 The position debt in token0 owed to the pool at settlement. If long token1 (zeroForOne = true), this is the debt to be repaid at settlement by owner. Otherwise, simply used for internal accounting debt1 The position debt in token1 owed to the pool at settlement. If long token0 (zeroForOne = false), this is the debt to be repaid at settlement by owner. Otherwise, simply used for internal accounting insurance0 The insurance in token0 set aside to backstop the position in case of late liquidations insurance1 The insurance in token1 set aside to backstop the position in case of late liquidations zeroForOne Whether the position is long token1 and short token0 (true) or long token0 and short token1 (false) liquidated Whether the position has been liquidated tick The pool tick prior to opening the position blockTimestamp The `block.timestamp` at which the position was last synced for funding tickCumulativeDelta The difference in the Uniswap v3 oracle tick cumulative and the Marginal v1 pool tick cumulative at the last funding sync margin The position margin in the token the owner is long liquidityLocked The liquidity locked by the pool to collateralize the position rewards The liquidation rewards in the native (gas) token received by liquidator if position becomes unsafe|
|`debt0`|`uint128`||
|`debt1`|`uint128`||
|`insurance0`|`uint128`||
|`insurance1`|`uint128`||
|`zeroForOne`|`bool`||
|`liquidated`|`bool`||
|`tick`|`int24`||
|`blockTimestamp`|`uint32`||
|`tickCumulativeDelta`|`int56`||
|`margin`|`uint128`||
|`liquidityLocked`|`uint128`||
|`rewards`|`uint256`||


### open

Opens a leverage position on the pool

*The caller of this method receives a callback in the form of IMarginalV1OpenCallback#marginalV1OpenCallback.
The caller must forward liquidation rewards in the native (gas) token to be escrowed by the pool contract
Rewards determined by current `block.basefee` * estimated gas cost to call IMarginalV1Pool#liquidate * rewardPremium*


```solidity
function open(
    address recipient,
    bool zeroForOne,
    uint128 liquidityDelta,
    uint160 sqrtPriceLimitX96,
    uint128 margin,
    bytes calldata data
) external payable returns (uint256 id, uint256 size, uint256 debt, uint256 amount0, uint256 amount1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient`|`address`|The address of the owner of the opened position|
|`zeroForOne`|`bool`|Whether long token1 and short token0 (true), or long token0 and short token1 (false)|
|`liquidityDelta`|`uint128`|The amount of liquidity for the pool to lock to capitalize the position|
|`sqrtPriceLimitX96`|`uint160`|The Q64.96 sqrt price limit. If zero for one, the price cannot be less than this value after opening the position otherwise the call reverts. If one for zero, the price cannot be greater than this value after opening|
|`margin`|`uint128`|The amount of margin used to back the position in the token the position is long|
|`data`|`bytes`|Any data to be passed through to the callback|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`id`|`uint256`|The ID of the opened position|
|`size`|`uint256`|The size of the opened position in the token the position is long. Excludes margin amount provided by caller|
|`debt`|`uint256`|The debt of the opened position in the token the position is short|
|`amount0`|`uint256`|The amount of token0 caller must send to pool to open the position|
|`amount1`|`uint256`|The amount of token1 caller must send to pool to open the position|


### adjust

Adjusts the margin used to back a position on the pool

*The caller of this method receives a callback in the form of IMarginalV1AdjustCallback#marginalV1AdjustCallback
Old position margin is flashed out to recipient prior to the callback*


```solidity
function adjust(address recipient, uint96 id, int128 marginDelta, bytes calldata data)
    external
    returns (uint256 margin0, uint256 margin1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient`|`address`|The address to receive the old position margin|
|`id`|`uint96`|The ID of the position to adjust|
|`marginDelta`|`int128`|The delta of the margin backing the position on the pool. Adding margin to the position when positive, removing margin when negative|
|`data`|`bytes`|Any data to be passed through to the callback|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`margin0`|`uint256`|The amount of token0 to be used as the new margin backing the position|
|`margin1`|`uint256`|The amount of token1 to be used as the new margin backing the position|


### settle

Settles a position on the pool

*The caller of this method receives a callback in the form of IMarginalV1SettleCallback#marginalV1SettleCallback.
If a contract, `recipient` must implement a `receive()` function to receive the escrowed liquidation rewards in the native (gas) token from the pool.
Position size, margin, and liquidation rewards are flashed out before the callback to allow the caller to swap to repay the debt to the pool*


```solidity
function settle(address recipient, uint96 id, bytes calldata data)
    external
    returns (int256 amount0, int256 amount1, uint256 rewards);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient`|`address`|The address to receive the size, margin, and liquidation rewards of the settled position|
|`id`|`uint96`|The ID of the position to settle|
|`data`|`bytes`|Any data to be passed through to the callback|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount0`|`int256`|The delta of the balance of token0 of the pool. Position debt into the pool (> 0) if long token1 (zeroForOne = true), or position size and margin out of the pool (< 0) if long token0 (zeroForOne = false)|
|`amount1`|`int256`|The delta of the balance of token1 of the pool. Position size and margin out of the pool (< 0) if long token1 (zeroForOne = true), or position debt into the pool (> 0) if long token0 (zeroForOne = false)|
|`rewards`|`uint256`|The amount of escrowed native (gas) token sent to `recipient`|


### liquidate

Liquidates a position on the pool

*Reverts if position is safe from liquidation. Position is considered safe if
(`position.margin` + `position.size`) / oracleTwap >= (1 + `maintenance`) * `position.debt0` when position.zeroForOne = true
(`position.margin` + `position.size`) * oracleTwap >= (1 + `maintenance`) * `position.debt1` when position.zeroForOne = false
Safety checks are performed after syncing the position debts for funding payments
If a contract, `recipient` must implement a `receive()` function to receive the escrowed liquidation rewards in the native (gas) token from the pool.*


```solidity
function liquidate(address recipient, address owner, uint96 id) external returns (uint256 rewards);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient`|`address`|The address to receive liquidation rewards escrowed with the position|
|`owner`|`address`|The address of the owner of the position to liquidate|
|`id`|`uint96`|The ID of the position to liquidate|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`rewards`|`uint256`|The amount of escrowed native (gas) token sent to `recipient`|


### swap

Swap token0 for token1, or token1 for token0

*The caller of this method receives a callback in the form of IMarginalV1SwapCallback#marginalV1SwapCallback*


```solidity
function swap(
    address recipient,
    bool zeroForOne,
    int256 amountSpecified,
    uint160 sqrtPriceLimitX96,
    bytes calldata data
) external returns (int256 amount0, int256 amount1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient`|`address`|The address to receive the output of the swap|
|`zeroForOne`|`bool`|The direction of the swap, true for token0 to token1, false for token1 to token0|
|`amountSpecified`|`int256`|The amount of the swap, which implicitly configures the swap as exact input (positive), or exact output (negative)|
|`sqrtPriceLimitX96`|`uint160`|The Q64.96 sqrt price limit. If zero for one, the price cannot be less than this value after the swap otherwise the call reverts. If one for zero, the price cannot be greater than this value after the swap|
|`data`|`bytes`|Any data to be passed through to the callback|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount0`|`int256`|The delta of the balance of token0 of the pool, exact when negative, minimum when positive|
|`amount1`|`int256`|The delta of the balance of token1 of the pool, exact when negative, minimum when positive|


### mint

Adds liquidity to the pool

*The caller of this method receives a callback in the form of IMarginalV1MintCallback#marginalV1MintCallback.
The pool is initialized through the first call to mint*


```solidity
function mint(address recipient, uint128 liquidityDelta, bytes calldata data)
    external
    returns (uint256 shares, uint256 amount0, uint256 amount1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient`|`address`|The address to mint LP tokens to after adding liquidity to the pool|
|`liquidityDelta`|`uint128`|The liquidity added to the pool|
|`data`|`bytes`|Any data to be passed through to the callback|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`shares`|`uint256`|The amount of LP token shares minted to recipient|
|`amount0`|`uint256`|The amount of token0 added to the pool reserves|
|`amount1`|`uint256`|The amount of token1 added to the pool reserves|


### burn

Removes liquidity from the pool

*Reverts if not enough liquidity available to exit due to outstanding leverage positions*


```solidity
function burn(address recipient, uint256 shares)
    external
    returns (uint128 liquidityDelta, uint256 amount0, uint256 amount1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient`|`address`|The address to send token amounts to after removing liquidity from the pool|
|`shares`|`uint256`|The amount of LP token shares to burn|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`liquidityDelta`|`uint128`|The liquidity removed from the pool|
|`amount0`|`uint256`|The amount of token0 removed from pool reserves|
|`amount1`|`uint256`|The amount of token1 removed from pool reserves|


### setFeeProtocol

Set the denominator of the protocol's % share of the fees


```solidity
function setFeeProtocol(uint8 feeProtocol) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`feeProtocol`|`uint8`|new protocol fee denominator for the pool|


### collectProtocol

Collect the protocol fee accrued to the pool


```solidity
function collectProtocol(address recipient) external returns (uint128 amount0, uint128 amount1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient`|`address`|The address to which collected protocol fees should be sent|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount0`|`uint128`|The protocol fee collected in token0|
|`amount1`|`uint128`|The protocol fee collected in token1|


