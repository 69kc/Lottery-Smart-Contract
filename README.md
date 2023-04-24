# Lottery-Smart-Contract
A lottery smart contract is a smart contract that can be used to create a decentralized lottery. This is an excellent way to learn how to create a smart contract that interacts with random numbers. The following code shows how to create a basic lottery smart contract:



pragma solidity ^0.8.0;

contract Lottery {
    address payable[] public players;

    function play() public payable {
        require(msg.value == 1 ether);
        players.push(payable(msg.sender));
    }

    function generateRandomNumber() private view returns (uint256) {
        return uint256(keccak256(abi.encodePacked(block.timestamp, block.difficulty))) % players.length;
    }

    function distributePrize() public {
        require(players.length > 0);
        uint256 winnerIndex = generateRandomNumber();
        players[winnerIndex].transfer(address(this).balance);
        players = new address payable[](0);
    }
}
