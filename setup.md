# LikeCoin
Instructions on how to set up LikeCoin node and create validator. This is my version of official guide (https://docs.like.co/validator/likecoin-chain-node/setup-a-node) with some extra steps which allow you to set up a node in a step-by-step mode.

1. Update and upgrade packages:
```
sudo apt update
sudo apt upgrade --yes
```
2. Install git, curl and make:
```
sudo apt install git curl make --yes
```
3. Clone LikeCoin project:
```
git clone https://github.com/likecoin/likecoin-chain.git --branch release/v1.x --single-branch
```
4. Set up variables. Replace ``<moniker>`` with your validator moniker:
```
export MONIKER='<moniker>'
export GENESIS_URL='https://raw.githubusercontent.com/likecoin/mainnet/master/genesis.json'
export LIKED_SEED_NODES='913bd0f4bea4ef512ffba39ab90eae84c1420862@34.82.131.35:26656,e44a2165ac573f84151671b092aa4936ac305e2a@nnkken.dev:26656'
export LIKED_VERSION='1.2.0'
cd ~/likecoin-chain
make -C deploy setup-node
```
5. Go to ``likecoin-chain``, create ``liked`` service and start it:
```
cd ~/likecoin-chain
make -C deploy initialize-systemctl
make -C deploy start-node
```
6. Check logs and wait until Executed block height reached the curent LikeCoin blockchain height (can be found here: https://likecoin.bigdipper.live/blocks). The process might take some time.
```
journalctl -u liked.service -f
```
You can also track your current block height using this command:
```
curl -s localhost:26657/status
``` 
7. Add an operator key. Enter the password with at least 8 characters (you will use it to sign all transactions). **Important**: write  mnemonic phrase in a safe place:
```
~/liked keys add <key_name> --keyring-backend file
```
8. Send some LIKE tokens to your wallet, you can get them from exchange - Osmosis, Digifinex, or Liquid - or from https://liker.social/ where you get tokens for likes from other users). You need these tokens to pay fees and delegate to your validator.
9. Once you node is synced, you are ready to create a validator. Enter your node moniker and the amount of tokens you want to delegate to your validator as well as your commision rate. Optionally, you can add extra parameters like ``--identity <IDENTITY>`` and ``--website <WEBSITE>``.
```
~/liked tx staking create-validator \
--amount=<amount>nanolike \
--pubkey=$(~/liked tendermint show-validator) \
--moniker=$MONIKER \
--commission-rate="0.10" \
--commission-max-rate="0.50" \
--commission-max-change-rate="0.05" \
--min-self-delegation="<amount>" \
--chain-id="likecoin-mainnet-2" \
--from=<key_name> \
--keyring-backend=file \
--gas-prices 10nanolike
```
10. Track your node on this page: https://likecoin.bigdipper.live/validators.
