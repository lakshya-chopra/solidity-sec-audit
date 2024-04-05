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
