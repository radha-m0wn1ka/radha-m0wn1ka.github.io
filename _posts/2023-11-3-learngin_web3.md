https://docs.alchemy.com/docs/ethers-js-signer
## from tcp1ctf
```
https://themj0ln1r.github.io/posts/tcp1pctf
entervenu:------------
to get abi we can get it from remix or from solc
getting to know of solc
https://docs.soliditylang.org/en/latest/installing-solidity.html
npm install -g solc
->solc converts from a high-level solidity language into Ethereum Virtual Machine (EVM)
 bytecode so that it can be executed on the blockchain by EVM
to compile ->
solc Greeter.sol
$solcjs --help
```
## compile .sol using node
https://medium.com/coinmonks/how-to-compile-a-solidity-smart-contract-using-node-js-51ea7c6bf440
next
https://www.alchemy.com/overviews/solidity-compiler

## installing nvm in wsl
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash
<br>
nvm install node (node version manager)
## using solc js
$solcjs --help
$solcjs --abi/bin contract_file.sol
# guide to ethersjs
https://blog.finxter.com/i-created-a-counter-smart-contract-with-ether-js-heres-how/
### signer
- A Signer represents an account on the Ethereum Blockchain, and is most often backed by a private key represented by a mnemonic or residing on a Hardware Wallet
- The Provider attached to this Signer (if any).(signer.provder)
- https://docs.ethers.org/v6/api/providers/#Signer
### provider
```
- A Provider provides a connection to the blockchain, whch can be used to query its current state,
  simulate execution and send transactions to update the state.

- It is one of the most fundamental components of interacting with a blockchain application
 , and there are many ways to connect, such as over HTTP, WebSockets or injected providers such as MetaMask.
```
#### get default provider function

```
Returns a default provider for network.

If network is a WebSocketLike or string that begins with "ws:" or "wss:", a WebSocketProvider is returned backed by that WebSocket or URL.

If network is a string that begins with "HTTP:" or "HTTPS:", a JsonRpcProvider is returned connected to that URL.

Otherwise, a default provider is created backed by well-known public Web3 backends (such as INFURA) using community-provided API keys.

The options allows specifying custom API keys per backend (setting an API key to "-" will omit that provider) and options.exclusive can be set to either a backend name or and array of backend names, which will whitelist only those backends.

Current backend strings supported are:


"alchemy"
"ankr"
"cloudflare"
"etherscan"
"infura"
"publicPolygon"
"quicknode"
https://dev.to/yakult/03-understanding-blockchain-with-ethersjs-4-tasks-of-interacting-with-smart-contract-3ef6
```
## import vs require in detail
https://www.scaler.com/topics/nodejs/require-vs-import-nodejs/
## default vs named exports in detail
https://dev.to/shacodes/default-vs-named-exports-19hj
# 04-11-2023
https://docs.alchemy.com/docs/what-is-ethers-js
## send transaction using ethersjs infura 
https://docs.infura.io/tutorials/ethereum/send-a-transaction/send-a-transaction-2
# next
alchemy sdk whole folder
<br>
https://docs.alchemy.com/docs/ethers-js-signer 
```
require('dotenv').config();
const ethers = require('ethers');

ADDRESS = '0x1AC90AFd478F30f2D617b3Cb76ee00Dd73A9E4d3'
ABI = [{"inputs":[{"internalType":"string","name":"initialFlag","type":"string"},{"internalType":"string","name":"initialMessage","type":"string"}],"stateMutability":"nonpayable","type":"constructor"},{"inputs":[],"name":"enterVenue","outputs":[{"internalType":"string","name":"","type":"string"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"goBack","outputs":[{"internalType":"string","name":"","type":"string"}],"stateMutability":"view","type":"function"}]
// provider
const provider = new ethers.AlchemyProvider('sepolia', process.env.API_KEY);

const wallet = new ethers.Wallet(process.env.PRIVATE_KEY, provider);
async function main(){
    console.log("loging block num")
    console.log(await provider.getBlockNumber())
    const venueContract = new ethers.Contract(ADDRESS, ABI, wallet)
    const message = await venueContract.goBack();
    console.log(message);
    const flag = await venueContract.enterVenue(); 
    console.log(flag);
}
main()
```
# 05-11-2023
```
process :
In Node.js, process is a global object that provides information about the current Node.js process, as well as methods to interact with it
https://www.npmjs.com/package/dotenv
As early as possible in your application, import and configure dotenv:

require('dotenv').config()
console.log(process.env)
```
## storage layout
https://medium.com/@flores.eugenio03/exploring-the-storage-layout-in-solidity-and-how-to-access-state-variables-bf2cbc6f8018
```
Solidity provides 2²⁵⁶ slots (indexed from 0 to 2²⁵⁶- 1) each with a fixed length of 32 bytes.
State variables are stored according to their position declaration, length and wheter they are a value or dynamic type.
uint256 a; means a is of 256 bit size i.e 256/8=32 byte size
boolean 0x01(true) or 0x00(false) just 1 byte
address is a unique built-in type in Solidity that has a length of 20 byte
bytes32 has a visual length of 64
ex::
>>> s="0000000000000000000000cc8188e984b4c392091043caa73d227ef5e0d0a701"
 >>> len(s)
>>> 64
 >>>a="cc8188e984b4c392091043caa73d227ef5e0d0a7"
>>> len(a)
>>>40  
maximum length of any slot is 32 bytes
we can find out the values of a contracts state variable just by using
web3.eth.getStorageAt("0x338ba36a41a1713edeb4020031f30f5be1645d43","0")-contract address,slot position
 
```
## example on remix
```
contract Venue {
    bytes32 public key=0x0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef;
    bytes4 public key_1=0x99998888;
    bytes16 public key_2=0x99998888999988889999888899998888;
    address public owner=0xDA0bab807633f07f013f94DD0E6A4F96F8742B53;
    uint256 public Token;
    address public Courier=0xDA0bab807633f07f013f94DD0E6A4F96F8742B53;
    uint256 public lump_sum;
    bytes32 public password=0x0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef;
}
contract addres ,0x55AD49B102CE9a1AE3A30E8119cF886C4df1579c
slot 0 and slot 1
0x0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef
0x0000000000000000000000009999888899998888999988889999888899998888
in remix by going to compilation details we can get storage layout and abi


```
## foundry up
```
https://book.getfoundry.sh/getting-started/installation
curl -L https://foundry.paradigm.xyz | bash
foundryup
```
## function selector --cast
```
https://medium.com/coinmonks/function-selectors-in-solidity-understanding-and-working-with-them-25e07755e976
 function selector is a four-byte identifier determined through the Keccak (SHA-3) hash of the function's signature. The function signature is derived from the function name and the parenthesized list of parameter types. For instance, the function signature for a function named myFunction that takes an address and a uint256 would be myFunction(address,uint256).
bytes4(keccak256(bytes("function_name(type_of_argument1,type_of_arg2,..)" )))

radha@DESKTOP-E4J3HG3:~$ cast sig "fun1(arg1,arg2)"
  0xf5d93e45  --4bytes f5  d9 3e 45
```
## ways of interacting with a outside contract
### we have  contract  abi
```
equire('dotenv').config();
const ethers = require('ethers');

ADDRESS = '0x1AC90AFd478F30f2D617b3Cb76ee00Dd73A9E4d3'
ABI = [{"inputs":[{"internalType":"string","name":"initialFlag","type":"string"},{"internalType":"string","name":"initialMessage","type":"string"}],"stateMutability":"nonpayable","type":"constructor"},{"inputs":[],"name":"enterVenue","outputs":[{"internalType":"string","name":"","type":"string"}],"stateMutability":"view","type":"function"},{"inputs":[],"name":"goBack","outputs":[{"internalType":"string","name":"","type":"string"}],"stateMutability":"view","type":"function"}]
// provider
const provider = new ethers.AlchemyProvider('sepolia', process.env.API_KEY);

const wallet = new ethers.Wallet(process.env.PRIVATE_KEY, provider);
async function main(){
    const venueContract = new ethers.Contract(ADDRESS, ABI, wallet)
    const message = await venueContract.goBack();
    console.log(message);
    const flag = await venueContract.enterVenue(); 
    console.log(flag);
}
main()
```
### we have just contract address
->one way using some script on remix(need to know it)
```
another way using foundry

```
## forge create ..scripting 
https://book.getfoundry.sh/tutorials/solidity-scripting
```
Forge can deploy smart contracts to a given network with the forge create command.
$ forge create --rpc-url <your_rpc_url> --private-key <your_private_key> src/MyContract.sol:MyContract

Solidity scripting is a way to declaratively deploy contracts using Solidity, instead of using the more limiting and less user friendly forge create.

vm.envInt()
vm.envString()
we can write our contract in src folder
we go to script folder and in the run funciton we deploy our contract

```
