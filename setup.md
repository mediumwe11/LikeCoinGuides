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
4. Install Docker Compose (version >= 1.28 is required):
```
sudo curl -L https://github.com/docker/compose/releases/download/1.29.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
5. Clone LikeCoin project:
```
git clone https://github.com/likecoin/likecoin-chain --branch fotan-1 --single-branch
```
6. Go to ``likecoin-chain`` folder and run ``build.sh`` script:
```
cd likecoin-chain
./scripts/build.sh
```
7. Prepare ``docker-compose.yml`` and ``.env`` files for edit:
```
cp docker-compose.yml.template docker-compose.yml
cp .env.template .env
```
8. Open and modify ``.env`` file - follow instructions inside the file and the variables below:
```
LIKECOIN_MONIKER="<change this for your node's name>"
LIKECOIN_DOCKER_IMAGE="likecoin/likecoin-chain:fotan-1"
LIKECOIN_CHAIN_ID="likecoin-mainnet-2"
LIKECOIN_GENESIS_URL="https://gist.githubusercontent.com/williamchong/de1bdf2b2a8f3bce50a4b5e46af26959/raw/4e21bff586771c849d22e1916bcb88c6463fbaa0/genesis.json"
LIKECOIN_SEED_NODES="913bd0f4bea4ef512ffba39ab90eae84c1420862@34.82.131.35:26656,e44a2165ac573f84151671b092aa4936ac305e2a@nnkken.dev:26656"
```
9.  Create ``.liked`` directories, with node config and keys initialized.
```
docker-compose run --rm init
```
10. Add an operator key. Enter the password with at least 8 characters (you will use it to sign all transactions). **Important**: write  mnemonic phrase in a safe place:
```
docker-compose run --rm liked-command keys add validator
```
11. Create and run the Docker containers in background
```
docker-compose up -d
```
12. Check logs and wait until Executed block height reached the curent LikeCoin blockchain height (can be found here: https://likecoin.bigdipper.live/blocks). The process might take some time. You can also track your current block height using this link: http://{YOUR_NODES_IP}:26657/status.
```
docker-compose logs --tail="20"
```
13. Send some LIKE tokens to your wallet, you can get them from exchange - Digifinex or Liquid - or from https://liker.social/ where you get tokens for likes from other users). You need these tokens to pay fees and delegate to your validator.
14. Once you node is synced, you are ready to create a validator. Enter your node moniker and the amount of tokens you want to delegate to your validator as well as your commision rate. Optionally, you can add extra parameters like ``--identity <IDENTITY>`` and ``--website <WEBSITE>``.
```
docker-compose run --rm create-validator \
    --amount <AMOUNT> \
    --details <DETAILS> \
    --commission-rate <COMMISSION_RATE>
```
15. Track your node on this page: https://likecoin.bigdipper.live/validators.
