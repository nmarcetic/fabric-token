### Ethereum-style token [ERC-20 standard](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-20.md) smart contract for Hyperledger Fabric v1.x

How to use it:

1. Clone the repository to `$GOPATH/src/github.com`
2. Fetch the vendor packages `cd $GOPATH/src/github.com/token/chaincode && govendor fetch github.com/hyperledger/fabric/protos/msp`
2. Run tests: `cd $GOPATH/src/github.com/token/chaincode && go test`
3. Install on peers:

```
peer chaincode install -n token -v 1.0 -p github.com/token/chaincode
```
4. Instantiate on peers:
```
peer chaincode instantiate -o orderer_address:7050  -C mychannel -n token -v 1.0 -p github.com/token/chaincode -c '{"Args":["init","{\"name\": \"Fabric Demo Token\", \"symbol\": \"FTD\", \"decimals\": 2, \"totalSupply\": 1000}"]}'
```
5. Query balance:
```
peer chaincode query -C mychannel -n token -c '{"Args":["balance","{\"user\": \"myuser\"}"]}'
```
6. Invoke transfer:
```
peer chaincode invoke -o orderer_address:7050 -C mychannel -n token -c '{"Args":["transfer","{\"to\": \"otherUser\", \"value\": 200}"]}'
```
