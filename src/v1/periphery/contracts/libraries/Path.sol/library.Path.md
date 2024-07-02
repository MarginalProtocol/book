# Path
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/d846d56fa6d1e439306e60a85e98fc298babb2f7/contracts/libraries/Path.sol)

*Fork of Uniswap V3 periphery Path.sol*


## State Variables
### ADDR_SIZE
*The length of the bytes encoded address*


```solidity
uint256 private constant ADDR_SIZE = 20;
```


### MAINTENANCE_SIZE
*The length of the bytes encoded maintenance*


```solidity
uint256 private constant MAINTENANCE_SIZE = 3;
```


### NEXT_OFFSET
*The offset of a single token address, pool maintenance, and oracle*


```solidity
uint256 private constant NEXT_OFFSET = ADDR_SIZE + MAINTENANCE_SIZE + ADDR_SIZE;
```


### POP_OFFSET
*The offset of an encoded pool key*


```solidity
uint256 private constant POP_OFFSET = NEXT_OFFSET + ADDR_SIZE;
```


### MULTIPLE_POOLS_MIN_LENGTH
*The minimum length of an encoding that contains 2 or more pools*


```solidity
uint256 private constant MULTIPLE_POOLS_MIN_LENGTH = POP_OFFSET + NEXT_OFFSET;
```


## Functions
### hasMultiplePools

Returns true iff the path contains two or more pools


```solidity
function hasMultiplePools(bytes memory path) internal pure returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`path`|`bytes`|The encoded swap path|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|True if path contains two or more pools, otherwise false|


### numPools

Returns the number of pools in the path


```solidity
function numPools(bytes memory path) internal pure returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`path`|`bytes`|The encoded swap path|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The number of pools in the path|


### decodeFirstPool

Decodes the first pool in path


```solidity
function decodeFirstPool(bytes memory path)
    internal
    pure
    returns (address tokenA, address tokenB, uint24 maintenance, address oracle);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`path`|`bytes`|The bytes encoded swap path|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`tokenA`|`address`|The first token of the given pool|
|`tokenB`|`address`|The second token of the given pool|
|`maintenance`|`uint24`|The maintenance level of the pool|
|`oracle`|`address`|The oracle referenced by the given pool|


### getFirstPool

Gets the segment corresponding to the first pool in the path


```solidity
function getFirstPool(bytes memory path) internal pure returns (bytes memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`path`|`bytes`|The bytes encoded swap path|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes`|The segment containing all data necessary to target the first pool in the path|


### skipToken

Skips a token + maintenance + oracle element from the buffer and returns the remainder


```solidity
function skipToken(bytes memory path) internal pure returns (bytes memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`path`|`bytes`|The swap path|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes`|The remaining token + maintenance + oracle elements in the path|


