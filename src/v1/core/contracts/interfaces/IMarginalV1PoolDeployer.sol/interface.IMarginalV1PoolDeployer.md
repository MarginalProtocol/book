# IMarginalV1PoolDeployer
[Git Source](https://github.com/MarginalProtocol/v1-core/blob/692b49fa7fdd08211d0090e7004215e23af735d5/contracts/interfaces/IMarginalV1PoolDeployer.sol)

The Marginal v1 pool deployer deploys new pools


## Functions
### deploy

Deploys a new Marginal v1 pool for the given unique pool key

*`msg.sender` treated as factory address for the pool*


```solidity
function deploy(address token0, address token1, uint24 maintenance, address oracle) external returns (address pool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token0`|`address`|The address of token0 for the pool|
|`token1`|`address`|The address of token1 for the pool|
|`maintenance`|`uint24`|The minimum maintenance requirement for the pool|
|`oracle`|`address`|The address of the Uniswap v3 oracle used by the pool|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`pool`|`address`|The address of the deployed Marginal v1 pool|


