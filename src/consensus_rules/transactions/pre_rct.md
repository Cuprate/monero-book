# Transaction Version 1 Rules

## Fee

Transactions must have a higher amount in than out[^more-in-than-out].

## Inputs And Outputs Must Not Overflow

The inputs when summed must not overflow a u64 and the outputs when summed must no either[^amount-overflow].

## Output Amount

All outputs must have an amount bigger than 0[^zero-output].


[^more-in-than-out]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_core/cryptonote_core.cpp#L1163> 

[^amount-overflow]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_basic/cryptonote_format_utils.cpp#L871>

[^zero-output]: <https://github.com/monero-project/monero/blob/eac1b86bb2818ac552457380c9dd421fb8935e5b/src/cryptonote_basic/cryptonote_format_utils.cpp#L862>
