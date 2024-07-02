# IMarginalV1AdjustCallback
[Git Source](https://github.com/MarginalProtocol/v1-core/blob/2d246e9b4f6e970321a0f235176b47b340c9a03b/contracts/interfaces/callback/IMarginalV1AdjustCallback.sol)

Callbacks called by Marginal v1 pools when adjusting the margin backing a position

*Any contract that calls IMarginalV1Pool#adjust must implement this interface*


## Functions
### marginalV1AdjustCallback

Called to `msg.sender` after adjusting the margin backing a position via IMarginalV1Pool#adjust

*In the implementation you must pay the pool tokens owed to adjust the margin backing a position. The tokens owed
is the new position margin, as the original margin is flashed out to `recipient` in the IMarginalV1Pool#adjust call.
The caller of this method must be checked to be a MarginalV1Pool deployed by the canonical MarginalV1Factory.*


```solidity
function marginalV1AdjustCallback(uint256 amount0Owed, uint256 amount1Owed, bytes calldata data) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amount0Owed`|`uint256`|The amount of token0 that must be payed to pool to successfully adjust the margin backing a position|
|`amount1Owed`|`uint256`|The amount of token1 that must be payed to pool to successfully adjust the margin backing a position|
|`data`|`bytes`|Any data passed through by the caller via the IMarginalV1Pool#adjust call|


