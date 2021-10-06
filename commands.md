# LikeCoin
Useful commands for LikeCoin chain. Note: 1 LIKE = 1 000 000 000 nanolike.

0. Before executing any commands you need to enter ``likecoin-chain`` folder:
```
cd likecoin-chain
```
1. Send tokens to another address (``<destination_address>`` begins with ``cosmos1``).
```
docker-compose run --rm liked-command \
   tx bank send validator <destination_address> <amount>nanolike \
        --from validator \
        --chain-id likecoin-mainnet-2 \
        --node tcp://liked-service:26657
```
2. Delegate tokens to validator (``<validator_address>`` begins with ``cosmosvaloper1``).
```
docker-compose run --rm liked-command \
    tx staking delegate <validator_address> <amount>nanolike \
        --from validator \
        --chain-id likecoin-mainnet-2 \
        --node tcp://liked-service:26657
```
3. Redelegate tokens from existing validator (``<existing_validator_address>``) to another validator (``<new_validator_address>``).
```
docker-compose run --rm liked-command \
    tx staking redelegate <existing_validator_address> <new_validator_address> <amount>nanolike \
        --from validator \
        --chain-id likecoin-mainnet-2 \
        --node tcp://liked-service:26657
```
4. Unbond tokens.
```
docker-compose run --rm liked-command \
    tx staking unbond <validator_address> <amount>nanolike \
        --from validator \
        --chain-id likecoin-mainnet-2 \
        --node tcp://liked-service:26657 \
        --fees "300000nanolike"
```
5. Withdraw delegation rewards from all validators.
```
docker-compose run --rm liked-command \
    tx distribution withdraw-all-rewards \
        --from validator \
        --chain-id likecoin-mainnet-2 \
        --node tcp://liked-service:26657
```
6. Withdraw validator rewards and validator commission from your validator.
```
docker-compose run --rm liked-command \
    tx distribution withdraw-rewards <your_validator_address> --commission \
        --from validator \
        --chain-id likecoin-mainnet-2 \
        --node tcp://liked-service:26657
```
7. Vote in proposal. You can find the ``<proposal_ID>`` in explorer: https://likecoin.bigdipper.live/proposals.
```
docker-compose run --rm liked-command \
    tx gov vote <proposal_ID> <yes/no/no_with_veto/abstain> \
        --from validator \
        --chain-id likecoin-mainnet-2 \
        --node tcp://liked-service:26657
```
8. Unjail your validator.
```
docker-compose run --rm liked-command \
   tx slashing unjail \
        --from validator \
        --chain-id likecoin-mainnet-2 \
        --node tcp://liked-service:26657
```
9. Edit your validator. ``details``, ``identity`` and ``website`` parameters are optional.
```
docker-compose run --rm liked-command \
    tx staking edit-validator \
        --from validator \
        --moniker="<moniker>" \
        --details="<details>" \
        --identity=<identity> \
        --website="<website>" \
        --chain-id likecoin-mainnet-2 \
        --node tcp://liked-service:26657
```
10. Info about other types of commands.
```
docker exec -it likechain_liked --help
```
You can verify if your transaction was successful with its hash in explorer: https://likecoin.bigdipper.live/transactions. If you see "Out Of Gas" error, try setting ``--fees`` parameter (as in "Unbond tokens" sample).
