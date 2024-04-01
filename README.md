# encode-tokenBallot-script
Homework 3 of the solidity bootcamp, create voting script to show tokenized ballot
## 1. create accounts for voting
```typescript
const [deployer, acc1, acc2, acc3, acc4] = await viem.getWalletClients();
```
Account1 address: 0x70997970c51812dc3a010c7d01b50e0d17dc79c8  
Account2 address: 0x3c44cdddb6a900fa2b585dd299e03d12fa4293bc  
Account3 address: 0x90f79bf6eb2c4f870365e785982e1f101e93b906  
Account4 address: 0x15d34aaf54267db7d7c367839aaf71a00a2c6a65  
## 2. deploy Token contract
```typescript
const contract = await viem.deployContract("MyToken");
```
Token contract deployed at 0x5fbdb2315678afecb367f032d93f642f64180aa3  
## 3. mint tokens
```typesript
const mintTxAcc1 = await contract.write.mint([acc1.account.address, MINT_VALUE,]);
const mintTxAcc2 = await contract.write.mint([acc2.account.address, MINT_VALUE,]);
const mintTxAcc3 = await contract.write.mint([acc3.account.address, MINT_VALUE,]);
```
Minted 100000000000000000000 decimal units to account 0x70997970c51812dc3a010c7d01b50e0d17dc79c8
Minted 100000000000000000000 decimal units to account 0x90f79bf6eb2c4f870365e785982e1f101e93b906
Minted 100000000000000000000 decimal units to account 0x90f79bf6eb2c4f870365e785982e1f101e93b906
### 3.1. Before deploying vote contract
When minting before deploying the vote contract, the block number will be lower and the voting power will be available.  
### 3.2. After deploying vote contract
In this case the block number of the vote contract will be earlier than the available voting power and voting will result in an error.  
```
details: "VM Exception while processing transaction: reverted with reason string 'Not enough votingpower'",
```
## 4. delegate voting power
```typescript
const delTxAcc1 = await contract.write.delegate([acc1.account.address], {account: acc1.account,});
const delTxAcc2 = await contract.write.delegate([acc2.account.address], {account: acc2.account,});
const delTxAcc3 = await contract.write.delegate([acc3.account.address], {account: acc3.account,});
```
Account 0x70997970c51812dc3a010c7d01b50e0d17dc79c8 has 100000000000000000000 units of voting power after self delegating  
Account 0x3c44cdddb6a900fa2b585dd299e03d12fa4293bc has 100000000000000000000 units of voting power after self delegating  
Account 0x90f79bf6eb2c4f870365e785982e1f101e93b906 has 100000000000000000000 units of voting power after self delegating  
## 5. deploy vote contract
## 6. voting
## 7. result
