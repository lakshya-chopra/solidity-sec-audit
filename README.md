# solidity-sec-audit

## Prerequisites
  - Install [Docker](https://github.com/lakshya-chopra/docker-gettingstarted)
  - Pull [devopstestlab/solgraph](https://www.npmjs.com/package/solgraph) : `docker pull devopstestlab/solgraph`.
    
## Create the smart contract in solidity:
```
$ sudo mkdir data
$ cd data
$ sudo vi MyContracts.sol

```
Run this smart contract in the docker image we just pulled:
```docker run -it --rm -v $PWD:/data devopstestlab/solgraph```

View the image using: `xdg-open MyContracts.sol.png`

![image](https://github.com/lakshya-chopra/solidity-sec-audit/assets/77010972/c4ebb1f6-1145-4f5f-b404-19aca695f56e)


## Solidity smart contracts security audit images:
```
Mythril
Slither (https://github.com/crytic/slither)
Securify

```

## Using slither:
```
$ docker pull trailofbits/eth-security-toolbox
```
Create a new mycontract.sol (Voting Blockchain):
```
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.4;
contract SimpleAuction {

    address payable public beneficiary;
    uint public auctionEndTime;

    // Current state of the auction.
    address public highestBidder;
    uint public highestBid;

    // Allowed withdrawals of previous bids
    mapping(address => uint) pendingReturns;


    /// The auction has already ended.
    error AuctionAlreadyEnded();
    /// There is already a higher or equal bid.
    error BidNotHighEnough(uint highestBid);
    /// The auction has not ended yet.
    error AuctionNotYetEnded();
    /// The function auctionEnd has already been called.
    error AuctionEndAlreadyCalled();


    constructor(
        uint biddingTime,
        address payable beneficiaryAddress
    ) {
        beneficiary = beneficiaryAddress;
        auctionEndTime = block.timestamp + biddingTime;
    }

    function bid() external payable {

        if (block.timestamp > auctionEndTime)
            revert AuctionAlreadyEnded();

        // If the bid is not higher, send the
        // Ether back (the revert statement
        // will revert all changes in this
        // function execution including
        // it having received the Ether).
        if (msg.value <= highestBid)
            revert BidNotHighEnough(highestBid);

        if (highestBid != 0) {

            pendingReturns[highestBidder] += highestBid;
        }
        highestBidder = msg.sender;
        highestBid = msg.value;
        emit HighestBidIncreased(msg.sender, msg.value);
    }

    /// Withdraw a bid that was overbid.
    function withdraw() external returns (bool) {
        uint amount = pendingReturns[msg.sender];
        if (amount > 0) {

            pendingReturns[msg.sender] = 0;


            if (!payable(msg.sender).send(amount)) {
                // No need to call throw here, just reset the amount owing
                pendingReturns[msg.sender] = amount;
                return false;
            }
        }
        return true;
    }

    /// End the auction and send the highest bid
    /// to the beneficiary.
    function auctionEnd() external {


        // 1. Conditions
        if (block.timestamp < auctionEndTime)
            revert AuctionNotYetEnded();
        if (ended)
            revert AuctionEndAlreadyCalled();

        // 2. Effects
        ended = true;
        emit AuctionEnded(highestBidder, highestBid);

        // 3. Interaction
        beneficiary.transfer(highestBid);
    }
}

```

Mount the contracts data directory to the container and run it:
```
$ docker run -v $(pwd)/contracts:/contracts/ trailofbits/eth-security-toolbox bash -c "solc /contracts/mycontract.sol"
```
![image](https://github.com/lakshya-chopra/solidity-sec-audit/assets/77010972/46fad5ea-48fd-4ac8-82a2-08aeb5ac15db)


Note that one could've directly opened an interactive terminal using `docker run -it -v $(pwd)/contracts:/contracts/ trailofbits/eth-security-toolbox bash`

Compile and generate the artifact using the `-o` flag.
![image](https://github.com/lakshya-chopra/solidity-sec-audit/assets/77010972/ea648c99-8178-455a-a40a-37ac6193384e)

Run this command to view the audit report:
```
slither /contracts/mycontract.sol
```
![image](https://github.com/lakshya-chopra/solidity-sec-audit/assets/77010972/f8b7bca5-5771-41eb-8534-a36928b518f2)

```
slither-check-erc /contracts/mycontract.sol Ballot
```
