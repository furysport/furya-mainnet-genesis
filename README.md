![Banner!](assets/loading.png)

# Furya mainnet genesis

This is the repo to manage gentxs and create mainnet genesis.

Genesis validators can check their addresses in the pre-genesis file to confirm balances and submit their gentxs

```
## How to create gentx
```

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
curl -o ~/.furyad/config/genesis.json https://raw.githubusercontent.com/furysport/furya-mainnet-genesis/main/pre-genesis.json
```
Recover keys:

```shell
furyad keys add XXXX --recover 
```
Create the gentx:

```shell
furyad gentx brooklyn-nets-dao 9500000000000ufury --chain-id=furya-1 \
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

## Note:

1. Save `<YOUR_KEY>` seed phrase and `priv_validator_key.json` from the .furyad/config folder, in a secure place offline.
2. Ensure you 500,000 FURY in a kujira wallet to qualify for your genesis allocation of an equivalent amount of FURY on Mainnet
3. Use the Identity field to submit your selected Fan Club (please check the availability of the Fan Club you are selecting by checking both the list above and the gentx folder for already submitted gentxs)
4. Use the details field to submit your kujira-address
5. Update the list of Fan Clubs above with your selected validator details
