# OracleLibrary
[Git Source](https://github.com/MarginalProtocol/v1-core/blob/4dcf410464dd1b73aaabe9fa06bd3450c672d3b9/contracts/libraries/OracleLibrary.sol)

Enables calculation of the geometric time weighted average price


## Functions
### oracleSqrtPriceX96

Returns the geometric time weighted average sqrtP

*Rounds toward zero for both positive and negative tick delta*


```solidity
function oracleSqrtPriceX96(int56 tickCumulativeDelta, uint32 timeDelta) internal pure returns (uint160);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tickCumulativeDelta`|`int56`|The delta in tick cumulative over the averaging interval|
|`timeDelta`|`uint32`|The time to average over|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint160`|The geometric time weighted average price|


### oracleTickCumulativeDelta

Returns the tick cumulative delta over an interval

*Allows for tick cumulative overflow*


```solidity
function oracleTickCumulativeDelta(int56 tickCumulativeStart, int56 tickCumulativeEnd) internal pure returns (int56);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tickCumulativeStart`|`int56`|The tick cumulative value at the start of the interval|
|`tickCumulativeEnd`|`int56`|The tick cumulative value at the end of the interval|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`int56`|The delta in tick cumulative over the averaging interval|


