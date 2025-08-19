
# Stacks-FunderBase - Grant Funding Protocol (Clarity Smart Contract)

## Overview

This smart contract implements a **grant funding system** on the Stacks blockchain using **SIP-010 compliant fungible tokens**. The contract allows the creation of funding pools, submission and voting on funding proposals, and milestone-based fund disbursements. The system emphasizes **community governance** through voting and enforces **grant limits, quorum, and milestone verification**.

---

## 📜 Features

* **Grant Pool Creation** by contract owner
* **Proposal Submission** by applicants with milestone breakdown
* **Voting System** to approve or reject proposals
* **Quorum & Threshold Enforcement**
* **Milestone Completion Tracking**
* **Secure Token Management** using SIP-010 interface

---

## 🧩 Smart Contract Structure

### Traits

* `ft-trait`: Standard SIP-010 interface for fungible token interactions.

### Data Maps

* `grant-pools`: Tracks each funding pool's metadata.
* `proposals`: Stores grant proposals and their milestones.
* `votes`: Stores individual votes per proposal and voter.
* `vote-tallies`: Keeps a running tally of positive and total votes.

### Data Variables

* `current-pool-id`: Tracks latest pool ID.
* `current-proposal-id`: Tracks latest proposal ID.
* `minimum-grant-amount` / `maximum-grant-amount`: Enforces limits on proposal size.
* `minimum-votes-required`: Minimum number of votes to finalize a proposal.
* `quorum-threshold`: Approval percentage required (e.g., 50%).

---

## 🔐 Access Control

* **Only the contract owner** can create grant pools and finalize proposals.
* **Only proposal applicants** can complete their milestones.

---

## 🛠 Functions

### Public Functions

#### `create-grant-pool(total-amount, token-contract)`

Creates a new grant pool with a specified token and amount. Only callable by contract owner.

#### `submit-proposal(pool-id, requested-amount, milestones)`

Applicants submit proposals with requested funds and milestone breakdown.

#### `vote-on-proposal(proposal-id, in-favor)`

Community members can vote on proposals once.

#### `finalize-proposal(proposal-id)`

Only the pool owner can finalize based on quorum and vote count.

#### `complete-milestone(proposal-id, milestone-index)`

Applicants mark milestones as complete after approval.

---

### Read-Only Functions

#### `get-vote-counts(proposal-id)`

Returns current vote tally for a proposal.

---

## ✅ Validations & Error Handling

Error constants (e.g., `err-owner-only`, `err-insufficient-funds`) are used for:

* Permission checks
* Proposal and pool validation
* Milestone validation
* Vote duplication prevention

---

## 🔁 Proposal Lifecycle

1. **Create Grant Pool** → Owner funds pool with SIP-010 token.
2. **Submit Proposal** → Applicant submits milestones.
3. **Vote** → Community casts votes on proposals.
4. **Finalize** → Owner finalizes proposal based on vote results.
5. **Complete Milestones** → Applicant completes and marks progress.

---

## 📦 Requirements

* A SIP-010 compliant token contract deployed.
* A Clarity-compatible environment (e.g., Clarinet or Stacks testnet/mainnet).

---

## 🧪 Testing Suggestions

* Test with various quorum and minimum vote threshold values.
* Try milestone completion with valid and invalid indices.
* Ensure duplicate votes are not accepted.
* Simulate pool exhaustion and check rejection of oversized proposals.

---

## ⚠️ Limitations

* Milestone funds are not yet disbursed automatically—future functionality could transfer tokens per milestone.
* Only one vote per user per proposal.
* Milestone validation is shallow (checks only index and length, not amount consistency).

---

## ✨ Future Improvements

* Add automatic token transfers upon milestone completion.
* Event logging for milestones and approvals.
* Admin interface or front-end integration.
* Additional roles and permission layers.

---

## 📄 License

This project is open source under the MIT License.

---
