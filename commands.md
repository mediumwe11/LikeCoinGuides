# LikeCoin
Useful commands for LikeCoin chain. Note: 1 LIKE = 1 000 000 000 nanolike.

1. Send tokens to another address (``<destionation_address>`` begins with ``cosmos1``).
```
docker exec -it likechain_liked \
    likecli --home /likechain/.likecli tx send validator <destionation_address> <amount>nanolike \
        --from validator \
        --chain-id $(grep chain_id "/root/likecoin-chain/.liked/config/genesis.json" | sed 's/ *"chain_id": *"\(.*\)"/\1/g' | sed 's/,$//g') \
        --gas "auto"
```
2. Delegate tokens to validator (``<validator_address>`` begins with ``cosmosvaloper1``).
```
docker exec -it likechain_liked \
    likecli --home /likechain/.likecli tx staking delegate <validator_address> <amount>nanolike \
        --from validator \
        --chain-id $(grep chain_id "/root/likecoin-chain/.liked/config/genesis.json" | sed 's/ *"chain_id": *"\(.*\)"/\1/g' | sed 's/,$//g') \
        --gas "auto"
```
3. Redelegate tokens from existing validator (``<existing_validator_address>``) to another validator (``<new_validator_address>``).
```
docker exec -it likechain_liked \
    likecli --home /likechain/.likecli tx staking redelegate <existing_validator_address> <new_validator_address> <amount>nanolike \
        --from validator \
        --chain-id $(grep chain_id "/root/likecoin-chain/.liked/config/genesis.json" | sed 's/ *"chain_id": *"\(.*\)"/\1/g' | sed 's/,$//g') \
        --gas "auto"
```
4. Unbond tokens.
```
docker exec -it likechain_liked \
    likecli --home /likechain/.likecli tx staking unbond <validator_address> <amount>nanolike \
        --from validator \
        --chain-id $(grep chain_id "/root/likecoin-chain/.liked/config/genesis.json" | sed 's/ *"chain_id": *"\(.*\)"/\1/g' | sed 's/,$//g') \
        --fees "300000nanolike" \
        --gas "auto"
```
5. Withdraw delegation rewards from all validators.
```
docker exec -it likechain_liked \
    likecli --home /likechain/.likecli tx distribution withdraw-all-rewards \
        --from validator \
        --chain-id $(grep chain_id "/root/likecoin-chain/.liked/config/genesis.json" | sed 's/ *"chain_id": *"\(.*\)"/\1/g' | sed 's/,$//g') \
        --gas "auto"
```
6. Withdraw validator rewards and validator commission from your validator.
```
docker exec -it likechain_liked \
    likecli --home /likechain/.likecli tx distribution withdraw-rewards <your_validator_address> --commission \
        --from validator \
        --chain-id $(grep chain_id "/root/likecoin-chain/.liked/config/genesis.json" | sed 's/ *"chain_id": *"\(.*\)"/\1/g' | sed 's/,$//g') \
        --gas "auto"
```
7. Vote in proposal. You can find the ``<proposal_ID>`` in explorer: https://likecoin.bigdipper.live/proposals.
```
docker exec -it likechain_liked \
    likecli --home /likechain/.likecli tx gov vote <proposal_ID> <yes/no/no_with_veto/abstain> \
        --from validator \
        --chain-id $(grep chain_id "/root/likecoin-chain/.liked/config/genesis.json" | sed 's/ *"chain_id": *"\(.*\)"/\1/g' | sed 's/,$//g') \
        --gas "auto"
```
8. Unjail your validator.
```
docker exec -it likechain_liked \
    likecli --home /likechain/.likecli tx slashing unjail \
        --from validator \
        --chain-id $(grep chain_id "/root/likecoin-chain/.liked/config/genesis.json" | sed 's/ *"chain_id": *"\(.*\)"/\1/g' | sed 's/,$//g') \
        --gas "auto"
```
9. Info about other types of commands.
```
docker exec -it likechain_liked \
    likecli --home /likechain/.likecli --help
```
You can verify if your transaction was successful with its hash in explorer: https://likecoin.bigdipper.live/transactions. If you see "Out Of Gas" error, try setting ``--fees`` parameter (as in "Unbond tokens" sample).
