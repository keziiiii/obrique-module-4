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

contract DegenGuns is ERC20 {
    struct Gun {
        uint256 price;
        bool exists;
    }

    mapping(uint256 => Gun) public guns;
    mapping(address => mapping(uint256 => bool)) public ownedGuns;

    address public contractOwner;

    event GunRedeemed(address indexed player, uint256 indexed gunId, uint256 quantity);
    
    constructor() ERC20("DEGEN", "DGN") {
        contractOwner = msg.sender;
        addGun(1, 320); // Gun 1: Pistol - Price = 320 DegenTokens
        addGun(2, 480); // Gun 2: Shotgun - Price = 480 DegenTokens
        addGun(3, 10500); // Gun 3: Sniper Rifle - Price = 1050 DegenTokens
        addGun(4, 890); // Gun 4: Assault Rifle - Price = 890 DegenTokens
        addGun(5, 1120); // Gun 5: Submachine Gun - Price = 1120 DegenTokens
        addGun(6, 1500); // Gun 6: Rocket Launcher - Price = 1550 DegenTokens
    }

    modifier onlyContractOwner() {
        require(msg.sender == contractOwner, "Ownable: caller is not the contract owner");
        _;
    }

    function addGun(uint256 gunId, uint256 price) internal {
        require(!guns[gunId].exists, "Gun already exists");
        guns[gunId] = Gun(price, true);
    }

    function mintTokens(address account, uint256 amount) external onlyContractOwner {
        _mint(account, amount);
    }

    function burnTokens(uint256 amount) external {
        _burn(msg.sender, amount);
    }

    function redeemGun(uint256 gunId, uint256 quantity) external {
        require(guns[gunId].exists, "Invalid gun ID");
        require(balanceOf(msg.sender) >= guns[gunId].price * quantity, "Insufficient token balance");

        _burn(msg.sender, guns[gunId].price * quantity);
        ownedGuns[msg.sender][gunId] = true;
        emit GunRedeemed(msg.sender, gunId, quantity);
    }

    function redeemTokens(uint256 amount) external {
        require(balanceOf(msg.sender) >= amount, "Insufficient token balance");

        _burn(msg.sender, amount);
        emit GunRedeemed(msg.sender, 0, amount); // GunId 0 represents redeeming tokens
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
