# Decoys

Every non-miner transaction input must specify a `ring` of past outputs of which one is the true spend. Currently Monero restricts
the size of the ring to 16 (with some exceptions) but this was not always the case.

## Minimum Amount Of Decoys

This is the number of decoys an input must at least have.

> There are exceptions to this being the minimum decoy size for all transactions.

| Hard-Fork | Minimum Decoys[^min-decoys] |
| --------- | --------------------------- |
| 1         | N/A                         |
| 2 to 5    | 2                           |
| 6         | 4                           |
| 7         | 6                           |
| 8 to 14   | 10                          |
| 15+       | 15                          |

## Minimum And Maximum Decoys Used

To check a transaction inputs `ring` size we must first get the minimum and maximum number of `decoys`
used in the transactions inputs[^min-max-decoys].

So if this was our transactions:

| Input     | 1  | 2 | 3  |
| --------- | -- | - | -- |
| Ring size | 12 | 8 | 16 |

The minium and maximum amount of decoys would be 7 and 15 respectively.

## Mixable And UnMixable Inputs

A mixable input is one that has enough outputs on the chain with the same amount to be able to build a ring with the
minimum amount of decoys needed.

A ringCT input, aka an output with 0 amount, is always considered mixable[^0-amt-mixable].

For other inputs you first get the amount of outputs on chain with that amount and check if thats less than or equal
to the [minimum amount of decoys](#minimum-amount-of-decoys) if it is then the input is un-mixable otherwise it is
mixable[^check-mixability].

---

[^min-decoys]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3345>

[^min-max-decoys]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3369-L3373>

[^0-amt-mixable]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3357>

[^check-mixability]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3361-L3367>
