# Monero's Consensus Rules

## Introduction

This document separates rules by hardforks, unless otherwise stated rules in previous hardforks will apply to later
hardforks.

## Definitions

canonical scalar
: a scalar that has been reduced mod l

canonical point
: a point which y coordinate is reduced mod p and the point is not -0

torsion free point
: a point in the prime-order subgroup.

## Genesis

On first start, if the blockchain is empty, the Monero node will add a hardcoded genesis block to the blockchain [^1].
The fields of the block are different for each Monero network.

## Mainnet Genesis[^2]

```
{
    header: {
        major_version: 1,
        minor_version: 0,
        timestamp: 0,
        previous: [0; 32],
        nonce: 10000
        },
    miner_tx: "013c01ff0001ffffffffffff03029b2e4c0281c0b02e7c53291a94d1d0cbff8883f8024f5142ee494ffbbd08807121017767aafcde9be00dcfd098715ebcf7f410daebc582fda69d24a28e9d0bc890d1",
    txs: [],
}
```

## Testnet Genesis[^3]

```
{
    header: {
        major_version: 1,
        minor_version: 0,
        timestamp: 0,
        previous: [0; 32],
        nonce: 10001
        },
    miner_tx: "013c01ff0001ffffffffffff03029b2e4c0281c0b02e7c53291a94d1d0cbff8883f8024f5142ee494ffbbd08807121017767aafcde9be00dcfd098715ebcf7f410daebc582fda69d24a28e9d0bc890d1",
    txs: [],
}
```

## Stagenet Genesis[^4]

```
{
    header: {
        major_version: 1,
        minor_version: 0,
        timestamp: 0,
        previous: [0; 32],
        nonce: 10002
        },
    miner_tx: "013c01ff0001ffffffffffff0302df5d56da0c7d643ddd1ce61901c7bdc5fb1738bfe39fbe69c28a3a7032729c0f2101168d0c4ca86fb55a4cf6a36d31431be1c53a3bd7411bb24e8832410289fa6f3b",
    txs: [],
}
```

[^1]: /src/cryptonote_core/blockchain.cpp#L349
[^2]: The function to generate the genesis block is here: /src/cryptonote_core/cryptonote_tx_utils.cpp#L649
major and minor versions are both set here: /src/cryptonote_config.h#L45-46
The genesis nonce is set here: /src/cryptonote_config.h#L232-L233
The genesis transaction is set here: /src/cryptonote_config.h#L231-L232
[^3]: The only difference between testnet and mainnet is the nonce which for testnet is here: /src/cryptonote_config.h#L273
[^4]: stagenet has a different nonce: /src/cryptonote_config.h#L288 and miner transaction: /src/cryptonote_config.h#L287

## HardForks

Monero has a system in it's codebase for hardforking based on votes, although it has never been used. It works by using
the `minor_verison` as a vote to accept the next fork, it keeps a tally of the last 10080 blocks[^1] (~1 week) and if
the amount of blocks in that window is higher than the threshold for that fork then the hardfork is activated. The
threshold is set per hardfork but the default is 80%[^2].

TODO: explain the functions in depth, although not really necessary it would be good to have.

### Mainnet Hardforks [^3]

| Version | Height  | Threshold | Finalized (timestamp)    |
| ------- | ------- | --------- | ------------------------ |
| 1       | 1       | 0         | Jul 04 2012 (1341378000) |
| 2       | 1009827 | 0         | Sep 20 2015 (1442763710) |
| 3       | 1141317 | 0         | Mar 21 2016 (1458558528) |
| 4       | 1220516 | 0         | Jan 05 2017 (1483574400) |
| 5       | 1288616 | 0         | Mar 14 2017 (1489520158) |
| 6       | 1400000 | 0         | Aug 18 2017 (1503046577) |
| 7       | 1546000 | 0         | Mar 17 2018 (1521303150) |
| 8       | 1685555 | 0         | Sep 02 2018 (1535889547) |
| 9       | 1686275 | 0         | Sep 02 2018 (1535889548) |
| 10      | 1788000 | 0         | Feb 10 2019 (1549792439) |
| 11      | 1788720 | 0         | Feb 15 2019 (1550225678) |
| 12      | 1978433 | 0         | Oct 18 2019 (1571419280) |
| 13      | 2210000 | 0         | Aug 23 2020 (1598180817) |
| 14      | 2210720 | 0         | Aug 24 2020 (1598180818) |
| 15      | 2688888 | 0         | Jun 30 2022 (1656629117) |
| 16      | 2689608 | 0         | Jun 30 2022 (1656629118) |

### Stagenet Hardforks [^4]

TODO

### TestNet Hardforks [^5]

TODO

[^1]: /src/cryptonote_basic/hardfork.h#L51
[^2]: /src/cryptonote_basic/hardfork.h#L52
[^3]: /src/hardforks/hardforks.cpp#L34
[^4]: todo
[^5]: todo

## Version 1
