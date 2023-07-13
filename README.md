# Eth-intermediate-module-4
**Aim of the Project**
Create an ERC20 token and deploy it on the Avalanche network for Degen Gaming. It consists of minting, burning, transferring, redeeming tokens, and checking the account balance.

**Code of the program**

      // SPDX-License-Identifier: MIT
      pragma solidity ^0.8.18;

      import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
      import "@openzeppelin/contracts/access/Ownable.sol";
      import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Burnable.sol";
      import "hardhat/console.sol";

      contract DegenToken is ERC20, Ownable, ERC20Burnable {

     constructor() ERC20("Degen Token", "DGN ") {}

        function mint_Tokens(address to, uint256 amount) public onlyOwner{
            _mint(to, amount);//mint the tokens
        }
        function transfer_Tokens(address _reciever, uint amount) external{
            require(balanceOf(msg.sender) >= amount, "You are not a valid user");
            approve(msg.sender, amount);
            transferFrom(msg.sender, _reciever, amount);//transfer the tokens
        }
        function getBalance() external view returns(uint){
           return balanceOf(msg.sender);// know thw balance of the account
        }
        function burn_Tokens(uint amount) external{
            require(balanceOf(msg.sender)>= amount, "There are not enough of the Degen Tokens");
            _burn(msg.sender, amount);// burn the tokens
        }
        function redeem_Rewards() public pure returns(string memory) {//redeem the rewards from the earned tokens
            return "1. Diamond Royale Voucher = 500 \n 2. Legendary Skin = 250 /n 3.Resource Portion  = 100 /n 4.Fight Loot Box = 75 /n 5. Classic Crate Coupon=50";
        }
        function reedemTokens(uint choice) external payable{
            require(choice<=5,"");
            if(choice==1){
                require(balanceOf(msg.sender)>=500, "You don't have sufficient amount of tokens to redeem this reward");
                approve(msg.sender, 500);
                transferFrom(msg.sender, owner(), 500);
            }
            else if(choice ==2){
                require(balanceOf(msg.sender)>=250, "You don't have sufficient amount of tokens to redeem this reward");
                approve(msg.sender, 250);
                transferFrom(msg.sender, owner(), 250);
            }
             else if(choice ==3){
                require(balanceOf(msg.sender)>=100, "You don't have sufficient amount of tokens to redeem this reward");
                approve(msg.sender, 100);
                transferFrom(msg.sender, owner(), 100);
            }
             else if(choice ==4){
                require(balanceOf(msg.sender)>=75, "You don't have sufficient amount of tokens to redeem this reward");
                approve(msg.sender, 75);
                transferFrom(msg.sender, owner(), 75);
            }
            else{
                require(balanceOf(msg.sender)>=50, "You don't have sufficient amount of tokens to redeem this reward");
                approve(msg.sender, 50);
                transferFrom(msg.sender, owner(), 50);
            }


         }

         }


**Logic of the code**

1. Write the license identifier and solidity version.

2. Import the open Zeppelin contracts and hardhat/console.sol dependencies.

3. Create a contract named as DegenToken which is Ownable and ERC20Burnable.

4. It consists of a constructor which defines the name and symbol of the token as "Degen Token" and "DGN " respectively.

5. The function mint_tokens consists of minting a specific amount to a particular address. It is declared public so that it can be accessed outside the contract.

6. The transfer_Token function takes the receiver's address and amount to be transferred as its parameters. It has a require statement that confirms that the balance of the sender should be greater than or equal to the amount to be transferred else the string message is returned. If the condition returns to true, then the approve  and transferFrom  function transfers the tokens(amount) from the sender to the receiver.

7. The getBalance function is declared external and returns the unsigned int value of the valance in the sender's account/address.

8. The burn_Tokens take the unsigned int value of the amount as its parameter. It is declared as external. The require statement checks that the balance of the sender should be greater than or equal to the amount to be transferred else the string message is returned. If the condition returns to the true, then the burn function burns the specific amount of tokens from the sender's account.

9. The redeem_Tokens is declared public and pure. It returns the five rewards(strings) which will be redeemed if the conditions are satisfied.

10. The user enters a particular number. The require statement checks that the entered number should be less than the total number of the choices provided, if yes then the condition matching with the choice is executed and that particular numbered reward is redeemed by paying the listed tokens.

**Functionality of the code**

1. Open the Remix IDE(https://remix.ethereum.org) and clone the repository provided in the module.

2. Open the contacts folder and write the above code.

3. Compile the DegenToken.sol contract.

4. In the deploy section, select Injected Provider environment which will help us to connect with the metamask.

5. Paste the address of the account currently running in the meta mask in the At Address section.

6. Open the deployed contract. Run different functions of minting, burning, transferring, redeeming tokens, and checking the account balance.

7. Verify the transactions by pasting the same address in the Snowtrace Testnet site.(https://testnet.snowtrace.io)

8. If all the tests are passed, then the contract has successfully followed every requirement of the project.


**Authors**

Sehajpreet Kaur
(21BCS4518@cuchd.in)
