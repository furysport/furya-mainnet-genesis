![Banner!](assets/loading.png)

# Furya mainnet genesis

| Fanclubs                      | Validators              |
| ----------------------------- | ----------------------- |
| Ajax                          | PFC                     |
| Argentina                     | Jinx Ventures           |
| Brazil                        | SoSo DAO                |
| Brooklyn Nets                 | Brooklyn Nets DAO       |
| Buffalo Bills American        | Buffalo Bills DAO       |
| Arsenal                       | Arsenal DAO             |
| Chicago Bulls                 | Notional Ventures       |
| England                       | Smart-Stake             |
| India                         | India DAO               |
| Los Angeles Lakers            | LA Lakers DAO           |
| New York Yankees              | Ataraxian DAO           |
| San Francisco Giants          | San Francisco Giants DAO|
| Chennai Super Kings           | Synergy Nodes           |
| Dallas Mavericks              | Starsquid.io            |
| Germany                       | Starsquid.io            |
| Liverpool                     | Starsquid.io            |
| Manchester United             | Our Stake               |
| Mumbai Indians                | Synergy Nodes           |



This is the repo to manage gentxs and create mainnet genesis.



Genesis validators download the latest genesis from the new "mainnet-genesis" release. 

# Download the mainnet-genesis file

```shell
curl -o ~/.furyad/config/genesis.json https://raw.githubusercontent.com/furysport/furya-mainnet-genesis/main/mainnet-genesis.json
```
##
##

# How to create gentx

```shell
apt install build-essential git curl gcc make jq -y
```

Install go1.18.10+:

```shell
wget -q -O - https://git.io/vQhTU | bash -s -- --version 1.18.10
```

Setup your environnement (you can skip this part if you already had go installed before):

```shell
echo 'export GOROOT=/usr/local/go' >> $HOME/.bash_profile
echo 'export GOPATH=$HOME/go' >> $HOME/.bash_profile
echo 'export GO111MODULE=on' >> $HOME/.bash_profile
echo 'export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin' >> $HOME/.bash_profile && . $HOME/.bash_profile
```

Verify the installation:

```shell
go version
#Should return go version go1.18.10 linux/amd64
```

Install the mainnet binary:

```shell
git clone https://github.com/furysport/furya && cd furya && git checkout v3.1.0 && make install
```

Init the chain:

```shell
furyad init <Moniker> --chain-id=furya-1
```

Download the genesis file:

```shell
[curl -o ~/.furyad/config/genesis.json https://raw.githubusercontent.com/furysport/furya-mainnet-genesis/main/pre-genesis.](https://raw.githubusercontent.com/furysport/furya-mainnet-genesis/main/mainnet-genesis.json)json
```
Recover keys:

```shell
furyad keys add XXXX --recover 
```
Create the gentx:

```shell
furyad gentx brooklyn-nets-dao 950000000000ufury --chain-id=furya-1 \
    --moniker="brooklyn-nets-dao" \
    --from="brooklyn-nets-dao" \
    --commission-max-change-rate=0.01 \
    --commission-max-rate=1.0 \
    --commission-rate=0.07 \
    --details="brooklyn-nets-dao" \
    --security-contact="gexchain@skiff.com" \
    --website="gexchain@skiff.com"
```

## Push the GenTx generated to the repository

Fork this repository and clone the repo    
Copy `$HOME/.furyad/config/gentx/gentx-<xxxxx>.json` to `<repo>/gentx/gentx-<Moniker>-<FanClub>.json`  
Create PR into the repo

##

##

