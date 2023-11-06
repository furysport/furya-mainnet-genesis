![Banner!](assets/loading.png)

# Furya mainnet genesis

This is the repo to manage gentxs and create mainnet genesis.

## List of fan-clubs and associated validators to be on genesis

```
| Ajax                   | 159973 $FURY                                |
|-Al Hilal S-------------|-94863  $FURY--------------------------------|
| Al Sadd                | 656804 $FURY                                |
| Argentina              | 294465  $FURY     Fanfury-Genesis-Validator |
| Arsenal                | 511287      $FURY AR-Validators             |
| Atalanta               | 50200 $FURY                                 |
| Barcelona              | 26601 $FURY                                 |
| Bayern Munich Fan Club | 70500 $FURY                                 |
| Belgium                | 50200 $FURY                                 |
| Borussia Dortmund      | 55425 $FURY                                 |
| Brazil                 | 110537      $FURY BR-Validators             |
| Brooklyn Nets          | 159732      $FURY BN-Validators             |
| Buffalo Bills          | 320218 $FURY      BF-Validators             |
| Chelsea                | 72940 $FURY                                 |
| Chennai Super Kings    | 53548 $FURY                                 |
| Chicago Bears          | 50200 $FURY                                 |
| Chicago Bulls          | 425201  $FURY                               |
| Dallas Cowboys         | 52547       $FURY                           |
| Dallas Mavericks       | 53732 $FURY                                 |
| Denver Broncos         | 50200 $FURY                                 |
| England                | 219656      $FURY                           |
| Fan Club Utrecht       | 53826 $FURY                                 |
| Feyenoord Rotterdam    | 55105 $FURY                                 |
| France                 | 60200 $FURY                                 |
| Germany                | 64851 $FURY                                 |
| Green Bay Packers      | 56732 $FURY                                 |
| Houston Rockets        | 53825 $FURY                                 |
| India                  | 197017      $FURY IN-Validators             |
| Inter Milan            | 53594 $FURY                                 |
| Italy                  | 60200 $FURY                                 |
| Juventus               | 80668 $FURY                                 |
| Kansas City Chiefs     | 25200 $FURY                                 |
| Kolkata Knight Riders  | 45200 $FURY                                 |
| Liverpool              | 149975      $FURY Kujira-Validator          |
| Los Angeles Angels     | 27547 $FURY                                 |
| Los Angeles Lakers     | 238436      $FURY LA-Validators             |
| Manchester City        | 62492 $FURY                                 |
| Manchester United      | 229516  $FURY                               |
| Memphis Grizzlies      | 25200 $FURY                                 |
| Miami Dolphins         | 30946 $FURY                                 |
| Milwaukee Bucks        | 25200 $FURY                                 |



```

## How to create gentx

Install few packages:

```shell
apt install build-essential git curl gcc make jq -y
```

Install go1.20.0+:

```shell
wget -q -O - https://git.io/vQhTU | bash -s -- --version 1.20
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
#Should return go version go1.20.0 linux/amd64
```

Install the mainnet binary:

```shell
git clone https://github.com/furysport/furya && cd furya && git switch v2.0.0 && git checkout v2.0.0 && make install
```

Init the chain:

```shell
furyad init <Moniker> --chain-id=furya-1
```

Download the genesis file:

```shell
curl -o ~/.furya/config/genesis.json https://raw.githubusercontent.com/furysport/furya-mainnet-genesis/main/genesis.json
```
Recover keys:

```shell
furyad keys add XXXX --recover 
```
Create the gentx:

```shell
furyad genesis gentx <moniker> 100000000000ufury --chain-id=furya-1 \
    --moniker="XXXXXXXX" \
    --from="XXXXXXXX" \
    --commission-max-change-rate=0.01 \
    --commission-max-rate=1.0 \
    --commission-rate=0.07 \
    --details="XXXXXXXX" \
    --security-contact="XXXXXXXX" \
    --website="XXXXXXXX"
```

## Push the GenTx generated to the repository

Fork this repository and clone the repo    
Copy `$HOME/.furya/config/gentx/gentx-<xxxxx>.json` to `<repo>/gentx/gentx-<Moniker>-<FanClub>.json`  
Create PR into the repo

##

##

## Note:

1. Save `<YOUR_KEY>` seed phrase and `priv_validator_key.json` from the .furyad/config folder, in a secure place offline.
2. Ensure you 1,000,000 FURY in a kujira wallet to qualify for your genesis allocation of an equivalent amount of FURY on Mainnet
3. Use the Identity field to submit your selected Fan Club (please check the availability of the Fan Club you are selecting by checking both the list above and the gentx folder for already submitted gentxs)
4. Use the details field to submit your kujira-address
5. Update the list of Fan Clubs above with your selected validator details
