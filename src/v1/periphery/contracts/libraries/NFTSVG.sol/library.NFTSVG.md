# NFTSVG
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/d846d56fa6d1e439306e60a85e98fc298babb2f7/contracts/libraries/NFTSVG.sol)

**Author:**
Sablier Labs

Generates the SVG image for the Marginal V1 leverage position

*Fork of Sablier V2 NFTSVG library adapted for Marginal V1 leverage positions*


## State Variables
### CARD_MARGIN

```solidity
uint256 internal constant CARD_MARGIN = 16;
```


## Functions
### generateSVG


```solidity
function generateSVG(SVGParams memory params) internal pure returns (string memory);
```

### generateLogo


```solidity
function generateLogo() internal pure returns (string memory);
```

### generateDefs


```solidity
function generateDefs(string memory accentColor, string memory cards) internal pure returns (string memory);
```

### generateFloatingText


```solidity
function generateFloatingText(string memory poolAddress, string memory poolTicker)
    internal
    pure
    returns (string memory);
```

### generateHrefs


```solidity
function generateHrefs(uint256 sizeXPosition, uint256 debtXPosition, uint256 marginXPosition, uint256 healthXPosition)
    internal
    pure
    returns (string memory);
```

## Structs
### SVGParams

```solidity
struct SVGParams {
    string accentColor;
    string size;
    string debt;
    string margin;
    string healthFactor;
    string poolAddress;
    string poolTicker;
}
```

### SVGVars

```solidity
struct SVGVars {
    string cards;
    uint256 cardsWidth;
    string sizeCard;
    uint256 sizeWidth;
    uint256 sizeXPosition;
    string debtCard;
    uint256 debtWidth;
    uint256 debtXPosition;
    string marginCard;
    uint256 marginWidth;
    uint256 marginXPosition;
    string healthCard;
    uint256 healthWidth;
    uint256 healthXPosition;
}
```

