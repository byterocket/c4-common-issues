# Non-Critial Issues

## NC001 - Functions Mutating Storage Should Emit Events

### Description

Functions mutating storage should emit an Event for easy off-chain monitoring.

### Example

🤦 Bad:
```solidity
function setFee(uint256 _fee) external onlyOwner {
    fee = _fee;
}
```

🚀 Good:
```solidity
function setFee(uint256 _fee) external onlyOwner {
    emit ChangedFee(fee, _fee);
    fee = _fee;
}
```

### Background Information

- [RariCapital's solcurity - T2](https://github.com/Rari-Capital/solcurity#contract)