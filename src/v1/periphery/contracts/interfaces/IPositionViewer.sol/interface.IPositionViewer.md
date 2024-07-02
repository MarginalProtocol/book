# IPositionViewer
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/d846d56fa6d1e439306e60a85e98fc298babb2f7/contracts/interfaces/IPositionViewer.sol)

Gets the synced positions on Marginal v1 pools


## Functions
### positions

Returns details of an existing position on pool


```solidity
function positions(address pool, address owner, uint96 id)
    external
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
|`pool`|`address`|The pool address position taken out on|
|`owner`|`address`|The owner address of the position|
|`id`|`uint96`|The position ID stored in the pool for the associated position|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`zeroForOne`|`bool`|Whether position settlement requires debt in of token0 for size + margin out of token1|
|`size`|`uint128`|The position size on the pool in the margin token|
|`debt`|`uint128`|The position debt owed to the pool in the non-margin token|
|`margin`|`uint128`|The margin backing the position on the pool|
|`safeMarginMinimum`|`uint128`|The minimum margin requirements necessary to keep position open on pool while also being safe from liquidation|
|`liquidated`|`bool`|Whether the position has been liquidated|
|`safe`|`bool`|Whether the position can be liquidated|
|`rewards`|`uint256`|The reward available to liquidators when position not safe|


