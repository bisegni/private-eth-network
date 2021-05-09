# private-eth-network
Project for an how-to on how create a custom private ETH network

## install ETH cli
for isntall all necessary software follow directly the main ETH [installation](https://geth.ethereum.org/docs/install-and-build/installing-geth) documentation

## setup
At the beginnig create a folder where we can create our genesis.json file an folder for test nodes, for exaple *private-eth* and the create two folder for node-1 and node-2 as in folow example:
```bash
mkdir -p private-eth/node-1 private-eth/node-2
```
Now we have our folder structure and in the beginning we need a genesis.json file for setup our node, an example of a genesis file can be of type of the one reported below, any a god pint to start for genesis.json exaplanation can be [here](https://ethereum.stackexchange.com/questions/2376/what-does-each-genesis-json-parameter-mean/2377):
```json
{
    "nonce": "0x0000000000000042",
    "timestamp": "0x0",
    "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "extraData": "0x00",
    "gasLimit": "0x8000000",
    "difficulty": "0x400",
    "mixhash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "coinbase": "0x3333333333333333333333333333333333333333",
    "alloc": {},
    "config": {"chainId": 987, "homesteadBlock": 0, "eip150Block":0 , "eip155Block": 0, "eip158Block": 0}
}
```

## init and start nodes
Now we can init and start the nodes; from within the our private-eth root folder we can launch these command:
```bash
geth --datadir node-1 init genesis.json
geth --datadir node-2 init genesis.json
```

after the initilization we can start the two node with the example below, keep in mind that the *--networkid* parameter value, in the example *132435* need to be equals for either the nodes, the published port obviously need to be different, because the nodes run on the same host:
```bash
geth --datadir node-1 --networkid 132435 --port 30303
geth --datadir node-2 --networkid 132435 --port 30304
```
After each nodes has been started wthin the node folder will be a file geth.ipc, this is a socket where a geth client can be attacched for let us to comunicate with a respective node. nowa the two command below can be launched in two different console
```bash
geth attach private-eth/node-1/geth.ipc
geth attach private-eth/node-2/geth.ipc
```

# create one account into each node
Now that all server are up and we are connected to each one, create in each of them a new account with the command:
```bash
personal.newAccount()
```
this command will ask for a password, memorize aither the address and the password of each account

NOTE: with commadn ```personal.listAccounts``` can be show the list of all acocunt on the node
