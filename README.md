# Causality of lexically ambiguous phrases

## Description of the dataset

The dataset consists on 2 JSON files:
* `SV.json`: Subject-Verb phrases
* `VO.json`: Verb-Object phrases

### Keys
Each of these files is of the form:

```
{
    phrase_1: {
        "model": array,
        "type": str,
        "A_to_B": float,
        "B_to_A": float,
        "A___B": float
    },
    phrase_2: {
        "model": array,
        "type": str,
        "A_to_B": float,
        "B_to_A": float,
        "A___B": float
    },
    ...
}
```

The keys `phrase_k` is used to extract the contexts of the empirical model. For example `letter_press_admit_bury` will have the following contexts:

1. `(letter, admit)`
2. `(letter, bury)`
3. `(press, admit)`
4. `(press, bury)`

(in this order)

The key `model` is used for denoting the empirical model obtain from AmazonMTurk as follows:
```
[
    [
        P[output=(0,0) | context 1],
        P[output=(0,1) | context 1],
        P[output=(1,0) | context 1],
        P[output=(1,1) | context 1]
    ],
    [
        P[output=(0,0) | context 2],
        P[output=(0,1) | context 2],
        P[output=(1,0) | context 2],
        P[output=(1,1) | context 2]
    ],
    [
        P[output=(0,0) | context 3],
        P[output=(0,1) | context 3],
        P[output=(1,0) | context 3],
        P[output=(1,1) | context 3]
    ],
    [
        P[output=(0,0) | context 4],
        P[output=(0,1) | context 4],
        P[output=(1,0) | context 4],
        P[output=(1,1) | context 4]
    ]
]
```

The key ``type`` stores the levels of ambiguity of the different words (`M` corresponding to words with multiple *meanings* and `S` to words with multiple *senses*). For example in the model `letter_press_admit_bury` with `type: "SMMS"`:
- `letter` has multiple senses (`S`)
- `press` has multiple meanings (`M`)
- `admit` has multiple meanings (`M`)
- `bury` has multiple sense (`S`)

The key `A_to_B` corresponds to the causal fraction associated with the order `A -> B`, e.g. `S_to_V` corresponds to the causal order `S -> V`

Similarly, `B_to_A`corresponds to the causal fraction associated with the order `B -> A`.

Finally, the key `A___B` corresponds to the no-signalling fraction.