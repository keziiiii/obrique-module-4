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
import "@openzeppelin/contracts/access/Ownable.sol";

contract DegenGamingToken is ERC20, Ownable {
    struct Item {
        string name;
        uint256 price;
    }

    mapping(string => Item) public items;

    constructor() ERC20("KeziToken", "KZ") Ownable(msg.sender) {}

    function mint(address account, uint256 amount) public onlyOwner {
        _mint(account, amount);
    }

    function transfer(address recipient, uint256 amount) public virtual override returns (bool) {
        _transfer(_msgSender(), recipient, amount);
        return true;
    }

    function redeemItem(string memory itemName) public {
        require(items[itemName].price > 0, "Item not found");
        require(balanceOf(msg.sender) >= items[itemName].price, "Insufficient balance");
        
        // Deduct the price of the item from the user's balance
        _burn(msg.sender, items[itemName].price);
        
        emit ItemRedeemed(msg.sender, itemName);
    }
      
    function addItem(string memory itemName, uint256 price) public onlyOwner {
        require(price > 0, "Price must be greater than zero");
        items[itemName] = Item(itemName, price);
    }

    event ItemRedeemed(address indexed user, string itemName);

     function burn(uint256 amount) public virtual {
        _burn(_msgSender(), amount);
    }

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
