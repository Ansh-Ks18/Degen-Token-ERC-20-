# 🛠️ Building on Avalanche: Degen Token (ERC-20) 🛠️

## Project: Degen Token (ERC-20): Unlocking the Future of Gaming 🎮

### Description

Are you up for a challenge that will put your skills to the test? Degen Gaming 🎮, a renowned game studio, has approached you to create a unique token that can reward players and take their game to the next level. You have been tasked with creating a token that can be earned by players in their game and then exchanged for rewards in their in-game store. A smart step towards increasing player loyalty and retention 🧠

To support their ambitious plans, Degen Gaming has selected the Avalanche blockchain, a leading blockchain platform for web3 gaming projects, to create a fast and low-fee token. With these tokens, players can not only purchase items in the store, but also trade them with other players, providing endless possibilities for growth 📈

Are you ready to join forces with Degen Gaming and help turn their vision into a reality? The gaming world is counting on you to take it to the next level. Will you rise to the challenge 💪, or will it be game over ☠️ for you?

---

## Challenge

Your task is to create an ERC20 token and deploy it on the Avalanche network for Degen Gaming. The smart contract should have the following functionality:

1. **Minting new tokens**: The platform should be able to create new tokens and distribute them to players as rewards. Only the owner can mint tokens.
2. **Transferring tokens**: Players should be able to transfer their tokens to others.
3. **Redeeming tokens**: Players should be able to redeem their tokens for items in the in-game store.
4. **Checking token balance**: Players should be able to check their token balance at any time.
5. **Burning tokens**: Anyone should be able to burn tokens that they own and no longer need.

When writing the ERC-20 smart contract, make sure to follow the ERC-20 standard as closely as possible. This will ensure that the smart contract is interoperable with other ERC-20 tokens and can be used with a variety of wallets and exchanges. Additionally, consider adding any additional functionality or security measures that may be necessary to ensure that the token is secure and can be used effectively for the store's reward program.

Once you have written and deployed the smart contract, test it thoroughly to ensure that it is working as expected.

---

## Tools Used 🛠️

- Computer 💻
- NodeJS 🌐
- Hardhat 🔨
- Solidity ⛓️

---

## Step-by-Step Guide 📝

### Step 1: Write the Solidity Code in Remix

1. **Open Remix**:
   - Go to [Remix IDE](https://remix.ethereum.org) 🌐.

2. **Create a New File**:
   - Click on the "+" icon next to the "contracts" folder in the file explorer.
   - Name the file `DegenToken.sol`.

3. **Paste the Solidity Code**:

```solidity

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract DegenToken is ERC20, Ownable {
    struct Item {
        string name;        
        uint256 cost;       
    }

    mapping(string => Item) public items;   

    mapping(address => uint256) public itemsRedeemed;

    constructor() ERC20("DegenToken", "DGN") Ownable(msg.sender) {
        _mint(msg.sender, 10 * (10 ** uint256(decimals()))); // Initial supply for the owner
    }

    // Add an item to the store with a specific name and cost in tokens
    function addItem(string memory itemName, uint256 itemCost) external onlyOwner {
        items[itemName] = Item(itemName, itemCost);
    }

    // Redeem an item by specifying its name and quantity
    function redeemItem(string memory itemName, uint256 quantity) public {
        Item storage item = items[itemName];
        require(item.cost > 0, "Item does not exist or cost is not set");
        
        uint256 totalCost = item.cost * quantity;
        require(balanceOf(msg.sender) >= totalCost, "Insufficient tokens for redemption");

        itemsRedeemed[msg.sender] += quantity;
        _burn(msg.sender, totalCost);
    }

    // Check the number of items redeemed by a user
    function checkItemsRedeemed(address user) public view returns (uint256) {
        return itemsRedeemed[user];
    }

    // Owner can create (mint) more tokens
    function createTokens(address recipient, uint256 amount) public onlyOwner {
        _mint(recipient, amount);
    }

    // Check the token balance of an account
    function checkTokenBalance(address account) public view returns (uint256) {
        return balanceOf(account);
    }

    // Burn tokens (destroy them) from the caller's balance
    function burnTokens(uint256 amount) public {
        require(balanceOf(msg.sender) >= amount, "Insufficient tokens for burning");
        _burn(msg.sender, amount);
    }

    // Transfer tokens to another account
    function sendTokens(address recipient, uint256 amount) public {
        require(recipient != address(0), "Invalid recipient address");
        require(balanceOf(msg.sender) >= amount, "Insufficient tokens for transfer");
        _transfer(msg.sender, recipient, amount);
    }
}


```

### Step 2: Compile the Contract

1. **Select Compiler Version**:
   - On the left sidebar, click on the "Solidity Compiler" tab (icon of a "G" and "h").
   - Ensure the compiler version is set to `0.8.18`. If not, select it from the dropdown.

2. **Compile the Contract**:
   - Click the "Compile DegenToken.sol" button.

### Step 3: Deploy the Contract

1. **Select Deployment Environment**:
   - On the left sidebar, click on the "Deploy & Run Transactions" tab (icon of a computer and Ethereum logo).
   - Choose "Injected Web3" from the "Environment" dropdown. Ensure your MetaMask is connected to the Avalanche network (either Fuji Testnet or Avalanche Mainnet).

2. **Deploy the Contract**:
   - Make sure your contract `DegenToken` is selected in the "Contract" dropdown.
   - Click the "Deploy" button.
   - Confirm the transaction in MetaMask.

3. **Get the Contract Address**:
   - After the deployment, you will see the deployed contract instance at the bottom of the Remix window.
   - Copy the contract address by clicking the copy icon next to the deployed contract address.

### Step 4: Verify the Contract on Snowtrace

1. **Go to Snowtrace**:
   - For the Fuji Testnet, visit [Snowtrace Fuji](https://testnet.snowtrace.io/).
   - For the Avalanche Mainnet, visit [Snowtrace Mainnet](https://snowtrace.io/).

2. **Find Contract Verification**:
   - On Snowtrace, click on "Verify and Publish" under the "More" tab in the top menu.

3. **Enter Contract Details**:
   - Paste the contract address copied from Remix.
   - Select the compiler version `0.8.18`.
   - Select "No" for optimization if you didn't enable it in Remix, otherwise select "Yes".

4. **Paste Solidity Code**:
   - In the code verification section, paste the entire Solidity code of `DegenToken.sol`.

5. **Verify the Contract**:
   - Complete the verification process and wait for Snowtrace to confirm.

---

## Summary 📋

By following these steps and ensuring each requirement is met, you will be able to successfully complete the Degen Token project for Degen Gaming. This method ensures a straightforward deployment and verification process.

---

## Submission Requirements ✅

There are four requirements for submitting your project:
1. **Code Check**: Ensure the contract meets all functional requirements. ✅
2. **Testing**: All unit tests should pass.
3. **Deployment**: The contract should be deployed and tested on the Avalanche Fuji Testnet.
4. **Verification**: The contract should be verified on Snowtrace.

Share your smart contract with us once you have completed these steps!

---

Good luck, and may your coding journey be successful! 🚀

---

## Authors
ANSHU KUMAR

Feel free to enhance this README with any additional details or specific instructions related to your project's nuances.
