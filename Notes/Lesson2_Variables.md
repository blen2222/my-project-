# Lesson 2: Variables in Solidity

## í·  What Are Variables?
Variables are used to store data in smart contracts. Solidity supports several types of variables based on data types and access scope.

---

## í·‚ Types of Variables

### 1. **State Variables**
- Declared **outside** functions.
- Stored on the blockchain permanently.
```solidity
uint public number;
string name;
function setNum() public {
    uint x = 5;
}
address sender = msg.sender;
pragma solidity ^0.8.0;

contract Example {
    uint public myNumber = 100;

    function getSender() public view returns (address) {
        return msg.sender;
    }
}

