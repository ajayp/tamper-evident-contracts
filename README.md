# Smart Contract Validation with Merkle Trees

Clause-level contract validation using Merkle tree cryptography — the same integrity mechanism used in blockchain smart contract systems, applied to legal agreements.

<img alt="Example: warranty clause change" width="725" src="https://github.com/user-attachments/assets/4ec71e8e-8749-4c1c-9e02-f90130cbfd73" />

---

## What It Does

Paste two versions of a contract. The app hashes each clause independently, builds a Merkle tree for each version, and compares their roots. If the roots differ, it drills down to show exactly which clauses changed — without requiring you to read the full document.

Blockchains use Merkle trees to verify transaction integrity without storing full data on-chain. This project applies the same principle to contracts: instead of storing entire documents, you store only the Merkle root. Any modification — even a single word — produces a completely different root, making unauthorized edits immediately detectable.

**Example:** Changing *"Party A will pay $500"* to *"Party A will pay $550"* flips the root hash entirely, making the edit immediately visible.

---

## Features

- **Root comparison** — match or mismatch detected in one hash comparison
- **Clause-level diffing** — pinpoints which lines changed and shows both versions side by side
- **Merkle proof generation** — verify an individual clause belongs to a contract without exposing the rest
- **Interactive tree visualization** — see the full Merkle tree structure for each contract version

<img alt="Example with duplicate hash" src="https://github.com/user-attachments/assets/28cd7623-fd0e-41a8-a35c-aadef687d38a" width="725px" />

---

## How It Works

1. Each non-empty line is treated as a clause and hashed with SHA-256.
2. Hashes are combined pairwise up the tree until a single root hash remains.
3. Comparing roots tells you instantly if contracts match; if not, clause hashes are compared positionally to find the delta.
4. A Merkle proof lets you verify a single clause against the root without revealing other clauses — useful for privacy-preserving audits.

---

## Tech Stack

- **Python** — core Merkle tree logic ([contractVerification.py](contractVerification.py))
- **Streamlit** — interactive UI ([app.py](app.py))
- **Graphviz** — tree visualization

---

## Quick Start

```bash
pip install -r requirements.txt
streamlit run app.py
```

Browse to http://localhost:8501. Use the sidebar to load sample contract pairs or paste your own.
