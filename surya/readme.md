## Surya install

Pre-requisites:
```
NodeJS
NPM
```
Install Surya using npm:
```
npm install -g surya
```
Navigate to the directory where your solidity contracts are written & execute the following commands:

  - Parse your smart contract (create a tree like structure)
    ```
    surya parse mycontract.sol
    ```
    ![image](https://github.com/lakshya-chopra/solidity-sec-audit/assets/77010972/a531c013-3302-4eef-a2a1-4332e78d978c)

  - Flatten:
    ```
    surya flatten mycontract.sol
    ```
  - Describe (give a concise summary)
    ```
    surya describe mycontract.sol
    ```
    ![image](https://github.com/lakshya-chopra/solidity-sec-audit/assets/77010972/e05d45e1-187d-482c-8c7f-3f34e5e79e89)

