# Consensus Rules

This chapter contains all of Monero's consensus rules, from genesis to now, split by hard fork. Unless otherwise stated rules in earlier
hard forks apply to later hard forks.

All references, unless otherwise stated, will be as of commit: eac1b86bb2818ac552457380c9dd421fb8935e5b on the release-v0.18 branch.

## Definitions

Canonical Scalar:
a scalar which is fully reduced mod l.

Canonical Point:
a point with y coordinate fully reduced mod p and not the negative identity.

Prime Order Point:
a point in the prime subgroup.

POW Hash:
the hash calculated by using the active proof of work function.

Block Hash:
the keccak hash of the block.

Transaction Blob:
the raw bytes of a serialized transaction.
