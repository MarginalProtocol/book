# TransferHelper
[Git Source](https://github.com/MarginalProtocol/v1-core/blob/2d246e9b4f6e970321a0f235176b47b340c9a03b/contracts/libraries/TransferHelper.sol)

Facilitates safe transfers of ERC20 tokens and native chain token


## Functions
### safeTransfer

Transfers an ERC20 token amount from this address

*If value > balance, transfers balance of this address*


```solidity
function safeTransfer(address token, address to, uint256 value) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`address`|The address of the ERC20 to transfer|
|`to`|`address`|The address of the recipient|
|`value`|`uint256`|The desired amount of tokens to transfer|


### safeTransferETH

Transfers an amount of native (gas) token from this address

*Ref @uniswap/v3-periphery/contracts/libraries/TransferHelper.sol#L56*


```solidity
function safeTransferETH(address to, uint256 value) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`to`|`address`|The address of the recipient|
|`value`|`uint256`|The amount of ETH to transfer|


