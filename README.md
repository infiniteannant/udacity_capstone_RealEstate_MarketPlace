# Udacity Blockchain Capstone

The capstone will build upon the knowledge you have gained in the course in order to build a decentralized housing product. 

## Getting Started

### Prequisites
For development make sure ganache-cli is installed globally,metamask extension is enabled and solidity compiler is configured in truffle config.

### Install Dependencies
* Install all requisite npm packages
```
npm install
```


### ZoKrates Setup

 The following instructions explain how to generate addtional proofs for tokenIds.

* Step 1: Run Docker

* Step 2: Run ZoKrates
  ```
  docker run -v `pwd`/zokrates/code/:/home/zokrates/code -ti zokrates/zokrates /bin/bash
  ```

  Change into the square directory
  ``` 
  cd code/square/
  ``` 

* Step 3: Compile the program written in ZoKrates DSL
  ``` 
  ~/zokrates compile -i square.code
  ``` 

* Step 4: Generate the trusted setup
  ``` 
  ~/zokrates setup -s GM17
  ```

* Step 5: Compute witness
  ``` 
  ~/zokrates compute-witness -a 3 9
  ```

* Step 6: Generate proof
  ```
  ~/zokrates generate-proof -s GM17 -j <path to proof file>
  ```

* Step 7: Export verifier
  ```  
  ~/zokrates export-verifier -s GM17
  ```
Re-run steps 5 and 6 with different arguments, e.g. 2 4, to generate additional proofs for minting tokens.

### Development environment
* Run ganache:
```
ganache-cli
```
* In another terminal window:
```
cd eth-contracts
```
* Compile the contracts:
```
truffle compile
```

* This will create the smart contract artifacts in folder ```build/contracts```.

* Migrate smart contracts to the locally running blockchain, ganache-cli:

```
truffle migrate
```

* Test the smart contracts:

```
truffle test
```

### Deploy on Rinkeby
Run
```
truffle migrate --network rinkeby --reset --compile-all
```


#### Output
```
Starting migrations...
======================
> Network name:    'rinkeby'
> Network id:      4
> Block gas limit: 0x989680


1_initial_migration.js
======================

   Deploying 'Migrations'
   ----------------------
   > transaction hash:    0x3347bb5db5f2e3c75da588ffd8002148f13d340f63af59549ad77e1a030e34a8
   > Blocks: 0            Seconds: 14
   > contract address:    0x2d747FF94532e4C1e28b4266Ae45B6f7A0963177
   > block number:        6494383
   > block timestamp:     1589571185
   > account:             0x7554744F910b0E8925f108a40201eE25B4823ab1
   > balance:             3.646895032977956869
   > gas used:            225237
   > gas price:           10 gwei
   > value sent:          0 ETH
   > total cost:          0.00225237 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.00225237 ETH


2_deploy_contracts.js
=====================

   Deploying 'RealStateToken'
   --------------------------
   > transaction hash:    0x659d8e06ed67aeb1ff965bbe2cc235a79aa3b25b06bbe39b4c5c8da8aa9548d6
   > Blocks: 1            Seconds: 21
   > contract address:    0x7eafd9B354274d7a12d4DB424ad0c10aBFB3A1ED
   > block number:        6494386
   > block timestamp:     1589571230
   > account:             0x7554744F910b0E8925f108a40201eE25B4823ab1
   > balance:             3.618382312977956869
   > gas used:            2808909
   > gas price:           10 gwei
   > value sent:          0 ETH
   > total cost:          0.02808909 ETH


   Deploying 'BN256G2'
   -------------------
   > transaction hash:    0x32730350a735a6a4c793f34e3e7bbf67eb9c54ac25a80373d4e886a5be0921d6
   > Blocks: 1            Seconds: 17
   > contract address:    0xDB3D3B166a1Cc4b29a7236f28eB411701715E0B6
   > block number:        6494388
   > block timestamp:     1589571260
   > account:             0x7554744F910b0E8925f108a40201eE25B4823ab1
   > balance:             3.608046572977956869
   > gas used:            1033574
   > gas price:           10 gwei
   > value sent:          0 ETH
   > total cost:          0.01033574 ETH


   Linking
   -------
   * Contract: Verifier <--> Library: BN256G2 (at address: 0xDB3D3B166a1Cc4b29a7236f28eB411701715E0B6)

   Deploying 'Verifier'
   --------------------
   > transaction hash:    0xfc8a578e58dc7eecf1627a6fb1bb766ece5cdff149be81e3a387045f6d710b24
   > Blocks: 0            Seconds: 5
   > contract address:    0xB16f5b0D09cBe822a5bd35B273Eb54D0B2D9813c
   > block number:        6494389
   > block timestamp:     1589571275
   > account:             0x7554744F910b0E8925f108a40201eE25B4823ab1
   > balance:             3.596029102977956869
   > gas used:            1201747
   > gas price:           10 gwei
   > value sent:          0 ETH
   > total cost:          0.01201747 ETH


   Deploying 'SolnSquareVerifier'
   ------------------------------
   > transaction hash:    0x6c7f6b7702bef3e135029e70586de5b34ff25a40b3fe4a16aefec18261d8389f
   > Blocks: 1            Seconds: 18
   > contract address:    0xfB68b5688D3B2892Cd2b01f028Aa41838cCA243C
   > block number:        6494391
   > block timestamp:     1589571305
   > account:             0x7554744F910b0E8925f108a40201eE25B4823ab1
   > balance:             3.562502092977956869
   > gas used:            3352701
   > gas price:           10 gwei
   > value sent:          0 ETH
   > total cost:          0.03352701 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.08396931 ETH


Summary
=======
> Total deployments:   5
> Final cost:          0.08622168 ETH

```

### Mint Tokens
* Inside ```eth-contracts folder```, Run
```
node addSolution.js ../zokrates/code/square/proofs/proof<number>.json <tokenId>
```
	
	
## output for token 1
```
Submitting solution:
- Input: 0x0000000000000000000000000000000000000000000000000000000000000009,0x0000000000000000000000000000000000000000000000000000000000000001
- TokenID: 1
- Address: 0x7554744F910b0E8925f108a40201eE25B4823ab1
{ blockHash: '0xbc4615c96a4731bef02f78ad76fbda45a7b6815680d3bd736b5581193f683045',
  blockNumber: 6494400,
  contractAddress: null,
  cumulativeGasUsed: 540447,
  from: '0x7554744f910b0e8925f108a40201ee25b4823ab1',
  gasUsed: 487594,
  logsBloom: '0x0000000000000000000000004000000800000000000000040000000000000000080000000000000000000200000000000000000000010000000000000c040000000000000000020000000000000000000000010000040000000000000000004000000000000001000000000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000008000000400000000000000000000000000000000000000000000000000000040000000020000000000000000000000000000000000400000000000000000000000',
  status: true,
  to: '0xfb68b5688d3b2892cd2b01f028aa41838cca243c',
  transactionHash: '0xc772fe5dde4b76f282bac544f051808b09236aae79a53b76be55b56c46f53f11',
  transactionIndex: 2,
  events: 
   { '0': 
      { address: '0xB16f5b0D09cBe822a5bd35B273Eb54D0B2D9813c',
        blockHash: '0xbc4615c96a4731bef02f78ad76fbda45a7b6815680d3bd736b5581193f683045',
        blockNumber: 6494400,
        logIndex: 0,
        removed: false,
        transactionHash: '0xc772fe5dde4b76f282bac544f051808b09236aae79a53b76be55b56c46f53f11',
        transactionIndex: 2,
        id: 'log_5cfef24f',
        returnValues: Result {},
        event: undefined,
        signature: null,
        raw: [Object] },
     solutionAdded: 
      { address: '0xfB68b5688D3B2892Cd2b01f028Aa41838cCA243C',
        blockHash: '0xbc4615c96a4731bef02f78ad76fbda45a7b6815680d3bd736b5581193f683045',
        blockNumber: 6494400,
        logIndex: 1,
        removed: false,
        transactionHash: '0xc772fe5dde4b76f282bac544f051808b09236aae79a53b76be55b56c46f53f11',
        transactionIndex: 2,
        id: 'log_b8e0e097',
        returnValues: [Object],
        event: 'solutionAdded',
        signature: '0x009c6ded84843084fe9bc0caed609ea68a61107c44ae1f1ae757f07d382edde5',
        raw: [Object] } } }


```

```
node mintToken.js <tokenId>
```

#### Output for tokenid 1
```
Before minting, the contract has 0 token
Minting new token:
- Token ID: 1
- Address 0x7554744F910b0E8925f108a40201eE25B4823ab1
{ blockHash: '0xa18c402c1340aa1f13f333a477c647c30eec5578cf638cd7654e0e83642d22f5',
  blockNumber: 6494403,
  contractAddress: null,
  cumulativeGasUsed: 633561,
  from: '0x7554744f910b0e8925f108a40201ee25b4823ab1',
  gasUsed: 242493,
  logsBloom: '0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000100000000000000040000000000000000000000000008000000000000000000040000000000000000000000000000020001000000000000000800000000000000000000000010000000000000000000000000800000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000008000000402000000000000000000000000000000000000000000000000000060000000000000000000000000000000000000000000000000000000000000000000',
  status: true,
  to: '0xfb68b5688d3b2892cd2b01f028aa41838cca243c',
  transactionHash: '0x12f4698330538be0b42f8fdbca23e7096c4aa9d1b31888f60e13a880ea446554',
  transactionIndex: 4,
  events: 
   { Transfer: 
      { address: '0xfB68b5688D3B2892Cd2b01f028Aa41838cCA243C',
        blockHash: '0xa18c402c1340aa1f13f333a477c647c30eec5578cf638cd7654e0e83642d22f5',
        blockNumber: 6494403,
        logIndex: 2,
        removed: false,
        transactionHash: '0x12f4698330538be0b42f8fdbca23e7096c4aa9d1b31888f60e13a880ea446554',
        transactionIndex: 4,
        id: 'log_ae3f23bc',
        returnValues: [Object],
        event: 'Transfer',
        signature: '0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef',
        raw: [Object] } } }
After minting, the contract has 1 token

```



### Contract Address and ABI
## View the contracts on etherscan 
  * "Verifier": "0xB16f5b0D09cBe822a5bd35B273Eb54D0B2D9813c",
	*	"SolnSquareVerifier": "0xfB68b5688D3B2892Cd2b01f028Aa41838cCA243C"
#### Contract ABI
* Verifier
```
"abi": [
    {
      "anonymous": false,
      "inputs": [
        {
          "indexed": false,
          "internalType": "string",
          "name": "s",
          "type": "string"
        }
      ],
      "name": "Verified",
      "type": "event"
    },
    {
      "constant": false,
      "inputs": [
        {
          "internalType": "uint256[2]",
          "name": "a",
          "type": "uint256[2]"
        },
        {
          "internalType": "uint256[2][2]",
          "name": "b",
          "type": "uint256[2][2]"
        },
        {
          "internalType": "uint256[2]",
          "name": "c",
          "type": "uint256[2]"
        },
        {
          "internalType": "uint256[2]",
          "name": "input",
          "type": "uint256[2]"
        }
      ],
      "name": "verifyTx",
      "outputs": [
        {
          "internalType": "bool",
          "name": "r",
          "type": "bool"
        }
      ],
      "payable": false,
      "stateMutability": "nonpayable",
      "type": "function"
    }
  ],

```
* SolnSquareVerifier
```
"abi": [
    {
      "inputs": [
        {
          "internalType": "address",
          "name": "verifierAddress",
          "type": "address"
        }
      ],
      "payable": false,
      "stateMutability": "nonpayable",
      "type": "constructor"
    },
    {
      "anonymous": false,
      "inputs": [
        {
          "indexed": true,
          "internalType": "address",
          "name": "owner",
          "type": "address"
        },
        {
          "indexed": true,
          "internalType": "address",
          "name": "approved",
          "type": "address"
        },
        {
          "indexed": true,
          "internalType": "uint256",
          "name": "tokenId",
          "type": "uint256"
        }
      ],
      "name": "Approval",
      "type": "event"
    },
    {
      "anonymous": false,
      "inputs": [
        {
          "indexed": true,
          "internalType": "address",
          "name": "owner",
          "type": "address"
        },
        {
          "indexed": true,
          "internalType": "address",
          "name": "operator",
          "type": "address"
        },
        {
          "indexed": false,
          "internalType": "bool",
          "name": "approved",
          "type": "bool"
        }
      ],
      "name": "ApprovalForAll",
      "type": "event"
    },
    {
      "anonymous": false,
      "inputs": [
        {
          "indexed": true,
          "internalType": "address",
          "name": "Operator",
          "type": "address"
        }
      ],
      "name": "Paused",
      "type": "event"
    },
    {
      "anonymous": false,
      "inputs": [
        {
          "indexed": true,
          "internalType": "address",
          "name": "from",
          "type": "address"
        },
        {
          "indexed": true,
          "internalType": "address",
          "name": "to",
          "type": "address"
        },
        {
          "indexed": true,
          "internalType": "uint256",
          "name": "tokenId",
          "type": "uint256"
        }
      ],
      "name": "Transfer",
      "type": "event"
    },
    {
      "anonymous": false,
      "inputs": [
        {
          "indexed": true,
          "internalType": "address",
          "name": "Operator",
          "type": "address"
        }
      ],
      "name": "Unpaused",
      "type": "event"
    },
    {
      "anonymous": false,
      "inputs": [
        {
          "indexed": true,
          "internalType": "address",
          "name": "previousOwner",
          "type": "address"
        },
        {
          "indexed": true,
          "internalType": "address",
          "name": "newOwner",
          "type": "address"
        }
      ],
      "name": "ownerShipTransferred",
      "type": "event"
    },
    {
      "anonymous": false,
      "inputs": [
        {
          "indexed": true,
          "internalType": "uint256",
          "name": "tokenId",
          "type": "uint256"
        },
        {
          "indexed": true,
          "internalType": "bytes32",
          "name": "key",
          "type": "bytes32"
        },
        {
          "indexed": true,
          "internalType": "address",
          "name": "to",
          "type": "address"
        }
      ],
      "name": "solutionAdded",
      "type": "event"
    },
    {
      "constant": false,
      "inputs": [
        {
          "internalType": "bool",
          "name": "pause",
          "type": "bool"
        }
      ],
      "name": "Pause",
      "outputs": [],
      "payable": false,
      "stateMutability": "nonpayable",
      "type": "function"
    },
    {
      "constant": false,
      "inputs": [
        {
          "internalType": "bool",
          "name": "pause",
          "type": "bool"
        }
      ],
      "name": "Unpause",
      "outputs": [],
      "payable": false,
      "stateMutability": "nonpayable",
      "type": "function"
    },
    {
      "constant": false,
      "inputs": [
        {
          "internalType": "bytes32",
          "name": "_myid",
          "type": "bytes32"
        },
        {
          "internalType": "string",
          "name": "_result",
          "type": "string"
        }
      ],
      "name": "__callback",
      "outputs": [],
      "payable": false,
      "stateMutability": "nonpayable",
      "type": "function"
    },
    {
      "constant": false,
      "inputs": [
        {
          "internalType": "bytes32",
          "name": "_myid",
          "type": "bytes32"
        },
        {
          "internalType": "string",
          "name": "_result",
          "type": "string"
        },
        {
          "internalType": "bytes",
          "name": "_proof",
          "type": "bytes"
        }
      ],
      "name": "__callback",
      "outputs": [],
      "payable": false,
      "stateMutability": "nonpayable",
      "type": "function"
    },
    {
      "constant": false,
      "inputs": [
        {
          "internalType": "address",
          "name": "to",
          "type": "address"
        },
        {
          "internalType": "uint256",
          "name": "tokenId",
          "type": "uint256"
        }
      ],
      "name": "approve",
      "outputs": [],
      "payable": false,
      "stateMutability": "nonpayable",
      "type": "function"
    },
    {
      "constant": true,
      "inputs": [
        {
          "internalType": "address",
          "name": "owner",
          "type": "address"
        }
      ],
      "name": "balanceOf",
      "outputs": [
        {
          "internalType": "uint256",
          "name": "",
          "type": "uint256"
        }
      ],
      "payable": false,
      "stateMutability": "view",
      "type": "function"
    },
    {
      "constant": true,
      "inputs": [
        {
          "internalType": "uint256",
          "name": "tokenId",
          "type": "uint256"
        }
      ],
      "name": "getApproved",
      "outputs": [
        {
          "internalType": "address",
          "name": "",
          "type": "address"
        }
      ],
      "payable": false,
      "stateMutability": "view",
      "type": "function"
    },
    {
      "constant": true,
      "inputs": [],
      "name": "getBaseTokenURI",
      "outputs": [
        {
          "internalType": "string",
          "name": "",
          "type": "string"
        }
      ],
      "payable": false,
      "stateMutability": "view",
      "type": "function"
    },
    {
      "constant": true,
      "inputs": [],
      "name": "getContractOwner",
      "outputs": [
        {
          "internalType": "address",
          "name": "",
          "type": "address"
        }
      ],
      "payable": false,
      "stateMutability": "view",
      "type": "function"
    },
    {
      "constant": true,
      "inputs": [],
      "name": "getTokenName",
      "outputs": [
        {
          "internalType": "string",
          "name": "",
          "type": "string"
        }
      ],
      "payable": false,
      "stateMutability": "view",
      "type": "function"
    },
    {
      "constant": true,
      "inputs": [],
      "name": "getTokenSymbol",
      "outputs": [
        {
          "internalType": "string",
          "name": "",
          "type": "string"
        }
      ],
      "payable": false,
      "stateMutability": "view",
      "type": "function"
    },
    {
      "constant": true,
      "inputs": [
        {
          "internalType": "address",
          "name": "owner",
          "type": "address"
        },
        {
          "internalType": "address",
          "name": "operator",
          "type": "address"
        }
      ],
      "name": "isApprovedForAll",
      "outputs": [
        {
          "internalType": "bool",
          "name": "",
          "type": "bool"
        }
      ],
      "payable": false,
      "stateMutability": "view",
      "type": "function"
    },
    {
      "constant": false,
      "inputs": [
        {
          "internalType": "address",
          "name": "to",
          "type": "address"
        },
        {
          "internalType": "uint256",
          "name": "tokenId",
          "type": "uint256"
        }
      ],
      "name": "mint",
      "outputs": [
        {
          "internalType": "bool",
          "name": "",
          "type": "bool"
        }
      ],
      "payable": false,
      "stateMutability": "nonpayable",
      "type": "function"
    },
    {
      "constant": true,
      "inputs": [
        {
          "internalType": "uint256",
          "name": "tokenId",
          "type": "uint256"
        }
      ],
      "name": "ownerOf",
      "outputs": [
        {
          "internalType": "address",
          "name": "",
          "type": "address"
        }
      ],
      "payable": false,
      "stateMutability": "view",
      "type": "function"
    },
    {
      "constant": false,
      "inputs": [
        {
          "internalType": "address",
          "name": "from",
          "type": "address"
        },
        {
          "internalType": "address",
          "name": "to",
          "type": "address"
        },
        {
          "internalType": "uint256",
          "name": "tokenId",
          "type": "uint256"
        }
      ],
      "name": "safeTransferFrom",
      "outputs": [],
      "payable": false,
      "stateMutability": "nonpayable",
      "type": "function"
    },
    {
      "constant": false,
      "inputs": [
        {
          "internalType": "address",
          "name": "from",
          "type": "address"
        },
        {
          "internalType": "address",
          "name": "to",
          "type": "address"
        },
        {
          "internalType": "uint256",
          "name": "tokenId",
          "type": "uint256"
        },
        {
          "internalType": "bytes",
          "name": "_data",
          "type": "bytes"
        }
      ],
      "name": "safeTransferFrom",
      "outputs": [],
      "payable": false,
      "stateMutability": "nonpayable",
      "type": "function"
    },
    {
      "constant": false,
      "inputs": [
        {
          "internalType": "address",
          "name": "to",
          "type": "address"
        },
        {
          "internalType": "bool",
          "name": "approved",
          "type": "bool"
        }
      ],
      "name": "setApprovalForAll",
      "outputs": [],
      "payable": false,
      "stateMutability": "nonpayable",
      "type": "function"
    },
    {
      "constant": true,
      "inputs": [
        {
          "internalType": "bytes4",
          "name": "interfaceId",
          "type": "bytes4"
        }
      ],
      "name": "supportsInterface",
      "outputs": [
        {
          "internalType": "bool",
          "name": "",
          "type": "bool"
        }
      ],
      "payable": false,
      "stateMutability": "view",
      "type": "function"
    },
    {
      "constant": true,
      "inputs": [
        {
          "internalType": "uint256",
          "name": "index",
          "type": "uint256"
        }
      ],
      "name": "tokenByIndex",
      "outputs": [
        {
          "internalType": "uint256",
          "name": "",
          "type": "uint256"
        }
      ],
      "payable": false,
      "stateMutability": "view",
      "type": "function"
    },
    {
      "constant": true,
      "inputs": [
        {
          "internalType": "address",
          "name": "owner",
          "type": "address"
        },
        {
          "internalType": "uint256",
          "name": "index",
          "type": "uint256"
        }
      ],
      "name": "tokenOfOwnerByIndex",
      "outputs": [
        {
          "internalType": "uint256",
          "name": "",
          "type": "uint256"
        }
      ],
      "payable": false,
      "stateMutability": "view",
      "type": "function"
    },
    {
      "constant": true,
      "inputs": [
        {
          "internalType": "uint256",
          "name": "tokenId",
          "type": "uint256"
        }
      ],
      "name": "tokenURI",
      "outputs": [
        {
          "internalType": "string",
          "name": "",
          "type": "string"
        }
      ],
      "payable": false,
      "stateMutability": "view",
      "type": "function"
    },
    {
      "constant": true,
      "inputs": [],
      "name": "totalSupply",
      "outputs": [
        {
          "internalType": "uint256",
          "name": "",
          "type": "uint256"
        }
      ],
      "payable": false,
      "stateMutability": "view",
      "type": "function"
    },
    {
      "constant": false,
      "inputs": [
        {
          "internalType": "address",
          "name": "from",
          "type": "address"
        },
        {
          "internalType": "address",
          "name": "to",
          "type": "address"
        },
        {
          "internalType": "uint256",
          "name": "tokenId",
          "type": "uint256"
        }
      ],
      "name": "transferFrom",
      "outputs": [],
      "payable": false,
      "stateMutability": "nonpayable",
      "type": "function"
    },
    {
      "constant": false,
      "inputs": [
        {
          "internalType": "address",
          "name": "newOwner",
          "type": "address"
        }
      ],
      "name": "transferOwnership",
      "outputs": [],
      "payable": false,
      "stateMutability": "nonpayable",
      "type": "function"
    },
    {
      "constant": false,
      "inputs": [
        {
          "internalType": "uint256[2]",
          "name": "a",
          "type": "uint256[2]"
        },
        {
          "internalType": "uint256[2][2]",
          "name": "b",
          "type": "uint256[2][2]"
        },
        {
          "internalType": "uint256[2]",
          "name": "c",
          "type": "uint256[2]"
        },
        {
          "internalType": "uint256[2]",
          "name": "input",
          "type": "uint256[2]"
        },
        {
          "internalType": "address",
          "name": "to",
          "type": "address"
        },
        {
          "internalType": "uint256",
          "name": "tokenId",
          "type": "uint256"
        }
      ],
      "name": "addSolution",
      "outputs": [],
      "payable": false,
      "stateMutability": "nonpayable",
      "type": "function"
    },
    {
      "constant": false,
      "inputs": [
        {
          "internalType": "address",
          "name": "to",
          "type": "address"
        },
        {
          "internalType": "uint256",
          "name": "tokenId",
          "type": "uint256"
        }
      ],
      "name": "mintNFT",
      "outputs": [
        {
          "internalType": "bool",
          "name": "",
          "type": "bool"
        }
      ],
      "payable": false,
      "stateMutability": "nonpayable",
      "type": "function"
    }
  ],
```


* OpenSea Market Place - https://rinkeby.opensea.io/assets/unidentified-contract-v370
* Picture and metadata is not coming as token id greater than 10.
* https://knowledge.udacity.com/questions/84458

##5 Token bought by account 0xC2c1E51365ca5b473B32CF9E39ce19C9Ee2F37a0

* https://rinkeby.opensea.io/assets/0xfb68b5688d3b2892cd2b01f028aa41838cca243c/1
* https://rinkeby.opensea.io/assets/0xfb68b5688d3b2892cd2b01f028aa41838cca243c/7
* https://rinkeby.opensea.io/assets/0xfb68b5688d3b2892cd2b01f028aa41838cca243c/8
* https://rinkeby.opensea.io/assets/0xfb68b5688d3b2892cd2b01f028aa41838cca243c/9
* https://rinkeby.opensea.io/assets/0xfb68b5688d3b2892cd2b01f028aa41838cca243c/10

![OpenSea Rinkeby marketplace](images/MP.png)


# Project Resources

* [Remix - Solidity IDE](https://remix.ethereum.org/)
* [Visual Studio Code](https://code.visualstudio.com/)
* [Truffle Framework](https://truffleframework.com/)
* [Ganache - One Click Blockchain](https://truffleframework.com/ganache)
* [Open Zeppelin ](https://openzeppelin.org/)
* [Interactive zero knowledge 3-colorability demonstration](http://web.mit.edu/~ezyang/Public/graph/svg.html)
* [Docker](https://docs.docker.com/install/)
* [ZoKrates](https://github.com/Zokrates/ZoKrates)
