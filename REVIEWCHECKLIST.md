# Contract Review Notes — <ContractName> (Cadence)

> **Goal:** Provide enough context so a reviewer can understand intent, trust assumptions, resource/capability design, and key risks quickly.

## 1) TL;DR (3–6 sentences)
**What does this contract do?**  
- <plain-English summary>

**Why does it exist?**  
- <product / business reason>

**Core user flows (happy path):**  
- <e.g., create vault -> deposit -> withdraw / mint -> transfer -> redeem>

## 2) Scope
**In scope (this contract is responsible for):**
- <bullet>
- <bullet>

**Out of scope (explicitly not handled here):**
- <bullet>
- <bullet>

## 3) Key Cadence Concepts Used
Check and briefly describe anything relevant:

- **Resources:** <which resources exist and why>
- **Interfaces:** <resource/interface contracts used>
- **Capabilities:** <what capabilities are exposed and to whom>
- **Storage / Public / Private paths:** <paths used and what they store/expose>
- **Events:** <key events emitted>
- **Auth patterns:** <auth(account) usage, auth(BorrowValue)/Entitlement usage, etc.>

## 4) Actors & Permissions
**Actors:**
- **Regular user:** <what can they do?>
- **Admin / privileged account(s):** <what powers exist?>
- **Operator / service account (if any):** <what can they do?>

**Admin actions & where they live:**
- `<functionName>`: <what it does, why it exists, what can go wrong>
- `<functionName>`: <...>

**How privileged access is enforced:**
- <e.g., only contract account, stored admin resource, capability gating, allowlist, etc.>

## 5) Storage Layout & Capability Surface
> This is usually where reviews spend time. Be explicit.

**Storage paths (contract account + user accounts):**
- `/storage/<...>`: <what resource lives here?>
- `/private/<...>`: <what capability is created/used?>
- `/public/<...>`: <what is publicly exposed?>

**Capabilities exposed publicly (and why they’re safe):**
- `/public/<...>` → <interface type> → <what actions it allows>

**Capabilities intended for private use:**
- `/private/<...>` → <interface type> → <who should have access>

**Resource lifecycle:**
- How are resources created? <factory, initializer, setup txn>
- How are resources moved/destroyed? <withdraw, destroy, burn, revoke>

## 6) Trust Assumptions
**We trust:**
- <which accounts/contracts and why (e.g., contract account admin, external contracts called into)>

**We do NOT trust (assume adversarial):**
- <arbitrary users, arbitrary tx submitters, any account calling public functions, etc.>

**External dependencies (contracts called / imported):**
- <FungibleToken, NonFungibleToken, MetadataViews, FlowToken, custom contracts, etc.>
- Assumptions: <e.g., standard FT behavior, no unexpected hooks, stable interfaces>

## 7) Key Invariants (must always be true)
Write invariants in a way a reviewer can try to break them:

- <Invariant 1 — e.g., totalSupply equals sum of all issued vault balances (or equivalent)>
- <Invariant 2 — e.g., withdrawals cannot exceed deposited amounts>
- <Invariant 3 — e.g., capability only grants read-only view, not withdraw>

## 8) Critical Functions / Hot Paths
List functions or transactions that are most security-sensitive:

- `<functionName>`: <why it’s critical + what could go wrong>
- `<functionName>`: <...>

Include any of:
- minting / issuing
- withdrawals / transfers
- admin configuration
- capability publication / revocation
- resource destruction / burning

## 9) Known Risks / Tradeoffs
Be honest — this helps reviewers focus.

- <Known risk 1> — <why it exists / mitigation>
- <Known risk 2>

## 10) Testing Notes
**What’s covered well:**
- <unit tests for X, Y>

**What’s not covered / needs reviewer attention:**
- <edge cases, integration behavior, capability misuse cases>

## 11) Review Checklist (Author)
- [ ] Code formatted / style-checked per repo standards
- [ ] No debug code, TODOs, or commented-out logic left in critical paths
- [ ] Public-facing functions and resource interfaces have doc comments
- [ ] Non-obvious logic is commented (math, access control, capability decisions, storage paths)
- [ ] Capability surface reviewed: public vs private exposure is intentional
- [ ] Resource lifecycle reviewed: no unintended resource loss or duplication
- [ ] Invariants listed above reflect the current implementation

## 12) Links
- **PR:** <link>
- **Contract location / paths:** <repo paths>
- **Deployment info (if known):** <network, contract address/account>
- **Related specs/docs:** <links>
- **Diagrams/images:** <links>
