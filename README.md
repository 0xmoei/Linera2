# Linera Series 2 Testnet

<h1 align="center"> Quest 1 </h1>
> follow my tweet (https://x.com/0xMoei/status/1788980488658423978) structures for Quest-1 besides running these codes

```console
# install dependecies
sudo apt-get install build-essential g++ libclang.dev libssl-dev protobuf-compiler

# install rust
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source "$HOME/.cargo/env"
rustup install stable
rustup update stable
rustup default stable
rustup target add wasm32-unknown-unknown

# install linera
git clone https://github.com/linera-io/linera-protocol
cd linera-protocol
cargo install --locked linera-service@^0.10 --bin linera

# check linera
linera

# run test
cd $HOME && cd linera-protocol/examples/fungible/tests
linera project test
```

<h1 align="center"> Quest 3 </h1>
> follow my tweet (https://x.com/0xMoei/status/1792308140936994832) structures for Quest-2 & Quest-3 besides running these codes

```console
# install dependecies
rustup target add wasm32-unknown-unknown
sudo apt-get install build-essential g++ libclang.dev libssl-dev protobuf-compiler
sudo apt install unzip

# install linera protoc-buffer
curl -LO https://github.com/protocolbuffers/protobuf/releases/download/v21.11/protoc-21.11-linux-x86_64.zip
unzip protoc-21.11-linux-x86_64.zip -d $HOME/.local
export PATH="$PATH:$HOME/.local/bin"
sudo apt-get update
cargo install --locked linera-service@^0.10 --bin linera

# wallet
linera wallet init --with-new-chain --faucet https://faucet.devnet-2024-03-26.linera.net/
linera sync
linera query-balance
linera wallet show

# create app
rm -rf fungible-app-tutorial
git clone https://github.com/linera-io/fungible-app-tutorial.git
linera project publish-and-create fungible-app-tutorial/ --json-argument '"100"'
git clone https://github.com/linera-io/meta-fungible-app-tutorial.git
cd meta-fungible-app-tutorial

# replace your fungible-app-id
export FUNGIBLE_APP_ID=REPLACE-WITH-YOUR-FUNGIBLE-APP-ID

# create app (it's all 1 command, copy them all)
linera project publish-and-create \
--required-application-ids $FUNGIBLE_APP_ID \
--json-parameters "\"$FUNGIBLE_APP_ID\""

# run app
linera service

# you can use --port xxxx if you wanna run it on a custom port
linera service --port 8085
```
> Once that’s done, open up a new window in your browser and visit the URL http://localhost:8080/ (it can be 8081 if 8080 is busy in your system)

<h1 align="center"> Quest 3 - Interact with dapp </h1>

```console
# 1
query {
  applications(chainId: "<REPLACE-WITH-YOUR-CHAIN-ID>") {
    id
    link
  }
}

# 2
mutation {
  transfer(owner: "<REPLACE-WITH-YOUR-OWNER-ID>", 
    amount: "10", 
    targetAccount:{
      chainId: "<REPLACE-WITH-YOUR-CHAIN-ID>",
      owner: "<REPLACE-WITH-ARBITRARY-RECIPIENT>"
    })
}

# 3
query {
  accounts{
    entry(key: "<REPLACE-WITH-YOUR-OWNER-ID>") {
      value
    }
  }
}
```
