# Metacrafters- ETH + AVAX PROOF: Intermediate EVM Course - Module 4
## Description

This course teaches how to build decentralized applications (Dapps) on the Ethereum blockchain and Avalanche using the Solidity programming language.
The course teaches how to create smart contracts, connect them to wallets, build a user interface, and deploy your Dapps. This is the detailed review of the fourth module of the same course. 

## Getting Started
For this project, my task is to create a ERC20 token and deploy it on the Avalanche network for Degen Gaming. The smart contract should have the following functionality:

Minting new tokens: The platform should be able to create new tokens and distribute them to players as rewards. Only the owner can mint tokens, 
 Transferring tokens: Players should be able to transfer their tokens to others,
  Redeeming tokens: Players should be able to redeem their tokens for items in the in-game store,
  Checking token balance: Players should be able to check their token balance at any time,
  Burning tokens: Anyone should be able to burn tokens, that they own, that are no longer needed
  ## Code explanation
```javascript
pragma solidity ^0.8.18;

contract DegenToken {
    string public name = "Degen";
    string public symbol = "DGN";
    uint public totalSupply;
    address public owner;
    string public Redemption_Status;

```
For the contract DegenToken, various public variables are declared using string(name, symbol, Redemption_Status), 
address(owner) and uint (totalSupply) 
   
Next, 
```javascript
 mapping(address => uint) public balanceOf;

    modifier onlyOwner() {
        require(msg.sender == owner, "Only the owner can call this function.");
        _;
```
 This mapping functipn stores the balance of each user in the contract. The key of the mapping is the address of the user and the value of the mapping is the user's balance.The modifier onlyOwner() {require(msg.sender == owner, "Only the owner can call this function."); _;} line ensures that only the owner of the contract can call the function that it is attached to.
 
```javascript
      constructor(uint initialSupply) {
        totalSupply = initialSupply;
        balanceOf[msg.sender] = totalSupply;
        owner = msg.sender;
```
The constructor initializes the contract with the total supply of tokens and sets the owner of the contract.totalSupply = initialSupply; sets the totalSupply variable to the value of the initialSupply parameter. This is the total number of tokens that will be created initially. balanceOf[msg.sender] = totalSupply; sets the balanceOf variable for the person deploying the contract to the totalSupply. This means that the person deploying the contract will own all of the tokens initially. owner = msg.sender; sets the owner variable to the person deploying the contract.


```javascript

    function transfer(address to, uint Amount) external returns (bool) {
        require(to != address(0), "Invalid recipient address.");
        require(Amount <= balanceOf[msg.sender], "Insufficient balance.");

        balanceOf[msg.sender] -= Amount;
        balanceOf[to] += Amount;
        return true;
```
function transfer(address to, uint Amount) external returns (bool) {

This line declares the transfer() function, which means that it can be called by anyone. The function takes two parameters: the address of the recipient and the amount of tokens to transfer. The function returns a boolean value, indicating whether or not the transfer was successful.

require(to != address(0), "Invalid recipient address.");

This line checks to make sure that the recipient address is not the zero address. If the recipient address is the zero, the function will show "Invalid recipient address."

require(Amount <= balanceOf[msg.sender], "Insufficient balance.");

This line checks to make sure that the sender has enough tokens to transfer the specified amount. If the sender does not have enough tokens, the function will show "Insufficient balance."


balanceOf[msg.sender] -= Amount;
balanceOf[to] += Amount;

These two lines subtract the specified amount of tokens from the sender's balance and add the specified amount of tokens to the recipient's balance.


return true;

This line returns true to indicate that the transfer was successful.




```javascript
function mint(address to, uint Amount) external onlyOwner {
        require(to != address(0), "Invalid recipient address.");
        totalSupply += Amount;
        balanceOf[to] += Amount;
```
The mint() function allows the owner of the contract to create new tokens and deposit them into a wallet address. The tokens after minting is added to the total supply of the token.
```javascript
    function burn(uint Amount) external {
        require(Amount <= balanceOf[msg.sender], "Insufficient balance.");

        balanceOf[msg.sender] -= Amount;
        totalSupply -= Amount;
```
 The burn() function allows the owner of the contract to destroy tokens from a wallet address. If the specified wallet address has amount less than or equal to the balance of the sender then it will show error. At last the sent amount is reduced from the sender's address and reduce the total suppply of the token by specified amount.
 ```javascript
 function transferFrom(address from, address to, uint Amount) external returns (bool) {
        require(to != address(0), "Invalid recipient address.");
        require(Amount <= balanceOf[from], "Insufficient balance.");
        balanceOf[from] -= Amount;
        balanceOf[to] += Amount;
        return true;
```
The transferFrom() function is used here to provide a facility to transfer token from one user's account to another user's account. the function returns a boolean value. It is required to provide a valid address which is not zero. It will show "Invalid recipient address." id address is given zero. Also the from address should have a balance greater than the amount specified to send. Or else it will show "Insufficient balance." And atlast the amount is substracted from the from address account and added to the to address account. After this it returns true to indicate that the transaction is successful.   
 ```javascript
function Redeem(uint prizeCost) external {
        require(balanceOf[msg.sender] >= prizeCost, "Insufficient balance for the prize.");
        balanceOf[msg.sender] -= prizeCost;
        Redemption_Status = "Redemption successful!"; 
```
The Redeem() function is used by the user to redeem prize. The second line of the code checks whether the user has enough tokens to redeem the prize. If not, the function will show error. And the next line subtracts the prize cost from the user's balance. The next line functions to show that the status of redemption meaning that if the redemption is successful it will show "Redemption successful!" 
## Authors
The author of this file is toshik sharma
email id : toshiksharma45@gmail.com
