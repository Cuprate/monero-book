# Transaction Rules

## Introduction

This chapter does not include miner, coinbase, transactions as they are handled elsewhere, the rules for them are under [blocks](blocks.md)

## Index

1. [Rules That Apply To All Versions](./transactions.md#rules-that-apply-to-all-versions)
2. [Rules Specific to Version 1](./transactions/pre_rct.md)

## Rules That Apply To All Versions

### Version

Version 0 is never allowed[^tx-v0].

The max transaction version is 1 up to hard fork 4 then the max is 2[^max-tx-version].

The minimum tx version is 1 up till version 6 then if the [number of un-mixable inputs](#minimum-decoys)
is 0 the minimum is 2 otherwise 1[^min-tx-version] so a version 1 transaction is allowed if the amount
it's spending does not have enough outputs with the same amount to mix with.

### Transaction Size

The size of the `transaction blob` must not be bigger than 1 million bytes[^tx-size-limit].

From v8 the transactions _weight_ must not be bigger than half of the [block penalty free zone](./blocks/weights.md#penalty-free-zone) minus 600[^tx-weight_limit].

### No Empty Inputs

The transaction must have at least 1 input[^no-empty-ins].

### No Empty decoys

All inputs must have decoys[^empty-decoys].

### Input Type

All inputs must be of type `txin_to_key`[^input-types].

### Inputs And Outputs Must Not Overflow

The inputs when summed must not overflow a u64 and the outputs when summed must not either[^amount-overflow].

### Output Keys Canonical

All output public keys must be `canonical points`[^output-key-canonical].

> This was added as a rule in hard-fork 4 but that check is redundant as it was done before that.
> So how did invalid keys get on the chain? [miner txs](./blocks/miner_tx.md).

### Output Type

The output type allowed depends on the hard-fork[^output-types]:

| hard-fork  | output type                          |
| ---------- | ------------------------------------ |
| 1 to 14    | txout_to_key                         |
| 15         | txout_to_key and txout_to_tagged_key |
| 16 onwards | txout_to_tagged_key                  |

> For hard-fork 15 both are allowed but the transactions outputs must all be the same type[^same-output-type].

### Unique Ring Members

From hard-fork 6 all ring members in an input must be unique, this is done by checking that
no `key_offset` after the first is 0[^unique-ring].

### Unique Key Image

The key image must be unique in a transaction[^key-images-in-tx] and the whole chain [^key-images-in-chain].

### Torsion Free Key Image

The key image must be a canonical prime order point[^torsion-free-keyimage].

### Minimum Decoys

These rules are in effect from hard fork 2.

First you get the [minimum number of decoys used in the transaction](./transactions/decoys.md#minimum-and-maximum-decoys-used).

Then you get the [amount of mixable and un-mixable inputs](./transactions/decoys.md#mixable-and-unmixable-inputs).

Now get the [default minimum decoys allowed for the current hard-fork](./transactions/decoys.md#default-minimum-decoys).

If the minimum amount of decoys used in the transaction is less than the default minimum decoys allowed then the transaction is only
allowed if there is at least one input which is un-mixable[^tx-without-minimum-decoys].

If there is an un-mixable then the transaction is not allowed to have more than 1 mixable input as well.

Special rules[^min-decoys-special-rules]:

- For hard-fork 15 both 10 and 15 decoys are allowed.
- From hard-fork 8 upwards the minimum amount of decoys used in a transaction must be equal to the minimum allowed.

### Equal Number Of Decoys

From hard-fork 12 all inputs must have the same number of decoys[^equal-decoys].

### Sorted Inputs

From hard-fork 7 the inputs must be sorted by key image, in descending lexicographic order[^sorted-kis].

### The Output Must Exist

The output a transaction references must exist in the chain[^output-must-exist].

### The Output Must Not Be Locked

The outputs unlock time must have passed, see the [chapter on unlock time](./transactions/unlock_time.md).

### 10 Block Lock

From hard-fork 12 all ring members must be at least 10 blocks old[^minimum-out-age].

### 2 Outputs

From hard-fork 12 version 2 transactions must have 2 outputs[^minimum-2-outs].

---

[^tx-v0]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/tx_pool.cpp#L152>

[^max-tx-version]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3418>

[^min-tx-version]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3425>

[^tx-size-limit]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/cryptonote_core.cpp#L791>
and <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_basic/cryptonote_basic_impl.cpp#L78>

[^tx-weight_limit]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/tx_pool.cpp#L117> && <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/tx_pool.cpp#L221>

[^no-empty-ins]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/cryptonote_core.cpp#L1125>

[^empty-decoys]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3473>

[^input-types]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_basic/cryptonote_format_utils.cpp#L844>

[^amount-overflow]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_basic/cryptonote_format_utils.cpp#L871>

[^output-key-canonical]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_basic/cryptonote_format_utils.cpp#L865>

[^output-types]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_basic/cryptonote_format_utils.cpp#L960>

[^same-output-type]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_basic/cryptonote_format_utils.cpp#L984>

[^unique-ring]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/cryptonote_core.cpp#L1309>

[^key-images-in-tx]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/cryptonote_core.cpp#L1297>

[^key-images-in-chain]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3475>

[^torsion-free-keyimage]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/cryptonote_core.cpp#L1324>

[^tx-without-minimum-decoys]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3392>

[^min-decoys-special-rules]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3406-L3410>

[^equal-decoys]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3378>

[^sorted-kis]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3435>

[^output-must-exist]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3995>

[^minimum-out-age]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3533>

[^minimum-2-outs]: <https://github.com/monero-project/monero/blob/ac02af92867590ca80b2779a7bbeafa99ff94dcb/src/cryptonote_core/blockchain.cpp#L3324>
