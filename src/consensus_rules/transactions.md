# Transaction Rules

## Introduction

This chapter does not include miner, coinbase, transactions as they are handled elsewhere, the rules for them are under [blocks](blocks.md)

## Index

1. [Rules That Apply To All Versions](./transactions.md#rules-that-apply-to-all-versions)
2. [Rules Specific to Version 1](./transactions/ring_signatures.md)

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

---

[^tx-v0]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/tx_pool.cpp#L152>

[^max-tx-version]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3418>

[^min-tx-version]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/blockchain.cpp#L3425>

[^tx-size-limit]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/cryptonote_core.cpp#L791>
and <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_basic/cryptonote_basic_impl.cpp#L78>

[^tx-weight_limit]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/tx_pool.cpp#L117> && <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/tx_pool.cpp#L221>
