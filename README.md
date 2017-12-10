# Introduction
This is a voting application based on Ethereum platform.  
Source: [Full Stack Hello World Voting Ethereum Dapp Tutorial](https://medium.com/@mvmurthy/full-stack-hello-world-voting-ethereum-dapp-tutorial-part-1-40d2d0d807c2)

# Installation
```
npm install ethereumjs-testrpc --save
npm install web3@0.20.1 --save
npm install solc --save
```

# How To Run
Start testrpc:
```
node_modules/.bin/testprc
```
Initialize a web3 object in the `node` console:
```
> Web3 = require('web3');
> web3 = new Web3(new Web3.providers.HttpProvider("http://localhost:8545"));
> web3.eth.accounts
```
Compile the contract:
```
> code = fs.readFileSync('voting.sol').toString()
> solc = require('solc')
> compiledCode = solc.compile(code)
```
Use `VotingContract.new` to deploy the contract:
```
> abiDefinition = JSON.parse(compiledCode.contracts[':Voting'].interface)
> VotingContract = web3.eth.contract(abiDefinition)
> byteCode = compiledCode.contracts[':Voting'].bytecode
> deployedContract = VotingContract.new(['Rama', 'Nick', 'Jose'], {data: byteCode, from: web3.eth.accounts[0], gas: 4700000})
> deployedContract.address
> contractInstance = VotingContract.at(deployedContract.address)
```
Interact with the contract:
```
> contractInstance.totalVotesFor.call('Rama')
> contractInstance.voteForCandidate('Rama', {from: web3.eth.accounts[0]})
> contractInstance.voteForCandidate('Rama', {from: web3.eth.accounts[0]})
> contractInstance.voteForCandidate('Rama', {from: web3.eth.accounts[0]})
> contractInstance.totalVotesFor.call('Rama')
```
