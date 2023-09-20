# Transaction Rules

## Introduction

This chapter does not include miner, coinbase, transactions as they are handled elsewhere, the rules for them are under [blocks](blocks.md)

## Index

1. [Rules That Apply To All Versions](./transactions.md#rules-that-apply-to-all-versions)
2. [Rules Specific to Version 1](./transactions/pre_rct.md)
3. [Rules Specific to Version 2](./transactions/rct.md)

## Rules That Apply To All Versions

## Version

Version 0 is never allowed[^tx-v0].

The max transaction version is 1 up to hard fork 4 then the max is 2[^max-tx-version].

The minimum tx version is 1 up till version 6 then if the [number of mixable inputs](#minimum-decoys)
is 0 the minimum is 2 otherwise 1[^min-tx-version].

### Transaction Size

The size of the `transaction blob` must not be bigger than 1 million bytes[^tx-size-limit].

From v8 the transactions weight must not be bigger than the transaction weight limit.

TODO ^

### No Empty Inputs

The transaction must have at least 1 input[^no-empty-ins].

### Input Type

All inputs must be of type `txin_to_key`[^input-types].

### Output Type

All output public keys must be `canonical points`[^output-key-canonical].

Up to hard-fork 15 outputs must be of type `txout_to_key`, for hard-fork 15 both `txout_to_key` and `txout_to_tagged_key` are allowed, from 16 onwards only
`txout_to_tagged_key` is allowed[^output-types].

For hard-fork 15 although both types are allowed a transactions outputs must all use
the same type[^same-output-type].

## Unique Inputs

From hard-fork 6 all decoys in an input must be unique, this is done by checking that
no `key_offset` after the first is 0[^unique-inputs].

## Unique Key Image

The key image must be unique in a transaction[^key-images-in-tx] and the whole chain [^todo-ki-chain].

## Torsion Free Key Image

The key image must be a canonical prime order point[^torsion-free-keyimage].

## Minimum Decoys

These rules are in effect from hard fork 2; a transactions must have a minimum amount
of decoys, if there are enough outputs to mix with.

First you get the minimum and maximum amount of decoys used in the transaction. Then
you get the total amount of inputs that don't have enough outputs to mix with and the
amount that does have enough to mix with.

To find out if an input has enough outputs on the chain to mix with you simply get
the amount of outputs from the chain with that amount, if the amount of outputs is
less than or equal to the minimum amount of decoys then it's impossible to reach the
minimum amount of decoys[^input-mixable].

Version 2 transactions are always counted as mixable[^v2-ins-mixable].

If the minimum amount of decoys is less than the current minimum then the transaction
is only allowed if the there is at least one input which don't have enough outputs to
mix with. The transaction is also only allowed up to one mixable input if another
input is un-mixable[^tx-without-minimum-decoys].

From hard-fork 12 all inputs must have the same number of decoys.

The minimum amount of decoys:

- hard-fork 1 does not follow these rules
- hard-fork 2 to 5 is 2 decoys (3 ring members)
- hard-fork 6 is 4
- hard-fork 7 is 6
- hard-fork 8 to 14 is 10
- hard-fork 15 and up is 15

Special rules[^min-decoys-special-rules]:

- For hard-fork 15 both 10 and 15 decoys are allowed.
- For hard-fork 8 and 9 the minimum amount of decoys in a transaction must be 10
- For hard-fork 10 to 14 the minimum amount of decoys in a transaction must be no more than 10

## Sorted Inputs

From hard-fork 7 the inputs must be sorted by key image, in ascending lexicographic
order[^sorted-kis].

---

[^tx-v0]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/tx_pool.cpp#L152>

[^max-tx-version]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3418>

[^min-tx-version]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3425>

[^tx-size-limit]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/cryptonote_core.cpp#L791>
and <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_basic/cryptonote_basic_impl.cpp#L78>

[^no-empty-ins]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/cryptonote_core.cpp#L1125>

[^input-types]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_basic/cryptonote_format_utils.cpp#L844>

[^output-key-canonical]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_basic/cryptonote_format_utils.cpp#L865>

[^output-types]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_basic/cryptonote_format_utils.cpp#L960>

[^same-output-type]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_basic/cryptonote_format_utils.cpp#L984>

[^unique-inputs]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/cryptonote_core.cpp#L1309>

[^key-images-in-tx]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/cryptonote_core.cpp#L1297>

[^todo-ki-chain]: TODO

[^torsion-free-keyimage]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/cryptonote_core.cpp#L1324>

[^input-mixable]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3361>

[^v2-ins-mixable]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3352>

[^tx-without-minimum-decoys]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3392>

[^min-decoys-special-rules]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3406-L3410>

[^sorted-kis]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3435>
