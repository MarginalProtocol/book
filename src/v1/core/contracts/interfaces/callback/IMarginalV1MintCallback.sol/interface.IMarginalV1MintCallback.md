# IMarginalV1MintCallback
[Git Source](https://github.com/MarginalProtocol/v1-core/blob/692b49fa7fdd08211d0090e7004215e23af735d5/contracts/interfaces/callback/IMarginalV1MintCallback.sol)

Callbacks called by Marginal v1 pools when adding liquidity

*Any contract that calls IMarginalV1Pool#mint must implement this interface*


## Functions
### marginalV1MintCallback

Called to `msg.sender` after adding liquidity via IMarginalV1Pool#mint

*In the implementation you must pay the pool tokens owed to add liquidity to the pool and mint LP tokens.
The caller of this method must be checked to be a MarginalV1Pool deployed by the canonical MarginalV1Factory.*


```solidity
function marginalV1MintCallback(uint256 amount0Owed, uint256 amount1Owed, bytes calldata data) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amount0Owed`|`uint256`|The amount of token0 that must be payed to pool to successfully mint LP tokens|
|`amount1Owed`|`uint256`|The amount of token1 that must be payed to pool to successfully mint LP tokens|
|`data`|`bytes`|Any data passed through by the caller via the IMarginalV1Pool#mint call|


