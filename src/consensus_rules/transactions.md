# Transaction Rules

## Introduction

This chapter does not include miner, coinbase, transactions as they are handled elsewhere, the rules for them are under [blocks](blocks.md)

## Index

1. [Rules That Apply To All Versions](./transactions.md#rules-that-apply-to-all-versions)
2. [Rules Specific to Version 1](./transactions/pre_rct.md)
3. [Rules Specific to Version 2](./transactions/rct.md)

## Rules That Apply To All Versions

### Transaction Size

The size of the `transaction blob` must not be bigger than 1 million bytes[^tx-size-limit].

### No Empty Inputs

The transaction must have at least 1 input[^no-empty-inputs].

### Input Type

All inputs must be of type `txin_to_key`[^input-types].

### Output Type

All output public keys must be `canonical points`[^output-key-canonical]

[^tx-size-limit]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/cryptonote_core.cpp#L791>
and <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_basic/cryptonote_basic_impl.cpp#L78>

[^no-empty-inputs]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/cryptonote_core.cpp#L1125>

[^input-types]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_basic/cryptonote_format_utils.cpp#L844>

[^output-key-canonical]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_basic/cryptonote_format_utils.cpp#L865>
