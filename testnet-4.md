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
export GENESIS_URL='https://raw.githubusercontent.com/oursky/testnets/master/likecoin-public-testnet-4/genesis.json'
export LIKED_SEED_NODES='4f5ebbf796c5f2dc928d88f212e92671a7e224ab@20.205.224.107:26656,c45c18de6178d0face7e684e064c6022b2de0f16@20.24.152.136:26656'
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
7. Check your sync status and service logs:
```
curl -s localhost:26657/status
journalctl -u liked.service -f
```
