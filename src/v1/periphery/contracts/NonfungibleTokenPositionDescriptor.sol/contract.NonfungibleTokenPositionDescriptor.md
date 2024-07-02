# NonfungibleTokenPositionDescriptor
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/d846d56fa6d1e439306e60a85e98fc298babb2f7/contracts/NonfungibleTokenPositionDescriptor.sol)

**Inherits:**
[INonfungibleTokenPositionDescriptor](/contracts/interfaces/INonfungibleTokenPositionDescriptor.sol/interface.INonfungibleTokenPositionDescriptor.md)

**Author:**
Sablier Labs

Produces a string containing the data URI for a JSON metadata string

*Fork of Sablier V2 SablierV2NFTDescriptor for Marginal V1 leverage positions. Incorporates a bit of Uniswap V3 NonfungibleTokenPositionDescriptor code.*


## Functions
### tokenURI

Produces the URI describing a particular token ID for a position manager

*Note this URI may be a data: URI with the JSON contents directly inlined*


```solidity
function tokenURI(INonfungiblePositionManager positionManager, uint256 tokenId)
    external
    view
    override
    returns (string memory);
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


### abbreviateAmount

Creates an abbreviated representation of the provided amount, rounded down and prefixed with ">= ".

*The abbreviation uses these suffixes:
- "K" for thousands
- "M" for millions
- "B" for billions
- "T" for trillions
For example, if the input is 1,234,567, the output is ">= 1.23M".*


```solidity
function abbreviateAmount(uint256 amount, uint256 decimals, string memory unit) internal pure returns (string memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amount`|`uint256`|The amount to abbreviate, denoted in units of `decimals`.|
|`decimals`|`uint256`|The number of decimals to assume when abbreviating the amount.|
|`unit`|`string`|The unit denomination of the amount.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`string`|abbreviation The abbreviated representation of the provided amount, as a string.|


### generateDescriptionPartOne

Generates a string with the first part of NFT's JSON metadata description, which provides a high-level overview.


```solidity
function generateDescriptionPartOne(
    string memory quoteTokenSymbol,
    string memory baseTokenSymbol,
    string memory poolAddress
) internal pure returns (string memory);
```

### generateDescriptionPartTwo

Generates a string with the second part of NFT's JSON metadata description, which provides a high-level overview.


```solidity
function generateDescriptionPartTwo(
    string memory tokenId,
    string memory baseTokenSymbol,
    string memory quoteTokenAddress,
    string memory baseTokenAddress,
    string memory maxLeverageTier
) internal pure returns (string memory);
```

### generateName

Generates a string with the NFT's JSON metadata name, which is unique for each tokenId.


```solidity
function generateName(string memory tokenId) internal pure returns (string memory);
```

### generateTicker

Geneartes a string with the pool ticker for the NFT's body.


```solidity
function generateTicker(string memory quoteTokenSymbol, string memory baseTokenSymbol, string memory maxLeverageTier)
    internal
    pure
    returns (string memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`quoteTokenSymbol`|`string`|The quote asset symbol of the pool|
|`baseTokenSymbol`|`string`|The base asset symbol of the pool|
|`maxLeverageTier`|`string`|The maximum leverage of the pool|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`string`|The string representation of the pool ticker|


### safeAssetDecimals

Retrieves the asset's decimals safely, defaulting to "0" if an error occurs.

*Performs a low-level call to handle assets in which the decimals are not implemented.*


```solidity
function safeAssetDecimals(address asset) internal view returns (uint8);
```

### safeAssetSymbol

Retrieves the asset's symbol safely, defaulting to a hard-coded value if an error occurs.

*Performs a low-level call to handle assets in which the symbol is not implemented or it is a bytes32
instead of a string.*


```solidity
function safeAssetSymbol(address asset) internal view returns (string memory);
```

### calculateHealthFactor

Calculates the health factor for a position


```solidity
function calculateHealthFactor(uint256 margin, uint256 safeMarginMinimum) internal pure returns (string memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`margin`|`uint256`|The position margin|
|`safeMarginMinimum`|`uint256`|The position safe margin minimum|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`string`|The health factor, as a string|


### calculateMaximumLeverage

Calculates the maximum leverage for a pool given the maintenance requirement


```solidity
function calculateMaximumLeverage(uint24 maintenance) internal pure returns (string memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`maintenance`|`uint24`|The maintenance requirement of the pool|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`string`|The string representation of maximum leverage|


### stringifyFractionalAmount

Converts the provided fractional amount to a string prefixed by a dot.


```solidity
function stringifyFractionalAmount(uint256 fractionalAmount) internal pure returns (string memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`fractionalAmount`|`uint256`|A numerical value with 2 implied decimals.|


## Structs
### TokenURIVars
*Needed to avoid Stack Too Deep.*


```solidity
struct TokenURIVars {
    string quoteTokenSymbol;
    string baseTokenSymbol;
    string maxLeverageTier;
    address tokenSize;
    address tokenDebt;
    string symbolSize;
    string symbolDebt;
    uint8 decimalsSize;
    uint8 decimalsDebt;
    bool zeroForOne;
    uint256 amountSize;
    uint256 amountDebt;
    uint256 amountMargin;
    uint256 amountSafeMarginMinimum;
    uint256 amountTotalSize;
    string healthFactor;
    address poolAddress;
    string svg;
    string json;
}
```

