Ì¥∞ Lesson 1: Introduction to Solidity
In this first lesson, I got introduced to Solidity, the main programming language used for writing smart contracts on the Ethereum blockchain. The idea of smart contracts was super interesting to me ‚Äî it's like making code that can run itself on the blockchain without anyone needing to trust each other.

Smart contracts are self-executing and once deployed, they can‚Äôt be easily changed. This means they can be used for serious things like money transfers, voting, or record-keeping ‚Äî all without middlemen.

Solidity is influenced by JavaScript and C++, so it felt somewhat familiar but still very different because it interacts with the blockchain in a special way.

Ì∑Æ Lesson 2: Variables
This lesson helped me understand how to store data inside smart contracts using variables.

State variables: These are stored permanently on the blockchain. They exist outside of functions and are part of the contract‚Äôs long-term memory.

Local variables: These are temporary. They are only used within functions and disappear after the function runs.

Global variables: These are special built-in variables provided by Solidity that give info about the blockchain environment. For example, msg.sender tells us who called the function, and block.timestamp tells us the current block‚Äôs timestamp.

Variables are the foundation for keeping track of important data in contracts.

‚öôÔ∏è Lesson 3: Functions
Functions are the actions of a smart contract. This lesson showed me how to define and use functions to do things like update data, send ETH, or calculate values.

There are different types of functions:

view: Only reads state, doesn't change anything

pure: Doesn‚Äôt even read anything from the contract, just uses logic

public: Anyone can call it

private: Only available inside the contract

Functions help organize code and make it reusable. I also learned to use parameters and return values to make my functions more powerful.

Ì¥í Lesson 4: Visibility
In this part, I learned about how visibility works in Solidity, which controls who can access variables and functions.

public: Can be called by anyone, including external users and other contracts.

private: Can only be used inside the contract where it‚Äôs defined.

internal: Can be used in the current contract and contracts that inherit from it.

external: Meant to be called only from outside the contract (like by other contracts or users).

Setting visibility properly helps keep the contract secure and organized ‚Äî I shouldn't expose everything to the public.

Ì∑æ Lesson 5: Data Types
Solidity supports many data types, and I learned to choose them carefully depending on what kind of data I want to store:

uint: unsigned integer (only positive numbers, commonly used)

int: can be positive or negative

bool: stores true or false

string: for text

address: stores Ethereum addresses (very important for interacting with users or contracts)

Picking the right data type helps with efficiency and clarity, especially when working with gas costs.

Ì∑∫ Lesson 6: Arrays
Arrays are used to store multiple values of the same type. I can think of them like a list or collection. Solidity supports:

Fixed-size arrays ‚Äî example: uint[3] ‚Äî this can only hold exactly 3 numbers

Dynamic arrays ‚Äî example: uint[] ‚Äî this can grow or shrink as needed

Useful things I can do with arrays:

.push(value) ‚Äî adds a value

array[index] ‚Äî gets a value at a certain position

array.length ‚Äî gives me how many items are in the array

delete array[index] ‚Äî deletes a value (but doesn‚Äôt shrink the array)

One important thing is to be careful with arrays when it comes to gas usage, especially if the array gets large. Looping over arrays can cost a lot of gas

