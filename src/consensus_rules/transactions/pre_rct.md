# Transaction Version 1 Rules

## Fee

Transactions must have a higher amount in than out[^more-in-than-out].

## Inputs And Outputs Must Not Overflow

The inputs when summed must not overflow a u64 and the outputs when summed must no either[^amount-overflow].

## Output Amount

All outputs must have an amount bigger than 0[^zero-output].

## Amount Of Signatures In Ring

For a ring signature at a certain index, the input at that same index must have the same amount of decoys as the ring signature has signatures[^amt-of-sigs].

---

From hard-fork 2 version 1 transaction output amounts must be validly decomposed[^decomposed-amounts]. A valid decomposed amount is an amount contained in [this table](https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_basic/cryptonote_format_utils.cpp#L52)

[^more-in-than-out]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/cryptonote_core.cpp#L1163>

[^amount-overflow]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_basic/cryptonote_format_utils.cpp#L871>

[^zero-output]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_basic/cryptonote_format_utils.cpp#L862>

[^decomposed-amounts]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3048>

[^amt-of-sigs]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3485>
and <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3999>
