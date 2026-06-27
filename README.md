# Smart Contract Validation with Merkle Trees

Clause-level contract validation using Merkle tree cryptography — the same integrity mechanism used in blockchain smart contract systems, applied to legal agreements.

<img alt="Example: warranty clause change" width="725" src="https://github.com/user-attachments/assets/4ec71e8e-8749-4c1c-9e02-f90130cbfd73" />

---

## What It Does

Paste two versions of a contract. The app hashes each clause independently, builds a Merkle tree for each version, and compares their roots. If the roots differ, it drills down to show exactly which clauses changed — without requiring you to read the full document.

Blockchains use Merkle trees to verify transaction integrity without storing full data on-chain. This project applies the same principle to contracts: instead of storing entire documents, you store only the Merkle root. Any modification — even a single word — produces a completely different root, making unauthorized edits immediately detectable.

> **Example:** Changing *"Party A will pay $500"* to *"Party A will pay $550"* flips the root hash entirely, making the edit immediately visible.

---

## 🎯 Key Use Cases

* **Tamper-Evident Storage:** Store a single 32-byte Merkle root on a blockchain or database to permanently lock and prove the integrity of a 100-page contract.
* **Privacy-Preserving Audits:** Prove a specific clause exists in a contract (using a Merkle proof) to a third party without revealing the rest of the sensitive agreement.
* **Rapid Multi-Party Review:** Instantly pinpoint where unauthorized "stealth" edits were made during redlining processes without manual comparison.

---

## Features

* **Root comparison** — Match or mismatch detected instantly via a single root hash comparison.
* **Clause-level diffing** — Pinpoints which lines changed and displays both versions side by side.
* **Merkle proof generation** — Verify an individual clause belongs to a contract without exposing the rest.
* **Interactive tree visualization** — See the full Merkle tree structure and hash propagation for each contract version.

<img alt="Example with duplicate hash" src="https://github.com/user-attachments/assets/28cd7623-fd0e-41a8-a35c-aadef687d38a" width="725px" />

---

## How It Works

1. **Hash Clauses:** Each non-empty line is treated as a clause and hashed using SHA-256.
2. **Build Tree:** Hashes are combined pairwise up the tree until a single root hash remains.
3. **Detect Deltas:** Comparing roots tells you instantly if contracts match; if not, clause hashes are compared positionally to isolate the exact divergence.
4. **Generate Proofs:** A Merkle proof lets you verify a single clause against the root without revealing other clauses — ideal for privacy-focused validation.

---

## Tech Stack

* **Python** — Core cryptographic Merkle tree logic ([contractVerification.py](contractVerification.py))
* **Streamlit** — Clean, interactive user interface ([app.py](app.py))
* **Graphviz** — Dynamic tree visualization and mapping

---

## Quick Start

### Prerequisites
Ensure you have Python installed, along with [Graphviz](https://graphviz.org/download/) on your system for the tree rendering features.

### Installation
```bash
# Clone the repository and navigate to the project directory
git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
cd your-repo-name

# Install dependencies
pip install -r requirements.txt

# Run the application
streamlit run app.py
