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
Mount the contracts data directory to the container and run it:
```
$ docker run -v $(pwd)/contracts:/contracts/ trailofbits/eth-security-toolbox bash -c "solc /contracts/mycontract.sol" 
```
Note that one could've directly opened an interactive terminal using `docker run -it -v $(pwd)/contracts:/contracts/ trailofbits/eth-security-toolbox bash`

Compile and generate the artifact using the `-o` flag.
![image](https://github.com/lakshya-chopra/solidity-sec-audit/assets/77010972/ea648c99-8178-455a-a40a-37ac6193384e)

Run this command to view the audit report:
```
slither /contracts/mycontract.sol
```
![image](https://github.com/lakshya-chopra/solidity-sec-audit/assets/77010972/f8b7bca5-5771-41eb-8534-a36928b518f2)

