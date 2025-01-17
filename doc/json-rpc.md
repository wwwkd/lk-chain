# JSON RPC

<!-- TOC -->

- [JSON RPC](#json-rpc)
    - [JSON-RPC Endpoint](#json-rpc-endpoint)
    - [Curl Examples Explained](#curl-examples-explained)
    - [JSON-RPC methods](#json-rpc-methods)
        - [eth_accounts](#eth_accounts)
            - [Parameters](#parameters)
            - [Returns](#returns)
            - [Example](#example)
        - [eth_blockNumber](#eth_blocknumber)
            - [Parameters](#parameters-1)
            - [Returns](#returns-1)
            - [Example](#example-1)
        - [eth_getBalance](#eth_getbalance)
            - [Parameters](#parameters-2)
            - [Returns](#returns-2)
            - [Example](#example-2)
        - [eth_getBlockByHash](#eth_getblockbyhash)
            - [Parameters](#parameters-3)
            - [Returns](#returns-3)
            - [Example](#example-3)
        - [eth_getBlockByNumber](#eth_getblockbynumber)
            - [Parameters](#parameters-4)
            - [Returns](#returns-4)
            - [Example](#example-4)
        - [eth_getBlockTransactionCountByHash](#eth_getblocktransactioncountbyhash)
            - [Parameters](#parameters-5)
            - [Returns](#returns-5)
            - [Example](#example-5)
        - [eth_getBlockTransactionCountByNumber](#eth_getblocktransactioncountbynumber)
            - [Parameters](#parameters-6)
            - [Returns](#returns-6)
            - [Example](#example-6)
        - [eth_getRawTransactionByBlockHashAndIndex](#eth_getrawtransactionbyblockhashandindex)
            - [Parameters](#parameters-7)
            - [Returns](#returns-7)
            - [Example](#example-7)
        - [eth_getRawTransactionByBlockNumberAndIndex](#eth_getrawtransactionbyblocknumberandindex)
            - [Parameters](#parameters-8)
            - [Returns](#returns-8)
            - [Example](#example-8)
        - [eth_getRawTransactionByHash](#eth_getrawtransactionbyhash)
            - [Parameters](#parameters-9)
            - [Returns](#returns-9)
            - [Example](#example-9)
        - [eth_getTransactionCount](#eth_gettransactioncount)
            - [Parameters](#parameters-10)
            - [Returns](#returns-10)
            - [Example](#example-10)
        - [eth_getTransactionByBlockNumberAndIndex](#eth_gettransactionbyblocknumberandindex)
            - [Parameters](#parameters-11)
            - [Returns](#returns-11)
            - [Example](#example-11)
        - [eth_getTransactionByHash](#eth_gettransactionbyhash)
            - [Parameters](#parameters-12)
            - [Returns](#returns-12)
            - [Example](#example-12)
        - [eth_getTransactionReceipt](#eth_gettransactionreceipt)
            - [Parameters](#parameters-13)
            - [Returns](#returns-13)
            - [Example](#example-13)
        - [eth_sendRawTransaction](#eth_sendrawtransaction)
            - [Parameters](#parameters-14)
            - [Returns](#returns-14)
            - [Example](#example-14)
        - [eth_signTransaction](#eth_signtransaction)
            - [Parameters](#parameters-15)
            - [Returns](#returns-15)
            - [Example](#example-15)
        - [personal_unlockAccount](#personal_unlockaccount)
            - [Parameters](#parameters-16)
            - [Returns](#returns-16)
            - [Example](#example-16)
        - [personal_lockAccount](#personal_lockaccount)
            - [Parameters](#parameters-17)
            - [Returns](#returns-17)
            - [Example](#example-17)
        - [personal_newAccount](#personal_newaccount)
            - [Parameters](#parameters-18)
            - [Returns](#returns-18)
            - [Example](#example-18)
        - [personal_listAccounts](#personal_listaccounts)
            - [Parameters](#parameters-19)
            - [Returns](#returns-19)
            - [Example](#example-19)
        - [personal_listWallets](#personal_listwallets)
            - [Parameters](#parameters-20)
            - [Returns](#returns-20)
            - [Example](#example-20)

<!-- /TOC -->

## JSON-RPC Endpoint

Default JSON-RPC endpoints: <http://localhost:44000>.
Endpoints is defined by ethermint rpcport.

```shell
ethermint --rpc --rpcaddr <ip> --rpcport <portnumber> --rpccorsdomain "http://localhost:44000"
```

## Curl Examples Explained

The curl options below might return a response where the node complains about the content type, this is because the --data option sets the content type to application/x-www-form-urlencoded . If your node does complain, manually set the header by placing -H "Content-Type: application/json" at the start of the call.

The examples also do not include the URL/IP & port combination which must be the last argument given to curl e.x. 127.0.0.1:44000

## JSON-RPC methods

### eth_accounts

Returns a list of addresses owned by client.

#### Parameters

none

#### Returns

Array of DATA, 20 Bytes - addresses owned by the client.

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_accounts","params":[],"id":1}' -H 'Content-Type:application/json'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": ["0xc94770007dda54cF92009BFF0dE90c06F603a09f"]
}
```

***

### eth_blockNumber

Returns the number of most recent block.

#### Parameters

none

#### Returns

QUANTITY - integer of the current block number the client is on.

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}' -H 'Content-Type:application/json'

// Result
{
  "id":83,
  "jsonrpc": "2.0",
  "result": "0xc94" // 1207
}
```

***

### eth_getBalance

Returns the balance of the account of given address.

#### Parameters

- DATA, 20 Bytes - address to check for balance.
- QUANTITY|TAG - integer block number, or the string "latest", "earliest" or "pending", see the default block parameter
Example Parameters

```json
params: [
   "0xc94770007dda54cF92009BFF0dE90c06F603a09f",
   "latest"
]
```

#### Returns

QUANTITY - integer of the current balance in wei.

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getBalance","params":["0xc94770007dda54cF92009BFF0dE90c06F603a09f", "latest"],"id":1}' -H 'Content-Type:application/json'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0x0234c8a3397aab58" // 158972490234375000
}
```

***

### eth_getBlockByHash

Returns information about a block by hash.

#### Parameters

- DATA, 32 Bytes - Hash of a block.
- Boolean - If true it returns the full transaction objects, if false only the hashes of the transactions.

Example Parameters

```json
params: [
   "0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331",
   true
]
```

#### Returns

Object - A block object, or null when no block was found:

- number: QUANTITY - the block number. null when its pending block.
- hash: DATA, 32 Bytes - hash of the block. null when its pending block.
- parentHash: DATA, 32 Bytes - hash of the parent block.
- nonce: DATA, 8 Bytes - hash of the generated proof-of-work. null when its pending block.
- sha3Uncles: DATA, 32 Bytes - SHA3 of the uncles data in the block.
- logsBloom: DATA, 256 Bytes - the bloom filter for the logs of the block. null when its pending block.
- transactionsRoot: DATA, 32 Bytes - the root of the transaction trie of the block.
- stateRoot: DATA, 32 Bytes - the root of the final state trie of the block.
- receiptsRoot: DATA, 32 Bytes - the root of the receipts trie of the block.
- miner: DATA, 20 Bytes - the address of the beneficiary to whom the mining rewards were given.
- difficulty: QUANTITY - integer of the difficulty for this block.
- totalDifficulty: QUANTITY - integer of the total difficulty of the chain until this block.
- extraData: DATA - the "extra data" field of this block.
- size: QUANTITY - integer the size of this block in bytes.
- gasLimit: QUANTITY - the maximum gas allowed in this block.
- gasUsed: QUANTITY - the total used gas by all transactions in this block.
- timestamp: QUANTITY - the unix timestamp for when the block was collated.
- transactions: Array - Array of transaction objects, or 32 Bytes transaction hashes depending on the last given parameter.

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getBlockByHash","params":["0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331", true],"id":1}' -H 'Content-Type:application/json'
// Result
{
    "jsonrpc": "2.0",
    "id": 67,
    "result": {
        "gasLimit": "0x12a05f200",
        "gasUsed": "0x0",
        "hash": "0xae51471fee367142fd4fbd9b3396ddb97adadb2d9bfe15320f701f5d9c7bc5c4",
        "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
        "miner": "0x0e61f85dcf1afe432da9a161f329eb80ad02b800",
        "number": "0x561c",
        "parentHash": "0x5fa71039aa4a6346bbc1c2171dae3fae7e43ed90586862aacf2bee10e5154552",
        "receiptsRoot": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "size": "0x4e8",
        "stateRoot": "0x05848750d53889e89938971bcca84aac547032807fc436aa453a834ee6756ebf",
        "timestamp": "0x5cdaafb9",
        "transactions": [

        ],
        "transactionsRoot": "0x0000000000000000000000000000000000000000000000000000000000000000"
    }
}
```

***

### eth_getBlockByNumber

Returns information about a block by block number.

#### Parameters

- QUANTITY|TAG - integer of a block number, or the string "earliest", "latest" or "pending", as in the default block parameter.
- Boolean - If true it returns the full transaction objects, if false only the hashes of the transactions.

Example Parameters

```json
params: [
   "0x1b4", // 436
   true
]
```

#### Returns

See **eth_getBlockByHash**

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["0x1b4", true],"id":1}' -H 'Content-Type:application/json'
```

Result see [**eth_getBlockByHash**](#eth_getBlockByHash)

***

### eth_getBlockTransactionCountByHash

Returns the number of transactions in a block from a block matching the given block hash.

#### Parameters

- DATA, 32 Bytes - hash of a block.

Example Parameters

```json
params: [
   "0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238"
]
```

#### Returns

QUANTITY - integer of the number of transactions in this block.

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getBlockTransactionCountByHash","params":["0xc94770007dda54cF92009BFF0dE90c06F603a09f"],"id":1}' -H 'Content-Type:application/json'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xc" // 11
}
```

***

### eth_getBlockTransactionCountByNumber

Returns the number of transactions in a block matching the given block number.

#### Parameters

- QUANTITY|TAG - integer of a block number, or the string "earliest", "latest" or "pending", as in the default block parameter.

Example Parameters

```json
params: [
   "0xe8", // 232
]
```

#### Returns

QUANTITY - integer of the number of transactions in this block.

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getBlockTransactionCountByNumber","params":["0xe8"],"id":1}' -H 'Content-Type:application/json'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xa" // 10
}
```

***

### eth_getRawTransactionByBlockHashAndIndex

Returns raw transaction.

#### Parameters

- block hash - block hash.
- transaction index - tx index.

#### Returns

transaction raw.

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getRawTransactionByBlockHashAndIndex","params":["0x3d4c49493237ea2c61cd003402ce517e2959bf64319fa354ffce3f3122889bf7","0x0"],"id":67}' -H 'Content-Type:application/json'

// Result
{
    "jsonrpc": "2.0",
    "id": 67,
    "result": "0xf8728085174876e800830186a09401dabe71ff3795018dbbe720be6f01f3e8fc09288b0422ca8b0a00a4250000008082ecdca0d14a011bfb14943e5c74372f4020933482cad19bae474b67a38c1bd76fdf1780a0351efbc2c6806187501ff24850b60bd95b7d9127e13e416f1228be5b86aed4e1"
}
```

***

### eth_getRawTransactionByBlockNumberAndIndex

Returns raw transaction.

#### Parameters

- block number
- transaction index

#### Returns

transaction raw.

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getRawTransactionByBlockNumberAndIndex","params":["0x1","0x0"],"id":67}' -H 'Content-Type:application/json'

// Result
{
    "jsonrpc": "2.0",
    "id": 67,
    "result": "0xf8728085174876e800830186a09401dabe71ff3795018dbbe720be6f01f3e8fc09288b0422ca8b0a00a4250000008082ecdca0d14a011bfb14943e5c74372f4020933482cad19bae474b67a38c1bd76fdf1780a0351efbc2c6806187501ff24850b60bd95b7d9127e13e416f1228be5b86aed4e1"
}
```

***

### eth_getRawTransactionByHash

Returns raw transaction.

#### Parameters

transaction hash

#### Returns

transaction raw.

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getRawTransactionByHash","params":["0x7e40e15b5ff5bb1d8857dee204b6c2df37bf7bef058faf8d526d0bdd9a6d9ee8"],"id":67}' -H 'Content-Type:application/json'

// Result
{
    "jsonrpc": "2.0",
    "id": 67,
    "result": "0xf8728085174876e800830186a09401dabe71ff3795018dbbe720be6f01f3e8fc09288b0422ca8b0a00a4250000008082ecdca0d14a011bfb14943e5c74372f4020933482cad19bae474b67a38c1bd76fdf1780a0351efbc2c6806187501ff24850b60bd95b7d9127e13e416f1228be5b86aed4e1"
}
```

***

### eth_getTransactionCount

Return transaction count.

#### Parameters

- address - account
- block - last/earliest/ blockNumber

#### Returns

account nonce.

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getTransactionCount","params":["0x54fb1c7d0f011dd63b08f85ed7b518ab82028100","latest"],"id":67}' -H 'Content-Type:application/json'

// Result
{
    "jsonrpc": "2.0",
    "id": 67,
    "result":"0x4cb"
}
```

***

### eth_getTransactionByBlockNumberAndIndex

Returns information about a transaction by block number and transaction index position.

#### Parameters

- QUANTITY|TAG - a block number, or the string "earliest", "latest" or "pending", as in the default block parameter.
- QUANTITY - the transaction index position.

Example Parameters

```json
params: [
   "0x29c", // 668
   "0x0" // 0
]
```

#### Returns

See **eth_getTransactionByHash**

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getTransactionByBlockNumberAndIndex","params":["0x29c", "0x0"],"id":1}' -H 'Content-Type:application/json'
```

Result see [**eth_getTransactionByHash**](#eth_getTransactionByHash)

***

### eth_getTransactionByHash

Returns the information about a transaction requested by transaction hash.

#### Parameters

DATA, 32 Bytes - hash of a transaction

Example Parameters

```json
params: [
   "0x88df016429689c079f3b2f6ad39fa052532c56795b733da78a91ebe6a713944b"
]
```

#### Returns

Object - A transaction object, or null when no transaction was found:

- blockHash: DATA, 32 Bytes - hash of the block where this transaction was in. null when its pending.
- blockNumber: QUANTITY - block number where this transaction was in. null when its pending.
- from: DATA, 20 Bytes - address of the sender.
- gas: QUANTITY - gas provided by the sender.
- gasPrice: QUANTITY - gas price provided by the sender in Wei.
- hash: DATA, 32 Bytes - hash of the transaction.
- input: DATA - the data send along with the transaction.
- nonce: QUANTITY - the number of transactions made by the sender prior to this one.
- to: DATA, 20 Bytes - address of the receiver. null when its a contract creation transaction.
- transactionIndex: QUANTITY - integer of the transaction's index position in the block. null when its pending.
- value: QUANTITY - value transferred in Wei.
- v: QUANTITY - ECDSA recovery id
- r: DATA, 32 Bytes - ECDSA signature r
- s: DATA, 32 Bytes - ECDSA signature s

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getTransactionByHash","params":["0x88df016429689c079f3b2f6ad39fa052532c56795b733da78a91ebe6a713944b"],"id":1}' -H 'Content-Type:application/json'

// Result
{
  "jsonrpc":"2.0",
  "id":1,
  "result":{
    "blockHash":"0x1d59ff54b1eb26b013ce3cb5fc9dab3705b415a67127a003c3e61eb445bb8df2",
    "blockNumber":"0x5daf3b", // 6139707
    "from":"0xa7d9ddbe1f17865597fbd27ec712455208b6b76d",
    "gas":"0xc350", // 50000
    "gasPrice":"0x4a817c800", // 20000000000
    "hash":"0x88df016429689c079f3b2f6ad39fa052532c56795b733da78a91ebe6a713944b",
    "input":"0x68656c6c6f21",
    "nonce":"0x15", // 21
    "to":"0xf02c1c8e6114b1dbe8937a39260b5b0a374432bb",
    "transactionIndex":"0x41", // 65
    "value":"0xf3dbb76162000", // 4290000000000000
    "v":"0x25", // 37
    "r":"0x1b5e176d927f8e9ab405058b2d2457392da3e20f328b16ddabcebc33eaac5fea",
    "s":"0x4ba69724e8f69de52f0125ad8b3c5c2cef33019bac3249e2c0a2192766d1721c"
  }
}
```

***

### eth_getTransactionReceipt

Returns the receipt of a transaction by transaction hash.

**Note** That the receipt is not available for pending transactions.

#### Parameters

- DATA, 32 Bytes - hash of a transaction

Example Parameters

```json
params: [
   "0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238"
]
```

#### Returns

Object - A transaction receipt object, or null when no receipt was found:

- transactionHash : DATA, 32 Bytes - hash of the transaction.
- transactionIndex: QUANTITY - integer of the transaction's index position in the block.
- blockHash: DATA, 32 Bytes - hash of the block where this transaction was in.
- blockNumber: QUANTITY - block number where this transaction was in.
- from: DATA, 20 Bytes - address of the sender.
- to: DATA, 20 Bytes - address of the receiver. null when it's a contract creation transaction.
- cumulativeGasUsed : QUANTITY - The total amount of gas used when this transaction was executed in the block.
- gasUsed : QUANTITY - The amount of gas used by this specific transaction alone.
- contractAddress : DATA, 20 Bytes - The contract address created, if the transaction was a contract creation, otherwise null.
- logs: Array - Array of log objects, which this transaction generated.
- logsBloom: DATA, 256 Bytes - Bloom filter for light clients to quickly retrieve related logs.

It also returns either :

- root : DATA 32 bytes of post-transaction stateroot (pre Byzantium)
- status: QUANTITY either 1 (success) or 0 (failure)

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getTransactionReceipt","params":["0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238"],"id":1}' -H 'Content-Type:application/json'

// Result
{
"id":1,
"jsonrpc":"2.0",
"result": {
     transactionHash: '0xb903239f8543d04b5dc1ba6579132b143087c68db1b2168786408fcbce568238',
     transactionIndex:  '0x1', // 1
     blockNumber: '0xb', // 11
     blockHash: '0xc6ef2fc5426d6ad6fd9e2a26abeab0aa2411b7ab17f30a99d3cb96aed1d1055b',
     cumulativeGasUsed: '0x33bc', // 13244
     gasUsed: '0x4dc', // 1244
     contractAddress: '0xb60e8dd61c5d32be8058bb8eb970870f07233155', // or null, if none was created
     logs: [{
         // logs as returned by getFilterLogs, etc.
     }, ...],
     logsBloom: "0x00...0", // 256 byte bloom filter
     status: '0x1'
  }
}
```

***

### eth_sendRawTransaction

Creates new message call transaction or a contract creation for signed transactions.

#### Parameters

DATA, The signed transaction data.

Example Parameters

```json
params: ["0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"]
```

#### Returns

- DATA, 32 Bytes - the transaction hash, or the zero hash if the transaction is not yet available.

Use eth_getTransactionReceipt to get the contract address, after the transaction was mined, when you created a contract.

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_sendRawTransaction","params":[{see above}],"id":1}' -H 'Content-Type:application/json'

// Result
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xe670ec64341771606e55d6b4ca35a1a6b75ee3d5145a99d05921026d1527331"
}
```

### eth_signTransaction

Creates new message call transaction or a contract creation, if the data field contains code.  

**Note** This method needs to unlock the from account first.

#### Parameters

Object - The transaction object

- from: DATA, 20 Bytes - The address the transaction is send from.
- to: DATA, 20 Bytes - (optional when creating new contract) The address the transaction is directed to.
- gas: QUANTITY - (optional, default: 90000) Integer of the gas provided for the transaction execution. It will return unused gas.
- gasPrice: QUANTITY - (optional, default: To-Be-Determined) Integer of the gasPrice used for each paid gas
- value: QUANTITY - (optional) Integer of the value sent with this transaction
- data: DATA - The compiled code of a contract OR the hash of the invoked method signature and encoded parameters. For details see Ethereum Contract ABI
- nonce: QUANTITY - Integer of a nonce. This allows to overwrite your own pending transactions that use the same nonce.

Example Parameters

```json
params: [{
  "from": "0xb60e8dd61c5d32be8058bb8eb970870f07233155",
  "to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",
  "gas": "0x76c0", // 30400
  "gasPrice": "0x9184e72a000", // 10000000000000
  "value": "0x9184e72a", // 2441406250
  "data": "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675",
  "nonce":"0x1"
}]
```

**Note**:If the client concurrently sends a transaction from an account, you'd better manage the nonce value yourself, otherwise a nonce related error will occur.

#### Returns

- DATA, 32 Bytes - the transaction hash, or the zero hash if the transaction is not yet available.

Use **eth_getTransactionReceipt** to get the contract address, after the transaction was mined, when you created a contract.

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_signTransaction","params":[{"from":"0x54fb1c7d0f011dd63b08f85ed7b518ab82028100","to":"0xd46e8dd67c5d32be8058bb8eb970870f07244567","gas":"0x76c0","gasPrice":"0x9184e72a000","value":"0x9184e72a","data":"0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675","nonce":"0x1"}],"id":67}' -H 'Content-Type:application/json'

// Result
{
    "jsonrpc": "2.0",
    "id": 67,
    "result": {
        "raw": "0xf8930185174876e8008276c094d46e8dd67c5d32be8058bb8eb970870f07244567849184e72aa9d46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f07244567582ecdba0fae8403192e252da20616f46583d47852c2f242b6809772f4bb93662e0bb4618a06301da7d4fcfa45f31618ae1afbe12fa6e1e17395b023b764d37053fa8858c14",
        "tx": {
            "nonce": "0x1",
            "gasPrice": "0x174876e800",
            "gas": "0x76c0",
            "to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",
            "value": "0x9184e72a",
            "input": "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675",
            "v": "0xecdb",
            "r": "0xfae8403192e252da20616f46583d47852c2f242b6809772f4bb93662e0bb4618",
            "s": "0x6301da7d4fcfa45f31618ae1afbe12fa6e1e17395b023b764d37053fa8858c14",
            "hash": "0x720d1f748629d4c2513a17201dd9175e6f27f503caa4df43d93fe4b289e1b40d"
        }
    }
}

```

***

### personal_unlockAccount

unlock Account

#### Parameters

- address - local account which needs to unlock.
- password - account password.
- unlockSeconds - unlock seconds.

#### Returns

Boolean - true success,otherwise false.

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"personal_unlockAccount","params":["0x54fb1c7d0f011dd63b08f85ed7b518ab82028100","1234",3600],"id":67}' -H 'Content-Type:application/json'

// Result
{
    "jsonrpc": "2.0",
    "id": 67,
    "result": true
}
```

***

### personal_lockAccount

lock Account

#### Parameters

address - local account which needs to lock.

#### Returns

Boolean - true success,otherwise false.

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"personal_lockAccount","params":["0x54fb1c7d0f011dd63b08f85ed7b518ab82028100"],"id":67}' -H 'Content-Type:application/json'

// Result
{
    "jsonrpc": "2.0",
    "id": 67,
    "result": true
}
```

***

### personal_newAccount

new Account

#### Parameters

password - string, account password.

#### Returns

account - account hash

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"personal_newAccount","params":["1234"],"id":67}' -H 'Content-Type:application/json'

// Result
{
    "jsonrpc": "2.0",
    "id": 67,
    "result": "0x8d160ce3fc01f067e5e58f0cc4c89ae5fdb3f3af"
}
```

***

### personal_listAccounts

list all local Accounts

#### Parameters

none

#### Returns

accounts - local account list.

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"personal_listAccounts","params":[],"id":67}' -H 'Content-Type:application/json'

// Result
{
    "jsonrpc": "2.0",
    "id": 67,
    "result": [
        "0x54fb1c7d0f011dd63b08f85ed7b518ab82028100",
        "0x7b6837189a3464d3c696069b2b42a9ae8e17dda1",
        "0x6e18e41a4357157487548dcf0c8826151d7d1073",
        "0xbab556fe7cee72691d510287ed6d897a37461929",
        "0x3e28415fc8893d67c753c4eee3515b5738ae810f"
    ]
}
```

***

### personal_listWallets

list all local Accounts wallets.

#### Parameters

none

#### Returns

wallets -  a list of local wallets info.

#### Example

```shell
// Request
curl -X POST --data '{"jsonrpc":"2.0","method":"personal_listWallets","params":[],"id":67}' -H 'Content-Type:application/json'

// Result
{
    "jsonrpc": "2.0",
    "id": 67,
    "result": [
        {
            "url": "keystore:///usr/local/ethermint/peer_data/keystore/UTC--2016-10-21T22-30-03.071787745Z--7eff122b94897ea5b0e2a9abf47b86337fafebdc",
            "status": "Locked",
            "accounts": [
                {
                    "address": "0x54fb1c7d0f011dd63b08f85ed7b518ab82028100",
                    "url": "keystore:///usr/local/ethermint/peer_data/keystore/UTC--2016-10-21T22-30-03.071787745Z--7eff122b94897ea5b0e2a9abf47b86337fafebdc"
                }
            ]
        }
    ]
}
```
