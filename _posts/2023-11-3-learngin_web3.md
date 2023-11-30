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
# 06-11-2023
## msg -global varialble
https://medium.com/upstate-interactive/what-you-need-to-know-about-msg-global-variables-in-solidity-566f1e83cc69

## calldata
```
Calldata is a type of temporary storage, containing the data specified in a function’s arguments. The difference between it and memory, another type of temporary storage, is that calldata’s immutability—whatever is stored inside calldata cannot be changed.
```
## call 
```

https://medium.com/@solidity101/100daysofsolidity-understanding-the-call-function-in-solidity-interacting-with-contracts-4ccd216b1dfe#:~:text=The%20%E2%80%9Ccall%E2%80%9D%20function%20in%20Solidity%20enables%20contract%2Dto%2D,certain%20considerations%20and%20potential%20pitfalls.
https://www.alchemy.com/overviews/solidity-call
```
## send ether using call
### receive contract

```
create a contract and deploy it ,make sure it have a receive external payble function
ex:
contract ReceiveEther {
	// Function to receive Ether. msg.data must be empty
  receive() external payable {}‍
  
  // Fallback function is called when msg.data is not empty
  fallback() external payable {}‍
  
  function getBalance() public view returns (uint) {
  	return address(this).balance;
   }
  }

```
### send contract
```

contract SendEther {
	function sendViaCall(address payable _to) public payable {
  	// Call returns a boolean value indicating success or failure.
    (bool sent, bytes memory data) = _to.call{value: msg.value}("");
    require(sent, "Failed to send Ether");
   }
  }
```
### call function example
```
/ SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;

// import "forge-std/Script.sol";
import {Script} from "forge-std/Script.sol";
import "forge-std/console.sol";

contract SolveVIP is Script {
    function getHelp() public{
        address target = 0x52DF9c7cc8f8f5C8204F2401505A6248cE49d637;
        (bool success, bytes memory _help) = target.call(abi.encodeWithSignature("help()"));
        require(success);
        console.logBytes(abi.decode(_help, (bytes)));
    }
    function run() public {
        getHelp();
    }
}
forge script script/Solve.s.sol --rpc-url https://eth-sepolia.g.alchemy.com/v2/SMfUKiFXRNaIsjRSccFuYCq8Q3QJgks8
```
### abi decode
https://solidity-by-example.org/abi-decode/
```
https://book.getfoundry.sh/cast/
```

# 30-11-2023
## calling other contract highly useful links
```
https://solidity-by-example.org/call/

(bool success, bytes memory data) = _addr.call{value: msg.value, gas: 5000}(
            abi.encodeWithSignature("foo(string,uint256)", "call foo", 123)
        );
(bool success, bytes memory data) = _addr.call{value: msg.value}(
            abi.encodeWithSignature("doesNotExist()")
        );
(msg.sender).call{value: amount}("");

https://solidity-by-example.org/calling-contract/
```
### another function example
```

TARGET.buy{value: 10 ether}();

function buy() public payable
    {
        _mint(msg.value, msg.sender);
    }
function _mint(uint256 amount, address target) internal
    {
        balances[target] += amount;
    } 
```
## solidity scripting
https://book.getfoundry.sh/tutorials/solidity-scripting
## hello world
```// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;

import {Script, console2} from "forge-std/Script.sol";

contract HelloWorld {
    string public greet = "Hello World!";
}
contract CounterScript is Script {
    function setUp() public {}

    function run() public {
        HelloWorld helloWorld;
        
        helloWorld=new HelloWorld();
        console2.log(helloWorld.greet());
        
        vm.broadcast();
    }
}
 $anvil
 $forge script script/Counter.s.sol:CounterScript --fork-url http://localhost:8545 --broadcast
```
## another code
```
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;

import {Script, console2} from "forge-std/Script.sol";
import {HelloWorld} from "../src/HelloWorld.sol";
contract Attack{
    function  f1() public {
    HelloWorld helloWorld;
    helloWorld=new HelloWorld();

    console2.log("returned values is ", helloWorld.get());
    helloWorld.inc();
    helloWorld.inc();
    helloWorld.dec();
    console2.log("msg sender is ",msg.sender);
    console2.log("greetnig person is",helloWorld.greeting_person());
    console2.log(helloWorld.greet());
    console2.log("returned values is ", helloWorld.get());
    } 

}
contract CounterScript is Script {
    function setUp() public {}

    function run() public {
        Attack attack=new Attack();
        attack.f1();

        
        
        vm.broadcast();
    }
}

// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;

contract HelloWorld {
     uint  count;
     address public greeting_person;
    constructor(){
        greeting_person=msg.sender;
    }
    string public greet = "Hello World!";
   

    // Function to get the current count
    function get() public view returns (uint) {
        return count;
    }

    // Function to increment count by 1
    function inc() public {
        count += 1;
    }

    // Function to decrement count by 1
    function dec() public {
        // This function will fail if count = 0
        count -= 1;
    }
}
```

