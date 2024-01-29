# IMarginalV1SwapCallback
[Git Source](https://github.com/MarginalProtocol/v1-core/blob/692b49fa7fdd08211d0090e7004215e23af735d5/contracts/interfaces/callback/IMarginalV1SwapCallback.sol)

Callbacks called by Marginal v1 pools when executing a swap

*Any contract that calls IMarginalV1Pool#swap must implement this interface*


## Functions
### marginalV1SwapCallback

Called to `msg.sender` after executing a swap via IMarginalV1Pool#swap

*In the implementation you must pay the pool tokens owed for the swap.
The caller of this method must be checked to be a MarginalV1Pool deployed by the canonical MarginalV1Factory.
Amount that must be payed to pool is > 0 as IMarginalV1Pool#swap reverts otherwise.*


```solidity
function marginalV1SwapCallback(int256 amount0Delta, int256 amount1Delta, bytes calldata data) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amount0Delta`|`int256`|The amount of token0 that was sent (negative) or must be received (positive) by the pool by the end of the swap. If positive, the callback must send that amount of token0 to the pool.|
|`amount1Delta`|`int256`|The amount of token1 that was sent (negative) or must be received (positive) by the pool by the end of the swap. If positive, the callback must send that amount of token1 to the pool.|
|`data`|`bytes`|Any data passed through by the caller via the IMarginalV1Pool#swap call|


