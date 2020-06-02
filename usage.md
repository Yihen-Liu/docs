# ![](https://img.shields.io/badge/status-wip-orange.svg?style=flat-square) Usage of ETHFSx

## Build from source
1. git clone ipfs relevantly.
```bash
~ git clone  https://github.com/Yihen/go-ipfs.git 
~ go mod tidy
~ cd go-ipfs/cmd/ipfs && go build
```

2. git clone contract source
```bash
~ git clone  https://github.com/Yihen/contracts.git
~ cd contracts/dataproof/contract && ./build.sh
```
By then, you will find a new dir named api has been generated. You can deploy it, or call api directly.

3. git clone ethereum source
```bash
~ git clone https://github.com/Yihen/go-ethereum.git
~ make geth
```
By then, you will find ethereum bin file named geth in build/bin dir.

4. git clone ethfs source
```bash
~ git clone https://github.com/Yihen/ethfs.git
~ cd ethfs && make
```
By then, you will find a bin file named __ethfs__ in ethfs/bin dir.

## Prepare for start
1. init ipfs workspace defaultly.
```bash
~ ./ipfs init
```
2. init ethereum workspace with a wallet
```bash
~ mkdir in ~ named .ethereum
~ new a eth wallet in ~/.ethereum
```

## Mining Start
Each node of ETHFS can running alonely for providing challenge response service. When other node want to download a file, it will send a challenge contract to the main chain. 
By then, Mining Node can choose to offer given challenge response.
```bash
~ cd  $GOPATH/ETHFSx/ethfs/bin
~ ./ethfs start --password="your eth wallet password" &
```

## Pledge Token
Before beginning to store data to ethfs system, we need to pledge some eth token to the smart contract
```bash
~ ./ethfs token pledge --password="your eth wallet password" --amount="amount you want to pledge to main chain" --address="your eth address"
```
## Download File
User can download file by cli command, for example:
```bash
~ ./ethfs data download --hash="file hash" --password="your eth wallet password"
```
## Upload File
User can upload file by cli command, for example:
```bash
~ ./ethfs data download --path="file path that will be upload" --password="your eth wallet password" --copynum="how many copy will be store" --amount="how manys token you will pledge for this file"
```

## Withdraw Token
When a node want to leave the ethfs distribute system, she can choose to withdraw all eth token stored in smart contract:
```bash
~ ./ethfs  token withdraw --password="your eth wallet password" --amount="how many you want to withdraw, default is all"
```
