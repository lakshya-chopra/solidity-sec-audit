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


## Solidity smart contracts security audit images:
```
Mythril
Slither
Securify

```
