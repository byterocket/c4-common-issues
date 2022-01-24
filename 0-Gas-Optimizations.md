# Gas Optimizations

## G001 - Don't Initialize Variables with Default Value

### Description

Uninitialized variables are assigned with the types default value.

Explicitly initializing a variable with it's default value costs unnecesary gas.

### Example

🤦 Bad:
```solidity
uint256 x = 0;
bool y = false;
```

🚀 Good:
```solidity
uint256 x;
bool y;
```

### Background Information

- [Mudit Gupta's Blog](https://mudit.blog/solidity-tips-and-tricks-to-save-gas-and-reduce-bytecode-size/)


## G002 - Cache Array Length Outside of Loop

### Description

Caching the array length outside a loop saves reading it on each iteration, as
long as the array's length is not changed during the loop.

### Example

🤦 Bad:
```solidity
for (uint256 i = 0; i < array.length; i++) {
    // invariant: array's length is not changed
}
```

🚀 Good:
```solidity
uint256 len = array.length
for (uint256 i = 0; i < len; i++) {
    // invariant: array's length is not changed
}
```

### Background Information

- [Issue submitted by WatchPug](https://github.com/code-423n4/2021-11-badgerzaps-findings/issues/36)


## G003 - Use `!= 0` instead of `> 0` for Unsigned Integer Comparison

### Description

When dealing with unsigned integer types, comparisons with `!= 0` are cheaper
then with `> 0`.

### Example

🤦 Bad:
```solidity
// `a` being of type unsigned integer
require(a > 0, "!a > 0");
```

🚀 Good:
```solidity
// `a` being of type unsigned integer
require(a != 0, "!a > 0");
```

### Background Information

TODO


## G004 - Remove Unused Variables

### Description

Removing unused variables saves gas, especially for state variables, i.e.
variables saved in storage.


## G005 - Make Variable `constant`/`immutable`

### Description

Making variables constant/immutable, if possible, saves gas as all variables
get replaced by the values assigned to the them.

### Background Information

- [Solidity docs](https://docs.soliditylang.org/en/latest/contracts.html?highlight=constant#constant)
- [RariCapitals solcurity](https://github.com/Rari-Capital/solcurity#variables)


## G006 - Use `immutable` for OpenZeppelin `AccessControl`'s Roles Declarations

### Description

Access roles marked as `constant` results in computing the `keccak256` operation
each time the variable is used because assigned opeartions for `constant`
variables are re-evaluated every time.

Changing the variables to `immutable` results in computing the hash only once
on deployment, leading to gas savings.

### Example

🤦 Bad:
```solidity
bytes32 public constant GOVERNOR_ROLE = keccak256("GOVERNOR_ROLE");
```

🚀 Good:
```solidity
bytes32 public immutable GOVERNOR_ROLE = keccak256("GOVERNOR_ROLE");
```

### Background Information

- [Solidity issue](https://github.com/ethereum/solidity/issues/9232)


## G007 - Long Revert Strings

### Description

Shortening revert strings to fit in 32 bytes will decrease gas costs for
deployment and gas costs when the revert condition has been met.

If the contract(s) in scope allow using Solidity `>= 0.8.4`, consider using
[Custom Errors](https://blog.soliditylang.org/2021/04/21/custom-errors/) as
they are more gas efficient while allowing developers to describe the error
in detail using [NatSpec](https://docs.soliditylang.org/en/latest/natspec-format.html).

### Example

🤦 Bad:
```solidity
require(condition, "UniswapV3: The reentrancy guard. A transaction cannot re-enter the pool mid-swap");
```

🚀 Good (with shorter string):
```solidity
// TODO: Provide link to a reference of error codes
require(condition, "LOK");
```

🚀 Good (with custom errors):
```solidity
/// @notice A transaction cannot re-enter the pool mid-swap.
error NoReentrancy();

// ...

if (!condition) {
    revert NoReentrancy();
}
```

### Background Information

- [C4 Issue with a deeper explanation](https://github.com/code-423n4/2021-09-sushimiso-findings/issues/134)
- [Uniswap V3 Error Code](https://docs.uniswap.org/protocol/reference/error-codes)


## G008 - Shift Right instead of Dividing by 2

### Description

A division by 2 can be calculated by shifting one to the right.

While the `DIV` opcode uses 5 gas, the `SHR` opcode only uses 3 gas.
Furthermore, Solidity's division operation also includes a division-by-0
prevention which is bypassed using shifting.

### Example

🤦 Bad:
```solidity
uint256 b = a / 2;
```

🚀 Good:
```solidity
uint256 b = a >> 1;
```

### Background Information

- [EVM Opcodes](https://www.evm.codes/)


## G009 - Make Function `external` instead of `public`

### Description

While `external` functions can read directly from calldata, for `public`
functions Solidity copies the arguments to memory.

Furthermore, as `public` grants more access rights to a function than
`external`, consider using `external` as default and only use `public` if there
are explicit reasons.

### Background Information

- [Gustavo (Gus) Guimaraes post](https://gus-tavo-guim.medium.com/public-vs-external-functions-in-solidity-b46bcf0ba3ac)
- [StackOverflow answer](https://ethereum.stackexchange.com/questions/19380/external-vs-public-best-practices?answertab=active#tab-top)


## G010 - Make Function `payable`

### Description

Functions marked as `paybale` are slightly cheaper than non-`payable` ones,
because the Solidity compiler inserts a check into non-`payable` functions
requiring `msg.value` to be zero.

However, keep in mind that this optimization opens the door for a whole set of
security considerations involving Ether held in contracts.

### Background Information

- [Solidity Compiler Discussion](https://github.com/ethereum/solidity/issues/12539)