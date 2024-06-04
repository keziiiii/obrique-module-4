# Project Title

Building on Avalanche.

## Description

Building on Avalanche involves leveraging its high-throughput, low-latency, and customizable blockchain platform to develop decentralized applications (dApps), smart contracts, and tokens. .


## Getting Started

You need an invitation to metacrafters to do this project.
### Executing program

* To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., HelloWorld.sol). Copy and paste the following code into the file:



```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract DegenToken is ERC20 {
    address public admin;
    
    constructor() ERC20("DegenToken", "DEGEN") {
        _mint(msg.sender, 1000000 * 10 ** uint(decimals())); // Initial supply: 1,000,000 DEGEN
        admin = msg.sender;
    }

    modifier onlyAdmin() {
        require(msg.sender == admin, "Only admin can call this function");
        _;
    }

    function mint(address to, uint256 amount) external onlyAdmin {
        _mint(to, amount);
    }

    function burn(uint256 amount) external {
        _burn(msg.sender, amount);
    }

    function deliverItems(address player, uint256 itemId, uint256 quantity) external onlyAdmin {
        // Here you would implement the logic to deliver items to the player
        // For simplicity, let's assume this just emits an event
        emit ItemsDelivered(player, itemId, quantity);
    }

    function transfer(address to, uint256 amount) public override returns (bool) {
        require(to != address(0), "ERC20: transfer to the zero address");
        require(amount <= balanceOf(msg.sender), "ERC20: transfer amount exceeds balance");
        
        _transfer(msg.sender, to, amount);
        return true;
    }

    event ItemsDelivered(address indexed player, uint256 indexed itemId, uint256 quantity);
}


```
To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.4" (or another compatible version), and then click on the "Compile HelloWorld.sol" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "HelloWorld" contract from the dropdown menu, and then click on the "Deploy" button.

Once the contract is deployed, you can interact with it by calling the sayHello function. Click on the "HelloWorld" contract in the left-hand sidebar, and then click on the "sayHello" function. Finally, click on the "transact" button to execute the function and retrieve the "Hello World!" message.
## Help
You must have a laptop and strong internet.
```
command to run if program contains helper info
```

## Authors

Contact info

Quezie Obrique 
8210606@ntc.edu.ph
## License

This project is licensed under the [MIT license] License - see the LICENSE.md file for details
