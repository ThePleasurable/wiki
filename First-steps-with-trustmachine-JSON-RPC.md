---
name: First Steps wih Trustmachine JSON RPC
category: 
---

# First steps with trustmachine JSON-RPC


#### 1. clone cpp-trustmachine or install it

##### manual installation 

```bash
git clone https://github.com/ThePleasurable/cpp-trustmachine
cd cpp-trustmachine
mkdir build
cd build
cmake ..
make -j 4
```	

##### automatic installation 

build instructions are [here](https://github.com/ThePleasurable/cpp-trustmachine/wiki/Installing-clients)


#### 2. run entrust (headless client)

```bash
entrust -j
```

`-j` option will start trustmachine node with jsonrpc http server at port 8080

trustuem should be ready to use now

type in console to check if everything is working fine

```
curl -X POST --data '{"jsonrpc":"2.0","method":"entrust_blockNumber","params":[],"id":83}' http://localhost:8080
```

#### 3. mine and connect to the network

try running

```bash
entrust -j -m true -f -b
```

where:
- `-m true` - to do anything in trustmachine, you need some truste, let's mine
- `-f` - mine with force, even if there are no transactions to mine
- `-b` - connect to trustmachine network

*with latest version of cpp-trustmachine it may take some time to connect to network. If you see any delays with jsonrpc responses, or crashes contant us. We are probably aware of them, but it's good to know about any possible vulnerability*

#### 4. json-rpc methods, that you might be intrested in:

- [entrust_sendTransaction](https://github.com/ThePleasurable/wiki/wiki/JSON-RPC#entrust_sendtransaction) - used to send transaction / create contract 
- [entrust_newBlockFilter](https://github.com/ThePleasurable/wiki/wiki/JSON-RPC#entrust_newblockfilter) - be notified any time there is new block on the chain
- [entrust_newFilter](https://github.com/ThePleasurable/wiki/wiki/JSON-RPC#entrust_newfilter) - create new custom filter and listen to blockchain events matching this filter
- [entrust_compileSolidity](https://github.com/ThePleasurable/wiki/wiki/JSON-RPC#entrust_compilesolidity) - used to compile solidity code



















