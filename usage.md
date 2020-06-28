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
~ mkdir $HOME/.ethereum
~ new an eth account in ~/.ethereum with command: geth account new
```

3. set constant value in constant.go. firstly, cat ~/.ethereum/keystore/UTC--*;
```text
for example:
const ACCOUNT_KEY = `
{
  "address": "1a9ec3b0b807464e6d3398a59d6b0a369bf422fa",
  "crypto": {
    "cipher": "aes-128-ctr",
    "ciphertext": "a471054846fb03e3e271339204420806334d1f09d6da40605a1a152e0d8e35f3",
    "cipherparams": {
      "iv": "44c5095dc698392c55a65aae46e0b5d9"
    },
    "kdf": "scrypt",
    "kdfparams": {
      "dklen": 32,
      "n": 262144,
      "p": 1,
      "r": 8,
      "salt": "e0a5fbaecaa3e75e20bccf61ee175141f3597d3b1bae6a28fe09f3507e63545e"
    },
    "mac": "cb3f62975cf6e7dfb454c2973bdd4a59f87262956d5534cdc87fb35703364043"
  },
  "id": "e08301fb-a263-4643-9c2b-d28959f66d6a",
  "version": 3
}
`
```

4. start an ethereum node
```bash
mkdir node
~$WORKSPACE/bin/geth --datadir ./node  --networkid 666 --port 30301 --nodiscover --rpc --allow-insecure-unlock  console

#start local ethereum node
~ geth attach ipc:/services/data/geth/data/geth.ipc
~ geth attach http://localhost:8545

#start remote ethereum node
~ geth attach http://remote_test_net_ip:8545
~ geth attach ws://remote_test_net_ip:8546

```
There are four test net you can choose:Ropsten,Kovan,Rinkeby,Goerli, enjoy yourself.

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
~ ./ethfs data upload --path="file path that will be upload" --password="your eth wallet password" --copynum="how many copy will be store" --amount="how manys token you will pledge for this file"
```

## Withdraw Token
When a node want to leave the ethfs distribute system, she can choose to withdraw all eth token stored in smart contract:
```bash
~ ./ethfs  token withdraw --password="your eth wallet password" --amount="how many you want to withdraw, default is all"
```
