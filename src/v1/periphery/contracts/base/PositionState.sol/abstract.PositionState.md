# PositionState
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/d846d56fa6d1e439306e60a85e98fc298babb2f7/contracts/base/PositionState.sol)


## Functions
### getStateSynced

Gets pool state synced for pool oracle updates


```solidity
function getStateSynced(address pool)
    internal
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
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`pool`|`address`|The pool to get state of|


### getOracleSynced

Gets external oracle tick cumulative values for time deltas: [secondsAgo, 0]


```solidity
function getOracleSynced(address pool) internal view returns (int56[] memory oracleTickCumulatives);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`pool`|`address`|The pool to get external oracle state for|


### getPositionSynced

Gets pool position synced for funding updates


```solidity
function getPositionSynced(address pool, address recipient, uint96 id)
    internal
    view
    returns (
        bool zeroForOne,
        uint128 size,
        uint128 debt,
        uint128 margin,
        uint128 safeMarginMinimum,
        bool liquidated,
        bool safe,
        uint256 rewards
    );
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`pool`|`address`|The pool the position is on|
|`recipient`|`address`|The recipient of the position at open|
|`id`|`uint96`|The position id|


### _safeMarginMinimum

Calculates the minimum margin requirement for the position to remain safe from liquidation

*c_y (safe) >= (1+M) * d_x * max(P, TWAP) - s_y when zeroForOne = true when no funding
or c_x (safe) >= (1+M) * d_y / min(P, TWAP) - s_x when zeroForOne = false when no funding*


```solidity
function _safeMarginMinimum(
    PositionLibrary.Info memory info,
    uint128 marginMinimum,
    uint24 maintenance,
    int56 oracleTickCumulativeDelta
) internal pure returns (uint128 safeMarginMinimum);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`info`|`PositionLibrary.Info`|The synced position info|
|`marginMinimum`|`uint128`|The margin minimum when ignoring funding and liquidation|
|`maintenance`|`uint24`|The minimum maintenance margin requirement|
|`oracleTickCumulativeDelta`|`int56`|The difference in oracle tick cumulatives averaged over to assess position safety with|


