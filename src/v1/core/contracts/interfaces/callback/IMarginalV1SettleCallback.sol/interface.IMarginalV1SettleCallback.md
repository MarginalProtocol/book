# IMarginalV1SettleCallback
[Git Source](https://github.com/MarginalProtocol/v1-core/blob/2d246e9b4f6e970321a0f235176b47b340c9a03b/contracts/interfaces/callback/IMarginalV1SettleCallback.sol)

Callbacks called by Marginal v1 pools when settling the debt owed by a position to the pool

*Any contract that calls IMarginalV1Pool#settle must implement this interface*


## Functions
### marginalV1SettleCallback

Called to `msg.sender` after settling a position via IMarginalV1Pool#settle

*In the implementation you must pay the pool tokens owed to settle the debt owed by a position to the pool.
Position size and margin are flashed out to `recipient` in the IMarginalV1Pool#settle call prior to enable debt repayment via swaps.
The caller of this method must be checked to be a MarginalV1Pool deployed by the canonical MarginalV1Factory.
Amount that must be payed to pool is > 0 as IMarginalV1Pool#open would have reverted otherwise.*


```solidity
function marginalV1SettleCallback(int256 amount0Delta, int256 amount1Delta, bytes calldata data) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amount0Delta`|`int256`|The amount of token0 that was sent (negative) or must be received (positive) by the pool by the end of position settlement. If positive, the callback must send that amount of token0 to the pool.|
|`amount1Delta`|`int256`|The amount of token1 that was sent (negative) or must be received (positive) by the pool by the end of position settlement. If positive, the callback must send that amount of token1 to the pool.|
|`data`|`bytes`|Any data passed through by the caller via the IMarginalV1Pool#settle call|


