# BB84 Quantum Cryptography

A Qiskit simulation of BB84 (Bennett and Brassard, 1984), the first quantum cryptography protocol. Alice sends single qubits to Bob to build a shared secret key, and an eavesdropper (eve) gets caught by the errors she introduces.

## How it works

- **Sending:** for each round, Alice picks a random bit and a random basis, then sends Bob a qubit encoding that bit. In the Z basis (the computational basis), 0 is ket 0 and 1 is ket 1. In the X basis (the Hadamard basis), 0 is ket + and 1 is ket −.
- **Measuring:** Bob measures each one in a random basis. Same basis as Alice gives her exact bit. A different basis gives a random result.
- **Key:** they publicly compare bases, never bits, and keep the rounds where the bases matched.
- **Check:** they compare a sample of key bits. Eve has to guess bases to measure, and wrong guesses corrupt the qubits, causing about 25% errors. Above about 11%, they abort.

## Results

4,000 rounds per run. Numbers vary slightly between runs.

| | Key error rate | Verdict |
|---|---|---|
| No eavesdropper | 0% | keep |
| Eve intercepting | ~25% | abort |

## Run it

```bash
pip install qiskit qiskit-aer matplotlib jupyter
jupyter notebook bb84_key_distribution.ipynb
```

## Notes

- BB84 secures how the key is shared. Messages are then encrypted normally with that key.
- Real systems send single photons over noisy channels, so the abort threshold allows some error.
- This is a simplified simulation for learning.

Made by Sultana with [Qiskit](https://www.ibm.com/quantum/qiskit).
