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
