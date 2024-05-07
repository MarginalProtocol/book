# INonfungibleTokenPositionDescriptor
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/3831eb0dc9ad872eeb8a0eb98bd8566331443136/contracts/interfaces/INonfungibleTokenPositionDescriptor.sol)

Describes position NFT tokens via URI


## Functions
### tokenURI

Produces the URI describing a particular token ID for a position manager

*Note this URI may be a data: URI with the JSON contents directly inlined*


```solidity
function tokenURI(INonfungiblePositionManager positionManager, uint256 tokenId) external view returns (string memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`positionManager`|`INonfungiblePositionManager`|The position manager for which to describe the token|
|`tokenId`|`uint256`|The ID of the token for which to produce a description, which may not be valid|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`string`|The URI of the ERC721-compliant metadata|


