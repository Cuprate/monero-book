# Hard Forks

Monero makes use of hard-forks to update it's protocol. Although it has never been used, Monero has a system in it's codebase to 
allow voting for activation of a hard-fork[^hardfork-class]. It works by using the blocks `minor version` field as a voting field, 
when enough blocks vote for a hard fork the fork is activated.

Because Monero has never used hard fork voting, you don't *need* to implement it but as it's included in the codebase, an explanation 
is included here.

## Blocks version and vote

Monero uses the blocks `major version` field as an indicator of hard-fork and the `minor version` field as an indicator of the blocks 
vote. A minor version of 0 is treated as a vote for 1 as legacy blocks use to just set this field to 0[^minor-v-0].

The blocks vote must be greater than or equal to the version, a vote higher than the maximum known hard-fork is interpreted
as a vote for the latest hard-fork[^minor-v-too-large]. So if a block is at V2 then the vote must be V2 or higher.

## Accepting a fork

When a hard-fork is added to Monero's protocol it must specify a `threshold`, a number between 0 and 100, this is the proportion of
blocks in the window that must vote for this fork (or a later one) for it to activate. For all current forks the threshold is 0 meaning
that no votes are needed for the fork to activate.

Monero keeps track of a week (10080 blocks) worth of votes[^window-size], when a new block is added Monero works backwards through the 
list of hard-forks (latest to oldest) tallying the votes and checking if the number of votes is bigger than the amount needed[^accepting-hfs], 
votes for later hardforks are also votes for previous hard-forks. The amount needed is calculated:

\\( amountNeeded = \frac{windowSize * threshold + 99}{100} \\)

If the amount of votes is greater than or equal to the amount needed and the current blockchain height is greater than or equal to the hard-fork 
height the HF is activated[^accepting-hfs].

## Mainnet Hard-Forks [^mainnet-hfs]


| Version | Height      | Threshold | Finalized (timestamp)    |
|---------|-------------|-----------|--------------------------|
| 1       | 0[^v1-at-0] | 0         | Jul 04 2012 (1341378000) |
| 2       | 1009827     | 0         | Sep 20 2015 (1442763710) |
| 3       | 1141317     | 0         | Mar 21 2016 (1458558528) |
| 4       | 1220516     | 0         | Jan 05 2017 (1483574400) |
| 5       | 1288616     | 0         | Mar 14 2017 (1489520158) |
| 6       | 1400000     | 0         | Aug 18 2017 (1503046577) |
| 7       | 1546000     | 0         | Mar 17 2018 (1521303150) |
| 8       | 1685555     | 0         | Sep 02 2018 (1535889547) |
| 9       | 1686275     | 0         | Sep 02 2018 (1535889548) |
| 10      | 1788000     | 0         | Feb 10 2019 (1549792439) |
| 11      | 1788720     | 0         | Feb 15 2019 (1550225678) |
| 12      | 1978433     | 0         | Oct 18 2019 (1571419280) |
| 13      | 2210000     | 0         | Aug 23 2020 (1598180817) |
| 14      | 2210720     | 0         | Aug 24 2020 (1598180818) |
| 15      | 2688888     | 0         | Jun 30 2022 (1656629117) |
| 16      | 2689608     | 0         | Jun 30 2022 (1656629118) |

## Testnet Hard-Forks [^testnet-hfs]

TODO

## Stagenet Hard-Forks [^stagenet-hfs]

TODO

---

[^hardfork-class]: /src/cryptonote_basic/hardfork.h

[^minor-v-0]: /src/cryptonote_basic/hardfork.cpp#L47

[^minor-v-too-large]: /src/cryptonote_basic/hardfork.cpp#L99

[^window-size]: /src/cryptonote_basic/hardfork.h#L51

[^accepting-hfs]: /src/cryptonote_basic/hardfork.cpp#L311

[^mainnet-hfs]: /src/hardforks/hardforks.cpp#L34

[^testnet-hfs]:

[^stagenet-hfs]:

[^v1-at-0]: Monero C++ sets this to 1 even though the [genesis block](genesis_block.md) has a major version of 1.
