# IMarginalV1OpenCallback
[Git Source](https://github.com/MarginalProtocol/v1-core/blob/692b49fa7fdd08211d0090e7004215e23af735d5/contracts/interfaces/callback/IMarginalV1OpenCallback.sol)

Callbacks called by Marginal v1 pools when opening a position

*Any contract that calls IMarginalV1Pool#open must implement this interface*


## Functions
### marginalV1OpenCallback

Called to `msg.sender` after opening a position via IMarginalV1Pool#open

*In the implementation you must pay the pool tokens owed to open a position.
The pool tokens owed are the margin and fees required to open the position.
The caller of this method must be checked to be a MarginalV1Pool deployed by the canonical MarginalV1Factory.*


```solidity
function marginalV1OpenCallback(uint256 amount0Owed, uint256 amount1Owed, bytes calldata data) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amount0Owed`|`uint256`|The amount of token0 that must be payed to pool to successfully open a position|
|`amount1Owed`|`uint256`|The amount of token1 that must be payed to pool to successfully open a position|
|`data`|`bytes`|Any data passed through by the caller via the IMarginalV1Pool#open call|


