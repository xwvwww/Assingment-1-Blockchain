
# EtherVault Smart Contract
**Done by SE-2315: Almen Alnur, Zhangir Yussupov, Yeskendir Khassangaliyev.**

## Overview

The EtherVault is a simple Solidity smart contract that allows you to receive, store, and withdraw Ether. The contract’s owner can withdraw the Ether, and anyone can check the current balance of the contract. It is deployed and tested using Remix IDE, an online Solidity development environment.


## Features

 - **Receive Ether**: The contract is able to receive Ether via the receive() function.
 - **Withdraw Ether**: Only the owner (the account that deployed the contract) can withdraw Ether from the contract.
 - **Check Balance**: A public function allows anyone to check the contract's balance.


## Smart Contract Code


```bash
  // SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract EtherVault {
    address public owner;

    constructor() payable  {
        owner = msg.sender;  // The account that deploys the contract becomes the owner
    }

    // Function to receive Ether
    receive() external payable {}

    // Function to withdraw a specified amount of Ether
    function withdraw(uint256 _amount) public {
        require(msg.sender == owner, "Only the owner can withdraw funds");
        require(address(this).balance >= _amount, "Insufficient balance");

        payable(owner).transfer(_amount);
    }

    // Function to check the contract's balance
    function getBalance() public view returns (uint256) {
        return address(this).balance;
    }
}

```


## Steps to Run the Contract in Remix IDE

**Step 1: Open Remix IDE**
- Open your browser and go to Remix IDE.
- You’ll be working in the Solidity environment, so ensure the Solidity compiler plugin is enabled in the left sidebar.

**Step 2: Create a New File and Add the Contract Code**
- In Remix, create a new file named EtherVault.sol under the contracts folder.
- Paste the smart contract code from above into the newly created file.

**Step 3: Compile the Contract**
- Click on the Solidity Compiler plugin (on the left sidebar).
- Select the correct compiler version (**0.8.0** or higher).
- Click Compile EtherVault.sol.

**Step 4: Deploy the Contract**
- Go to the Deploy & Run Transactions plugin in the left sidebar.
- Select the Environment (you can use JavaScript VM, Injected Web3 for MetaMask, or Web3 Provider for a public testnet like Rinkeby).
- For local testing, use JavaScript VM which does not require any configuration.
- For public testnets like Rinkeby or Goerli, use Injected Web3 to connect your MetaMask wallet.
- Ensure the correct Contract (EtherVault) is selected.
- Set the Gas limit and Value if needed (leave as default for this example).
- Click Deploy.

**Step 5: Interact with the Contract**
- After deployment, you'll see the contract under Deployed Contracts in the Deploy & Run Transactions section.
- Receive Ether: Use the receive() function to send Ether to the contract. You can interact with this by sending Ether directly through Remix or using the send button.
- Check Balance: To check the balance of the contract, call the getBalance() function.
- Withdraw Ether: To withdraw Ether, call the withdraw() function. Ensure that you are using the owner’s account (the one that deployed the contract) to perform the withdrawal. You can only withdraw from the contract if you are the owner.

**Step 6: Testing the Contract**
- Send some Ether to the contract by using the receive function.
- Check the contract's balance by calling the getBalance() function.
- As the owner, try withdrawing Ether using the withdraw() function.

**Step 7: Configure MetaMask**
- Install MetaMask: If you haven’t already, install the MetaMask browser extension.
- Connect MetaMask to a Public Testnet:
- Choose a testnet (e.g., Rinkeby or Goerli) and configure MetaMask to connect to it.
- Obtain some test Ether from a faucet for the selected testnet.
- Deploy to Public Testnet: After connecting Remix to MetaMask, use Injected Web3 to deploy the contract to a public testnet.


## Installation

Install my-project with npm
- Install Web3.js
```bash
  npm install web3
```
- Configure Web3.js: Set up Web3.js to connect to either a local Ethereum node (such as Ganache) or a public testnet like Rinkeby using the appropriate RPC URL.

For this assignment, Web3.js integration is not necessary as Remix provides a complete environment to interact with your contract directly.

## Example Interaction with Web3.js (Optional)
If you want to interact with the contract from a frontend or external environment, you can use the Web3.js library to connect and interact with the deployed contract.

```
const Web3 = require('web3');
const web3 = new Web3(window.ethereum);

const contractAddress = 'YOUR_CONTRACT_ADDRESS';
const contractABI = [ /* Contract ABI goes here */ ];

const contract = new web3.eth.Contract(contractABI, contractAddress);

async function getBalance() {
    const balance = await contract.methods.getBalance().call();
    console.log('Contract Balance:', balance);
}

async function withdrawEther(amount) {
    const accounts = await web3.eth.getAccounts();
    const ownerAddress = accounts[0];

    await contract.methods.withdraw(amount).send({ from: ownerAddress });
}
```
    


## Conclusion
The EtherVault smart contract demonstrates how to handle Ether transactions on the Ethereum blockchain. By following the above steps, you can deploy and interact with the contract in Remix IDE. The contract’s functionalities include receiving Ether, allowing the owner to withdraw Ether, and checking the contract balance.


## License

**This project is licensed under the MIT License.**

