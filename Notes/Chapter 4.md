# Chapter 4: Voting Contracts and Inheritance in Solidity

This chapter explores a practical application of Solidity through a voting contract, a real-world example of decentralized governance, and introduces inheritance, a feature that allows contracts to reuse and extend existing code. These concepts demonstrate how Solidity enables flexible and modular smart contract design.

## Overview

A voting contract allows members to propose and vote on actions, executing them only if enough support is received, mimicking decentralized decision-making. Inheritance enables developers to build on existing contracts, reusing common patterns and adding new functionality. Together, these features showcase Solidity’s power in creating secure and reusable decentralized applications (dApps).

## Key Concepts

### 1. Voting: A Real-World Contract

A voting contract is a smart contract that enables decentralized governance, where members propose actions, vote on them, and execute approved proposals. This setup is common in Decentralized Autonomous Organizations (DAOs), where collective decision-making governs actions like fund allocation or protocol upgrades.

#### How It Works

- **Proposals**: Any member can submit a proposal, which includes calldata specifying an action (e.g., a message call to another contract).
- **Voting**: Members vote to approve or reject the proposal (e.g., “yes” or “no”).
- **Threshold**: If the proposal receives enough “yes” votes (a predefined threshold), it is executed.
- **Execution**: The contract performs the action encoded in the proposal’s calldata, such as transferring funds, buying an NFT, or calling another contract.

#### Why It’s Powerful

The voting contract acts like an Externally Owned Account (EOA) (e.g., a user’s wallet) but requires voter approval for every action. This ensures transparency and collective control. Since proposals use calldata, they can trigger virtually any action, from simple Ether transfers to complex interactions with other contracts.

*Example*: 
    ```solidity
    contract Voting {
        struct Proposal {
            address target; // Contract to call
            bytes calldata; // Function and arguments to execute
            uint yesVotes; // Count of yes votes
            bool executed; // Has the proposal been executed?
        }
    
        Proposal[] public proposals;
        mapping(address => bool) public members; // Tracks valid voters
        uint public threshold = 3; // Minimum yes votes needed
    
        constructor() {
            members[msg.sender] = true; // Deployer is a member
        }
    
        function propose(address _target, bytes memory _calldata) public {
            require(members[msg.sender], "Not a member");
            proposals.push(Proposal(_target, _calldata, 0, false));
        }
    
        function vote(uint proposalId) public {
            require(members[msg.sender], "Not a member");
            Proposal storage proposal = proposals[proposalId];
            require(!proposal.executed, "Already executed");
            proposal.yesVotes += 1;
        }
    
        function execute(uint proposalId) public {
            Proposal storage proposal = proposals[proposalId];
            require(proposal.yesVotes >= threshold, "Not enough votes");
            require(!proposal.executed, "Already executed");
            proposal.executed = true;
            (bool success, ) = proposal.target.call(proposal.calldata);
            require(success, "Execution failed");
        }
    }

- **propose**: Members submit a proposal with a target contract and calldata.
- **vote**: Members increment the yes vote count for a proposal.
- **execute**: If the vote threshold is met, the contract calls the target with the provided calldata.
- **Security**: Uses `require` to enforce membership, vote thresholds, and execution status.

#### Use Cases

- **DAO Governance**: Approving budget allocations or protocol changes.
- **Crowdfunding**: Releasing funds only with member approval.
- **NFT Purchases**: Collectively buying assets like digital art.

#### Caution

- **Gas Costs**: Executing complex calldata can be expensive.
- **Security**: Validate calldata and ensure only trusted contracts are called to prevent malicious actions.

### 2. Inheritance

Inheritance allows a contract (the child) to inherit code from another contract (the parent), reusing common functionality and extending it with new features. This promotes modularity and reduces code duplication, making contracts easier to maintain and audit.

#### How It Works

- **Inheritance**: A child contract inherits all functions (except private ones) and state variables from the parent.
- **Override**: The child can override inherited functions to customize behavior.
- **Standards**: Inheritance is often used to implement common patterns, like ERC20 (tokens) or ERC721 (NFTs).

*Example*: 
    ```solidity
    contract Ownable {
        address public owner;
    
        constructor() {
            owner = msg.sender;
        }
    
        modifier onlyOwner() {
            require(msg.sender == owner, "Not owner");
            _;
        }
    }
    
    contract MyContract is Ownable {
        uint public value;
    
        function setValue(uint _value) public onlyOwner {
            value = _value; // Only the owner can set the value
        }
    }

- **Ownable**: A parent contract that tracks an owner and provides an `onlyOwner` modifier.
- **MyContract**: Inherits from Ownable using `is Ownable`, gaining owner and `onlyOwner`.
- **setValue**: Uses `onlyOwner` to restrict access, demonstrating reused functionality.

#### Key Features

- **Access**: 
  - Public/Internal: Functions and variables are inherited.
  - Private: Not inherited, keeping sensitive logic hidden.

- **Override**: Use the `override` keyword to redefine a parent’s function.
      ```solidity
      function setValue(uint _value) public override onlyOwner {
        value = _value * 2; // Custom logic
    }

- **Multiple Inheritance**: A contract can inherit from multiple parents using `is Parent1, Parent2`.

#### Use Cases

- **Standards**: Implement ERC20 for tokens or ERC721 for NFTs by inheriting from standard contracts.
- **Modularity**: Reuse access control (e.g., Ownable) or pausability patterns.
- **Customization**: Extend base contracts with project-specific logic.

#### Caution

- **Complexity**: Multiple inheritance can lead to conflicts (e.g., the “diamond problem”); use carefully.
- **Gas Costs**: Inherited code increases contract size, impacting deployment costs.

## Summary

Voting contracts enable decentralized governance by allowing members to propose, vote on, and execute actions via calldata, acting like a collective EOA. Inheritance promotes code reuse by letting child contracts inherit and extend parent contract functionality, supporting modular design and standards like ERC20. These features empower developers to build flexible, secure, and community-driven dApps on Ethereum.

This document is part of a series of notes on Solidity and Ethereum development. For more details, refer to the Solidity documentation. See Chapter 1 for value types and functions, Chapter 2 for message calls, and Chapter 3 for reference types.
