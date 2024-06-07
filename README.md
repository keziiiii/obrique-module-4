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
pragma solidity ^0.8.9;

contract DegenToken {
    string public name = "Degen Token";
    string public symbol = "DEGEN";
    uint256 public totalSupply;
    uint8 public decimals = 18;
    address public owner;

    struct Item {string name; uint256 cost;}
    Item[] private items;
    mapping(address => uint256) balances;
    mapping(address => mapping(address => uint256)) allow;

    event T(address indexed sender, address indexed receiver, uint256 amount);
    event A(address indexed owner, address indexed spender, uint256 amount);
    event R(address indexed player, string itemName, uint256 amount);

    modifier hasT(uint256 _amount) {
    require(balanceOf(msg.sender) >= _amount, "Insufficient DEGEN");
    _;
}
    modifier onlyOwner() {require(msg.sender == owner, "Only owner is authorized"); _;}

    function balanceOf(address _address) public view returns (uint256) {return balances[_address];}

    function addItem(string memory _name, uint256 _cost) private {items.push(Item(_name, _cost));}

    function redeem(uint8 _itemId) external {
        require(_itemId < items.length, "Invalid ID");
        Item memory item = items[_itemId];
        require(balanceOf(msg.sender) >= item.cost, "Insufficient balance");
        transfer(address(this), item.cost);
        emit R(msg.sender, item.name, item.cost);
    }

    function transfer(address _receiver, uint256 _amount) public {
        require(_receiver != address(0) && msg.sender != address(0), "Invalid address");
        require(_amount <= balances[msg.sender], "Insufficient balance");
        balances[msg.sender] -= _amount;
        balances[_receiver] += _amount;
        emit T(msg.sender, _receiver, _amount);
    }

    function approve(address _delegate, uint256 _amount) external {
        require(msg.sender != address(0) && balances[msg.sender] > _amount, "Insufficient balance");
        allow[msg.sender][_delegate] = _amount;
        emit A(msg.sender, _delegate, _amount);
    }

    function allowance(address _owner, address _delegate) external view returns (uint) {return allow[_owner][_delegate];}

    function transferFrom(address _owner, address _buyer, uint256 _amount) external {
        require(_owner != address(0) && _buyer != address(0), "Invalid address");
        require(_amount <= balances[_owner] && _amount <= allow[_owner][msg.sender], "Insufficient allowance");
        balances[_owner] -= _amount;
        allow[_owner][msg.sender] -= _amount;
        balances[_buyer] += _amount;
        emit T(_owner, _buyer, _amount);
    }

    function burn(uint256 _amount) public hasT(_amount) {
        balances[msg.sender] -= _amount;
        totalSupply -= _amount;
        emit T(msg.sender, address(0), _amount);
    }

    function mint(address _to, uint256 _amount) public onlyOwner {
        uint256 actualSupply = _amount * (10 ** decimals);
        balances[_to] += actualSupply;
        totalSupply += actualSupply;
        emit T(address(0), _to, actualSupply);
    }

    function transferOwnership(address _newOwner) external onlyOwner {owner = _newOwner;}

    constructor() {
        owner = msg.sender;
        mint(msg.sender, 1000000 * (10 ** decimals));
        addItem("Health", 70);
        addItem("Skins", 55);
        addItem(Emblem"s", 30);
        addItem("Weapon", 80);
        addItem("Diamond", 100);
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
