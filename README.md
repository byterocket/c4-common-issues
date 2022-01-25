<h1 align=center><code>c4-common-issues</code></h1>

This repository aims to provide a list of issues found regularly in [Code4Rena](https://code4rena.com/)
contests.

## Introduction

Code4Rena runs community-driven contests for smart contract audits in which
wardens search for issues and judges allocate awards to wardens based on performance.

A problem currently in the community is how to handle commonly found issues
as they increase the judge's workload.

This repo aims to identify common issues and provide background information.

The goal is, that wardens include the issue's identifier in a contest submittion.

This would help judges mark the issues as duplicates and hopefully decrease
their workload.


## Gas Optimization Issues

| Identifier | Title |
|------------|-------|
| [G001](./0-Gas-Optimizations.md/#g001---dont-initialize-variables-with-default-value) | Don't Initialize Variables with Default Value |
| [G002](./0-Gas-Optimizations.md/#g002---cache-array-length-outside-of-loop) | Cache Array Length Outside of Loop |
| [G003](./0-Gas-Optimizations.md/#g003---use--0-instead-of--0-for-unsigned-integer-comparison) | Use `!= 0` instead of `> 0` for Unsigned Integer Comparison |
| [G004](./0-Gas-Optimizations.md/#g004---remove-unused-variables) | Remove Unused Variables |
| [G005](./0-Gas-Optimizations.md/#g005---make-variable-constantimmutable) | Make Variable `constant`/`immutable` |
| [G006](./0-Gas-Optimizations.md/#g006---use-immutable-for-openzeppelin-accesscontrols-roles-declarations) | Use `immutable` for OpenZeppelin `AccessControl`'s Roles Declarations |
| [G007](./0-Gas-Optimizations.md/#g007---long-revert-strings) | Long Revert Strings |
| [G008](./0-Gas-Optimizations.md/#g008---use-shift-rightleft-instead-of-divisionmultiplication-if-possible) | Use Shift Right/Left instead of Division/Multiplication if possible |
| [G009](./0-Gas-Optimizations.md/#g009---make-function-external-instead-of-public) | Make Function `external` instead of `public` |
| [G010](./0-Gas-Optimizations.md/#g010---make-function-payable) | Make Function `payable` |


## Non-Critial Issues

| Identifier | Title |
|------------|-------|
| [NC001](./1-Non-Critial.md#nc001---functions-mutating-storage-should-emit-events) | Functions Mutating Storage Should Emit Events |


## Low Risk Issues

| Identifier | Title |
|------------|-------|
| [L001](./2-Low-Risk.md#l001---unsafe-erc20-operations) | Unsafe ERC20 Operation(s) |
| [L002](./2-Low-Risk.md#l002---feeontransfer-tokens-not-supported) | FeeOnTransfer Tokens not Supported |
| [L003](./2-Low-Risk.md#l003---unspecific-compiler-version-pragma) | Unspecific Compiler Version Pragma |
| [L004](./2-Low-Risk.md#l004---use-two-step-transfer-pattern-for-access-controls) | Use Two-Step Transfer Pattern for Access Controls |


## Contribution

**Any** kind of contribution is highly welcome!


## License

This work is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
