# Consensus Rules

This chapter contains all of Monero's consensus rules, from genesis to now. Some rules
are complex so have been split into there own chapter

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

Chain Height:
the amount of blocks in the chain, this is different to the height of the top block as
blocks start counting at 0.
