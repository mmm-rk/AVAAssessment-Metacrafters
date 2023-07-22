# Project: Smart Contract Project

This solidity program is a simple demonstration of how the different error handling functions such as require(), assert(), and revert() work on a smart contract.

## Description

This program is a simple contract written in Solidity programming language. The smart contract has two modified functions from the previous project in Solidity Beginner Course such as mint and burn functions. The main purpose of this program is to show how error handling functions work.

## Getting Started

### Executing program
To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., Module1Project.sol). Copy and paste the following code into the file:
```javascript
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0; //solidity version

/*
Smart Contract Project - For this project, write a smart contract that implements the require(), assert() and revert() statements.
*/

contract errorHandling {
    string private tokenName = "DEIMAN";
    string private tokenAbbrv = "DMN";
    uint public totalSupply = 0;
    mapping(address => uint) public balances;

    function mintToken(address _address, uint _value) public {
        //checks if its a valid address
        require(_address != address(0), "Invalid address");
        //checks if the value is >= 100, so there's a minimum of 100 token
        require(_value >= 100, "Value must be greater than or equal to 100");

        totalSupply += _value;
        balances[_address] += _value;
        
        //assert to check if the balance is updated correctly
        assert(balances[_address] >= _value);
    }

    function burnToken(address _address, uint _value) public {
        //checks if the balance of the sender is less than 500, therefore burning token is not yet available.
	    if(balances[_address] < 500) {
            revert("Token burning in this account is not yet available.");
    	}
        
        //checks if its a valid address
        require(_address != address(0), "Invalid address");
        //checks if the value is >= 30, so there's a minimum of 30 token
        require(_value >= 30, "Value must be greater than or equal to 30");
        //checks if the balance of the sender has more than or enough amount
        require(balances[_address] >= _value, "Insufficient Balance");

        totalSupply -= _value; 
        balances[_address] -= _value;

        //assert to check if the balance is updated correctly
        assert(balances[_address] <= totalSupply); 
    }
}
```

To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.0" (or another compatible version), and then click on the "Compile Module1Project.sol" button.

## Authors

Mark Joseph Pardiñas

## License

This project is licensed under the MIT License - see the LICENSE.md file for details
