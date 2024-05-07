# SVGElements
[Git Source](https://github.com/MarginalProtocol/v1-periphery/blob/3831eb0dc9ad872eeb8a0eb98bd8566331443136/contracts/libraries/SVGElements.sol)

**Author:**
Sablier Labs

Generates SVG elements for the Marginal V1 leverage position

*Fork of Sablier V2 SVGElements library addapted for Marginal V1 leverage positions*


## State Variables
### BACKGROUND

```solidity
string internal constant BACKGROUND =
    '<rect width="100%" height="100%" filter="url(#Noise)"/><rect x="70" y="70" width="860" height="860" fill="#fff" fill-opacity=".03" rx="45" ry="45" stroke="#fff" stroke-opacity=".1" stroke-width="4"/>';
```


### BACKGROUND_COLOR

```solidity
string internal constant BACKGROUND_COLOR = "hsl(0,0%,10%)";
```


### ACCENT_COLOR

```solidity
string internal constant ACCENT_COLOR = "hsl(19,99%,57%)";
```


### FLOATING_TEXT

```solidity
string internal constant FLOATING_TEXT =
    '<path id="FloatingText" fill="none" d="M125 45h750s80 0 80 80v750s0 80 -80 80h-750s-80 0 -80 -80v-750s0 -80 80 -80"/>';
```


### GLOW

```solidity
string internal constant GLOW = '<circle id="Glow" r="500" fill="url(#RadialGlow)"/>';
```


### NOISE

```solidity
string internal constant NOISE =
    '<filter id="Noise"><feFlood x="0" y="0" width="100%" height="100%" flood-color="hsl(0,0%,10%)" flood-opacity="1" result="floodFill"/><feTurbulence baseFrequency=".4" numOctaves="3" result="Noise" type="fractalNoise"/><feBlend in="Noise" in2="floodFill" mode="soft-light"/></filter>';
```


### SIGN_GE
*Escape character for "≥".*


```solidity
string internal constant SIGN_GE = "&#8805;";
```


### SIGN_GT
*Escape character for ">".*


```solidity
string internal constant SIGN_GT = "&gt;";
```


### SIGN_LT
*Escape character for "<".*


```solidity
string internal constant SIGN_LT = "&lt;";
```


## Functions
### card


```solidity
function card(CardType cardType, string memory content) internal pure returns (uint256 width, string memory card_);
```

### floatingText


```solidity
function floatingText(string memory offset, string memory text) internal pure returns (string memory);
```

### gradients


```solidity
function gradients(string memory accentColor) internal pure returns (string memory);
```

### calculatePixelWidth

Calculates the pixel width of the provided string.

*Notes:
- A factor of ~0.6 is applied to the two font sizes used in the SVG (26px and 22px) to approximate the average
character width.
- It is assumed that escaped characters are placed at the beginning of `text`.
- It is further assumed that there is no other semicolon in `text`.*


```solidity
function calculatePixelWidth(string memory text, bool largeFont) internal pure returns (uint256 width);
```

### stringifyCardType

Retrieves the card type as a string.


```solidity
function stringifyCardType(CardType cardType) internal pure returns (string memory);
```

## Enums
### CardType

```solidity
enum CardType {
    POSITION_SIZE,
    POSITION_DEBT,
    POSITION_MARGIN,
    HEALTH_FACTOR
}
```

