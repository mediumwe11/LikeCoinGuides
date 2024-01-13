# LikeCoin
Useful commands for LikeCoin chain. Note: 1 LIKE = 1 000 000 000 nanolike.

1. Send tokens to another address (``<destination_address>`` begins with ``like1``).
```
liked tx bank send <key_name> <destination_address> <amount>nanolike \
        --from <key_name> \
        --chain-id likecoin-mainnet-2 \
        --gas-prices 10000nanolike
```
2. Delegate tokens to validator (``<validator_address>`` begins with ``likevaloper1``).
```
liked tx staking delegate <validator_address> <amount>nanolike \
        --from <key_name> \
        --chain-id likecoin-mainnet-2 \
        --gas-prices 10000nanolike
```
3. Redelegate tokens from existing validator (``<existing_validator_address>``) to another validator (``<new_validator_address>``).
```
liked tx staking redelegate <existing_validator_address> <new_validator_address> <amount>nanolike \
        --from <key_name> \
        --chain-id likecoin-mainnet-2 \
        --gas-prices 10000nanolike
```
4. Unbond tokens.
```
liked tx staking unbond <validator_address> <amount>nanolike \
        --from <key_name> \
        --chain-id likecoin-mainnet-2 \
        --gas-prices 10000nanolike
```
5. Withdraw delegation rewards from all validators.
```
liked tx distribution withdraw-all-rewards \
        --from <key_name> \
        --chain-id likecoin-mainnet-2 \
        --gas-prices 10000nanolike
```
6. Withdraw validator rewards and validator commission from your validator.
```
liked tx distribution withdraw-rewards <your_validator_address> --commission \
        --from <key_name> \
        --chain-id likecoin-mainnet-2 \
        --gas-prices 10000nanolike
```
7. Deposit funds to proposal. You can find the ``<proposal_ID>`` in explorer: https://likecoin.bigdipper.live/proposals.
```
liked tx gov deposit <proposal_ID> <amount>nanolike  \
        --from <key_name> \
        --chain-id likecoin-mainnet-2 \
        --gas-prices 10000nanolike
```
8. Vote in proposal. You can find the ``<proposal_ID>`` in explorer: https://likecoin.bigdipper.live/proposals.
```
liked tx gov vote <proposal_ID> <yes/no/no_with_veto/abstain> \
        --from <key_name> \
        --chain-id likecoin-mainnet-2 \
        --gas-prices 10000nanolike
```
9. Unjail your validator.
```
liked tx slashing unjail \
        --from <key_name> \
        --chain-id likecoin-mainnet-2 \
        --gas-prices 10000nanolike
```
10. Edit your validator. ``details``, ``identity`` and ``website`` parameters are optional.
```
liked tx staking edit-validator \
        --from <key_name> \
        --moniker="<moniker>" \
        --details="<details>" \
        --identity=<identity> \
        --website="<website>" \
        --chain-id likecoin-mainnet-2 \
        --gas-prices 10000nanolike
```
11. Query address balance.
```
liked query bank balances <address> \
        --chain-id likecoin-mainnet-2
```
12. Info about other types of commands.
```
liked --help
```
You can verify if your transaction was successful with its hash in explorer: https://bigdipper.live/likecoin/transactions.
