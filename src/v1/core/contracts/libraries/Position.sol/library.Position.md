# Position
[Git Source](https://github.com/MarginalProtocol/v1-core/blob/4dcf410464dd1b73aaabe9fa06bd3450c672d3b9/contracts/libraries/Position.sol)

Facilitates calculations, updates, and retrieval of leverage position info

*Positions are represented in (x, y) space*


## Functions
### get

Gets a position from positions mapping


```solidity
function get(mapping(bytes32 => Info) storage positions, address owner, uint96 id)
    internal
    view
    returns (Info memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`positions`|`mapping(bytes32 => Info)`|The pool mapping that stores the leverage positions|
|`owner`|`address`|The owner of the position|
|`id`|`uint96`|The ID of the position|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`Info`|The position info associated with the (owner, ID) key|


### set

Stores the given position in positions mapping

*Used to create a new position or to update existing positions*


```solidity
function set(mapping(bytes32 => Info) storage positions, address owner, uint96 id, Info memory position) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`positions`|`mapping(bytes32 => Info)`|The pool mapping that stores the leverage positions|
|`owner`|`address`|The owner of the position|
|`id`|`uint96`|The ID of the position|
|`position`|`Info`|The position information to store|


### sync

Realizes funding payments via updates to position debt amounts


```solidity
function sync(
    Info memory position,
    uint32 blockTimestampLast,
    int56 tickCumulativeLast,
    int56 oracleTickCumulativeLast,
    uint24 tickCumulativeRateMax,
    uint32 fundingPeriod
) internal pure returns (Info memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`position`|`Info`|The position to sync|
|`blockTimestampLast`|`uint32`|The latest `block.timestamp` to sync to|
|`tickCumulativeLast`|`int56`|The `tickCumulative` from the pool at `blockTimestampLast`|
|`oracleTickCumulativeLast`|`int56`|The `tickCumulative` from the oracle at `blockTimestampLast`|
|`tickCumulativeRateMax`|`uint24`|The maximum rate of change in tick cumulative between the oracle and pool `tickCumulative` values|
|`fundingPeriod`|`uint32`|The pool funding period to benchmark funding payments to|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`Info`|The synced position|


### liquidate

Liquidates an existing position


```solidity
function liquidate(Info memory position) internal pure returns (Info memory positionAfter);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`position`|`Info`|The position to liquidate|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`positionAfter`|`Info`|The liquidated position info|


### settle

Settles existing position


```solidity
function settle(Info memory position) internal pure returns (Info memory positionAfter);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`position`|`Info`|The position to settle|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`positionAfter`|`Info`|The settled position info|


### assemble

Assembles a new position from pool state

*zeroForOne = true means short position (long token1, short token0)*


```solidity
function assemble(
    uint128 liquidity,
    uint160 sqrtPriceX96,
    uint160 sqrtPriceX96Next,
    uint128 liquidityDelta,
    bool zeroForOne,
    int24 tick,
    uint32 blockTimestampStart,
    int56 tickCumulativeStart,
    int56 oracleTickCumulativeStart
) internal pure returns (Info memory position);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`liquidity`|`uint128`|The pool liquidity before opening the position|
|`sqrtPriceX96`|`uint160`|The pool sqrt price before opening the position|
|`sqrtPriceX96Next`|`uint160`|The pool sqrt price after opening the position|
|`liquidityDelta`|`uint128`|The delta in pool liquidity used to collateralize the position|
|`zeroForOne`|`bool`|Whether the position is long token1 and short token0 (true), or long token0 and short token1 (false)|
|`tick`|`int24`|The pool tick before opening the position|
|`blockTimestampStart`|`uint32`|The timestamp at which the pool state was last synced before opening the position|
|`tickCumulativeStart`|`int56`|The tick cumulative value from the pool at `blockTimestampStart`|
|`oracleTickCumulativeStart`|`int56`|The tick cumulative value from the oracle at `blockTimestampStart`|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`position`|`Info`|The assembled position info|


### size

Size of position in (x, y) amounts

*Size amount in token1 if zeroForOne = true, or in token0 if zeroForOne = false*


```solidity
function size(uint128 liquidity, uint160 sqrtPriceX96, uint160 sqrtPriceX96Next, bool zeroForOne)
    internal
    pure
    returns (uint128);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`liquidity`|`uint128`|The pool liquidity before opening the position|
|`sqrtPriceX96`|`uint160`|The pool sqrt price before opening the position|
|`sqrtPriceX96Next`|`uint160`|The pool sqrt price after opening the position|
|`zeroForOne`|`bool`|Whether the position is long token1 and short token0 (true), or long token0 and short token1 (false)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint128`|The position size|


### insurances

Insurance balances to back position in (x, y) amounts


```solidity
function insurances(
    uint128 liquidity,
    uint160 sqrtPriceX96,
    uint160 sqrtPriceX96Next,
    uint128 liquidityDelta,
    bool zeroForOne
) internal pure returns (uint128 insurance0, uint128 insurance1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`liquidity`|`uint128`|The pool liquidity before opening the position|
|`sqrtPriceX96`|`uint160`|The pool sqrt price before opening the position|
|`sqrtPriceX96Next`|`uint160`|The pool sqrt price after opening the position|
|`liquidityDelta`|`uint128`|The delta in pool liquidity used to collateralize the position|
|`zeroForOne`|`bool`|Whether the position is long token1 and short token0 (true), or long token0 and short token1 (false)|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`insurance0`|`uint128`|The insurance reserves in token0 needed to prevent liquidity shortfall for late liquidations|
|`insurance1`|`uint128`|The insurance reserves in token1 needed to prevent liquidity shortfall for late liquidations|


### debts

Debts owed by position in (x, y) amounts

*Uses invariant (insurance0 + debt0) * (insurance1 + debt1) = liquidityDelta * sqrtPriceNext*


```solidity
function debts(uint160 sqrtPriceX96Next, uint128 liquidityDelta, uint128 insurance0, uint128 insurance1)
    internal
    pure
    returns (uint128 debt0, uint128 debt1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sqrtPriceX96Next`|`uint160`|The pool sqrt price after opening the position|
|`liquidityDelta`|`uint128`|The delta in pool liquidity used to collateralize the position|
|`insurance0`|`uint128`|The position insurance reserves in token0|
|`insurance1`|`uint128`|The position insurance reserves in token1|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`debt0`|`uint128`|The debt in token0 the position owes to the pool|
|`debt1`|`uint128`|The debt in token1 the position owes to the pool|


### fees

Fees owed when opening the position in (x, y) amounts

*Fees taken proportional to size*


```solidity
function fees(uint128 size, uint24 fee) internal pure returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`size`|`uint128`|The position size|
|`fee`|`uint24`|The fee rate charged on position size|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The amount of fees charged to open the position|


### liquidationRewards

Liquidation rewards required to set aside for liquidator in native (gas) token amount

*Returned on settle to position owner or used as incentive for liquidator to liquidate position when unsafe*


```solidity
function liquidationRewards(uint256 blockBaseFee, uint256 blockBaseFeeMin, uint256 gas, uint24 premium)
    internal
    pure
    returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`blockBaseFee`|`uint256`|Current block base fee|
|`blockBaseFeeMin`|`uint256`|Minimum block base fee to use in calculating cost to execute call to liquidate|
|`gas`|`uint256`|Estimated gas required to execute call to liquidate|
|`premium`|`uint24`|Liquidation premium to incentivize potential liquidators with|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The liquidation rewards to set aside for liquidator if position unsafe|


### marginMinimum

Absolute minimum margin amount required to be held in position

*Uses `position.tick` prior to position open (alongside insurance balances) to ensure repayment to pool of at least liquidityDelta liability if ignore funding*


```solidity
function marginMinimum(Info memory position, uint24 maintenance) internal pure returns (uint128);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`position`|`Info`|The position to check minimum margin amounts for|
|`maintenance`|`uint24`|The minimum maintenance margin requirement for the pool|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint128`|The minimum amount of margin the position must hold|


### amountsLocked

Amounts (x, y) of pool reserves locked in position

*Includes margin in the event position were to be liquidated*


```solidity
function amountsLocked(Info memory position) internal pure returns (uint256 amount0, uint256 amount1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`position`|`Info`|The position|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount0`|`uint256`|The amount of token0 set aside for the position|
|`amount1`|`uint256`|The amount of token1 set aside for the position|


### debtsAfterFunding

Debt adjusted for funding

*Ref @with-backed/papr/src/UniswapOracleFundingRateController.sol#L156
Follows debt0Next = debt0 * (oracleTwap / poolTwap) ** (dt / fundingPeriod) if zeroForOne = true*


```solidity
function debtsAfterFunding(
    Info memory position,
    uint32 blockTimestampLast,
    int56 tickCumulativeDeltaLast,
    uint24 tickCumulativeRateMax,
    uint32 fundingPeriod
) internal pure returns (uint128 debt0, uint128 debt1);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`position`|`Info`|The position to update debts for funding|
|`blockTimestampLast`|`uint32`|The block timestamp at the last pool state sync|
|`tickCumulativeDeltaLast`|`int56`|The delta in oracle tick cumulative minus pool tick cumulative values at `blockTimestampLast`|
|`tickCumulativeRateMax`|`uint24`|The maximum rate of change in tick cumulative between the oracle and pool `tickCumulative` values|
|`fundingPeriod`|`uint32`|The pool funding period to benchmark funding payments to|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`debt0`|`uint128`|The position debt in token0 after funding|
|`debt1`|`uint128`|The position debt in token1 after funding|


### safe

Whether the position is safe from liquidation

*If not safe, position can be liquidated
Considered safe if (`position.margin` + `position.size`) / oracleTwap >= (1 + `maintenance`) * `position.debt0` when position.zeroForOne = true
or (`position.margin` + `position.size`) * oracleTwap >= (1 + `maintenance`) * `position.debt1` when position.zeroForOne = false*


```solidity
function safe(Info memory position, uint160 sqrtPriceX96, uint24 maintenance) internal pure returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`position`|`Info`|The position to check safety of|
|`sqrtPriceX96`|`uint160`|The oracle time weighted average sqrt price|
|`maintenance`|`uint24`|The minimum maintenance margin requirement for the pool|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|true if safe and false if not safe|


## Structs
### Info

```solidity
struct Info {
    uint128 size;
    uint128 debt0;
    uint128 debt1;
    uint128 insurance0;
    uint128 insurance1;
    bool zeroForOne;
    bool liquidated;
    int24 tick;
    uint32 blockTimestamp;
    int56 tickCumulativeDelta;
    uint128 margin;
    uint128 liquidityLocked;
    uint256 rewards;
}
```

