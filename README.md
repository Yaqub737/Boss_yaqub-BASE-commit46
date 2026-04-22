# Boss_yaqub-BASE-commit46

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;
import {AggregatorV3Interface} from "@chainlink/contracts/src/v0.8/shared/interfaces/AggregatorV3Interface.sol";
contract SimpleStorage {


        //LIST OF STATE VARIABLES:
uint256 FavoriteNumber;
struct Person {
    uint256 FavoriteNumber;
    string Name;
}
Person[] public ListOfpeopleandTheirFavoriteNumber;
address[] public FundersAddress;
mapping(string name => uint256 _favoriteNumber) public NametofavoriteNumber;
mapping(address FunderAddress => uint256 ValuedStored) public ToGetAmount;
address private immutable owner;
constructor() {
    owner = msg.sender;
}

        // LIST OF FUNCTIONS;
        modifier OnlyOwner() {
            owner == msg.sender;
            _;
        }

function Store (uint256 myfavoriteNumber) public {
     FavoriteNumber = myfavoriteNumber;
}        
function Retrieve() public view returns (uint256) {
    return FavoriteNumber;
}

function Addperson (string memory _name, uint256 _myFavoriteNumber) public {
    ListOfpeopleandTheirFavoriteNumber.push(Person(_myFavoriteNumber, _name));
    NametofavoriteNumber[_name] = FavoriteNumber;
}
function FundME() public payable OnlyOwner  {
   ToGetAmount[msg.sender]  += msg.value;
   FundersAddress.push(msg.sender);
   }

function Withdraw() public payable OnlyOwner returns (bool success) {
    for(uint i = 0; i < FundersAddress.length; i++){
        ToGetAmount[FundersAddress[i]];
    }
    (success,) =payable (msg.sender).call{value: address (this).balance}('');
}
}
