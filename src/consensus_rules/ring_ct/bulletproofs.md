# Bulletproofs Rules

## Introduction

These rules apply to all ringCT types that use bulletproofs.

## Rules

### L & R Length

The Length of the L & R fields must be the same, they must both be greater than or equal to 6 and less than or equal to \\( 6 + log_2(maxOutputs) \\), 
maxOutputs being 16.[^L-R-Size]

### Number Of Bulletproofs

There must only be one bulletproof in a transaction.[^one-bulletproof]

### Max Outputs

The amount of outputs in the transaction must not be more than \\(2^{(len(L) - 6)} \\) and 2 * NumbOutputs must be more than \\(2^{(len(L) - 6)}\\) [^max-outputs]

### At Least One Output

There must be at least one element of V, which is constructed from the outPKs which must have the same number of elements as the outputs.[^one-out]

### Canonical Encoding

`taux`, `mu`, `a`, `b`, `t` must all be fully reduced scalars[^canonical-scalars].

All the elements of `V`, `L`, `R` and `A`, `T1`, `T2` and `S` must all be valid, canonically encoded points.[^canonical-points]

### The Bulletproof Must Be Valid

The bulletproof must pass verification. [^bulletproof-valid] 

---

[^L-R-Size]: <https://github.com/monero-project/monero/blob/master/src/ringct/rctTypes.cpp#L300-L304>

[^one-bulletproof]: <https://github.com/monero-project/monero/blob/ac02af92867590ca80b2779a7bbeafa99ff94dcb/src/cryptonote_basic/cryptonote_format_utils.cpp#L197>

[^max-outputs]: <https://github.com/monero-project/monero/blob/ac02af92867590ca80b2779a7bbeafa99ff94dcb/src/ringct/rctTypes.cpp#L261-L262>

[^one-out]: <https://github.com/monero-project/monero/blob/ac02af92867590ca80b2779a7bbeafa99ff94dcb/src/ringct/bulletproofs.cc#L839>

[^canonical-scalars]: <https://github.com/monero-project/monero/blob/ac02af92867590ca80b2779a7bbeafa99ff94dcb/src/ringct/bulletproofs.cc#L833-L837>

[^canonical-points]: <https://github.com/monero-project/monero/blob/ac02af92867590ca80b2779a7bbeafa99ff94dcb/src/ringct/bulletproofs.cc#L919-L930>

[^bulletproof-valid]: <https://github.com/monero-project/monero/blob/ac02af92867590ca80b2779a7bbeafa99ff94dcb/src/ringct/bulletproofs.cc#L810>
