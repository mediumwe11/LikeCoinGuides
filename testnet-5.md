# LikeCoin Public Testnet
Instructions on how to set up LikeCoin  Testnet node and create validator. This is my version of official guide (https://docs.like.co/validator/likecoin-chain-node/setup-a-node) with some extra steps which allow you to set up a node in a step-by-step mode.


1. Update and upgrade packages:
```
sudo apt update
sudo apt upgrade --yes
```
2. Install ``make`` and ``git``:
```
sudo apt install make git
```
3. Clone LikeCoin repository from GitHub:
```
cd ~
git clone https://github.com/likecoin/likecoin-chain.git --branch release/v1.x --single-branch
```
4. Fill variables with appropriate data. Replace ``<moniker>`` with your node name:
```
export MONIKER='<moniker>'
export GENESIS_URL='https://raw.githubusercontent.com/likecoin/testnets/master/likecoin-public-testnet-5/genesis.json'
export LIKED_SEED_NODES='7a38dfc59eb43b27cf2cc87b46a43e76aeaaf012@20.205.224.107:26656,11c0d57ae2b37122bd8e7de82a1b92c87bf3d45a@20.24.152.136:26656'
```
5. Execute setup script:
```
cd ~/likecoin-chain
make -C deploy setup-node
```
6. Activate service file and run it:
```
cd ~/likecoin-chain
make -C deploy initialize-systemctl
make -C deploy start-node
```
7. Check your sync status. Wait until you get ``"catching_up": false`` (this might take some time). 
```
curl -s localhost:26657/status
```
8. Optionally, you can also check your service logs:
```
journalctl -u liked.service -f
```
9. Add an operator key. Enter the password with at least 8 characters (you will use it to sign all transactions). **Important**: write mnemonic phrase in a safe place:
```
~/liked keys add <key_name> --keyring-backend file
```
10. Join the LikeCoin Discord server https://discord.gg/likecoin and request token in ``#faucet-testnet`` channel using ``/faucet <address>``
11. Create validator:
```
~/liked tx staking create-validator \
--amount=500000000000nanoekil \
--pubkey=$(~/liked tendermint show-validator) \
--moniker=<moniker> \
--commission-rate="0.10" \
--commission-max-rate="0.50" \
--commission-max-change-rate="0.05" \
--min-self-delegation="500000000000" \
--chain-id="likecoin-public-testnet-5" \
--from=<key_name> \
--keyring-backend=file \
--gas 200000 \
--fees 1000000000nanoekil
```
12. Make sure you appeared in Testnet Explorer: https://likecoin-public-testnet-5.netlify.app/validators
