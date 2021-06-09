# LikeCoin
Instructions on how to set up LikeCoin node and create validator.

1. Update and upgrade packages:
```
sudo apt update
sudo apt upgrade --yes
```
2. Install git and curl:
```
sudo apt install git curl --yes
```
3. Install docker using Snap:
```
sudo apt install snapd --yes
snap install docker 
```
4. Install Docker Compose (you may use another version if you want):
```
sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
5. Clone LikeCoin project:
```
git clone https://github.com/likecoin/likecoin-chain --branch sheungwan --single-branch
```
6. Go to ``likecoin-chain`` folder and run ``build.sh`` script:
```
cd likecoin-chain
./scripts/build.sh
```
7. Download ``genesis.json`` file:
```
wget https://gist.githubusercontent.com/nnkken/1d1b9d4aae4acb3d835dd3150f546d44/raw/4d97fd471b4bf3be8c5475efbc0361f4926e65e5/genesis.json
```
8. Run ``init.sh`` script, replace ``<your_moniker>`` with your node name; enter the password with at least 8 characters (you will use it to sign all transactions). **Important**: write  mnemonic phrase in a safe place:
```
./scripts/init.sh <your_moniker> genesis.json 913bd0f4bea4ef512ffba39ab90eae84c1420862@34.82.131.35:26656 
```
9. Create and run the Docker containers:
```
docker-compose up -d
```
10. Check logs and wait until Executed block height reached the curent LikeCoin blockchain height (can be found here: https://likecoin.bigdipper.live/blocks). The process might take 7+ days. You can also track your current block height using this link: http://{YOUR_NODES_IP}:26657/status.
```
docker-compose logs --tail="20"
```
(Optional) change your validator fee in staking.sh, then save the file with Ctrl+X, Y, Enter.
```
nano ./scripts/init.sh
```
11. Send some LIKE tokens to your wallet, you can get them from exchange - Digifinex or Liquid - or from https://liker.social/ where you get tokens for likes from other users). You need these tokens to pay fees and delegate to your validator.
12. Once you node is synced, you are ready to create a validator. Enter your node moniker and the amount of tokens you want to delegate to your validator.
```
./scripts/staking.sh
```
13. Track your node on this page: https://likecoin.bigdipper.live/validators.
