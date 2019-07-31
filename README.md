# Quy trình chạy Dapp

- Bước 1: cài đặt và chạy ganache-cli
  + install 2 package `npm install ganache-cli web3` 
  + `npm install`
  + `npm start`
  + install solc để compile file .sol: `npm install solc`

- Bước 2 : chạy trong môi trường node console để compile contract

  ```

    $ node
    > Web3 = require('web3')
    > web3 = new Web3(new Web3.providers.HttpProvider("http://localhost:8545"));

    
  ```
  + kiểm tra query tất cả accounts : `web3.eth.accounts`
  + compile file Voting.sol: 
  ```
    > code = fs.readFileSync('Voting.sol').toString()
    > solc = require('solc')
    > compiledCode = solc.compile(code)

  ```

- Bước 3: Deploy contract
  ```
    > abiDefinition = JSON.parse(compiledCode.contracts[':Voting'].interface)
    > VotingContract = web3.eth.contract(abiDefinition)
    > byteCode = compiledCode.contracts[':Voting'].bytecode
    > deployedContract = VotingContract.new(['Rama','Nick','Jose'],{data: byteCode, from: web3.eth.accounts[0], gas: 4700000})
    > deployedContract.address
    > contractInstance = VotingContract.at(deployedContract.address)

  ```

- Bước 4 : Add địa chỉ của contract đã deploy vào index.js 
  + `deployedContract.address` để lấy địa chỉ của contractInstance
  + lấy địa chỉ đó add vào `contractInstance = VotingContract.at('addressContract');`


----
- có thế coppy toàn bộ phần này để chạy trong node console:

```

Web3 = require('web3')
web3 = new Web3(new Web3.providers.HttpProvider("http://localhost:8545"));
web3.eth.accounts
code = fs.readFileSync('Voting.sol').toString()
solc = require('solc')
compiledCode = solc.compile(code)
abiDefinition = JSON.parse(compiledCode.contracts[':Voting'].interface);
VotingContract = web3.eth.contract(abiDefinition);
byteCode = compiledCode.contracts[':Voting'].bytecode;
deployedContract = VotingContract.new(['Rama','Nick','Jose'],{data: byteCode, from: web3.eth.accounts[0], gas: 4700000});
deployedContract.address;
contractInstance = VotingContract.at(deployedContract.address);
deployedContract.address;

```