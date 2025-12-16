# Contract Review Notes — <ContractName> (Cadence)

> **Goal:** Provide enough context so a reviewer can understand intent, design decisions, and security assumptions quickly.

## 1) TL;DR (3–6 sentences)
**What does this contract do?**  
- <plain-English summary>

**Why does it exist?**  
- <product / business reason>

**Core user flows (happy path):**  
- <e.g., create vault → deposit → withdraw>

---

## 2) Scope
**In scope (this contract is responsible for):**
- <bullet>
- <bullet>

**Out of scope (explicitly not handled here):**
- <bullet>
- <bullet>

---

## 3) Key Cadence Concepts Used
Briefly describe anything relevant:

- **Resources:** <which resources exist and why>
- **Interfaces:** <resource/interface contracts used>
- **Capabilities:** <what capabilities are exposed and to whom>
- **Storage / Public / Private paths:** <paths used and what they store/expose>
- **Events:** <key events emitted>
- **Auth patterns:** <auth(account), entitlements, capability gating, etc.>

---

## 4) Actors & Permissions
**Actors:**
- **Regular user:** <what can they do?>
- **Admin / privileged account(s):** <what powers exist?>
- **Operator / service account (if any):** <what can they do?>

**How privileged access is enforced:**
- <e.g., contract account only, admin resource in storage, capability gating>

---

## 5) Storage Layout & Capability Surface
> Be explicit — this is a primary audit focus.

**Storage paths:**
- `/storage/<...>`: <resource stored>
- `/private/<...>`: <capability type + intended consumers>
- `/public/<...>`: <capability type + why public access is safe>

**Resource lifecycle:**
- Creation: <how / where>
- Movement: <withdraw / deposit flows>
- Destruction: <burn / destroy semantics>

---

## 6) Trust Assumptions
**We trust:**
- <accounts/contracts and why>

**We do NOT trust (assume adversarial):**
- <arbitrary users, tx submitters, public callers>

**External dependencies:**
- <e.g., FungibleToken, NonFungibleToken, MetadataViews>
- Assumptions: <standard behavior relied upon>

---

## 7) Key Invariants (must always be true)
Write invariants so a reviewer can try to violate them:

- <Invariant 1>
- <Invariant 2>
- <Invariant 3>

---

## 8) Critical Functions / Hot Paths
Functions or transactions that are most security-sensitive:

- `<functionName>`: <why it’s critical + what could go wrong>
- `<functionName>`: <...>

Examples:
- minting / issuing
- withdrawals
- admin configuration
- capability publication / revocation
- resource destruction

---

## 9) Known Risks / Tradeoffs
Be explicit — this helps reviewers focus.

- <Known risk 1> — <why it exists / mitigation>
- <Known risk 2>

---

## 10) Testing & Emulator Workflows
**Cadence tests present:**
- <describe coverage or link to tests>

**Emulator workflows available:**
- <e.g., shell scripts or commands using Flow CLI>
- <examples: account setup, vault creation, mint, deposit, withdraw, balance check>

**What’s not covered / needs reviewer attention:**
- <edge cases, integration behavior>

---

## 11) Review Checklist (Author)

### Code Quality & Style
- [ ] Code follows the project style guide (link if applicable)
- [ ] Code is clearly documented (file-level, public functions, non-obvious logic)
- [ ] Code follows Cadence design patterns  
  https://cadence-lang.org/docs/design-patterns
- [ ] Code avoids known Cadence anti-patterns  
  https://cadence-lang.org/docs/anti-patterns
- [ ] Code follows project development standards  
  https://cadence-lang.org/docs/project-development-tips

### Security & Correctness
- [ ] Code follows Cadence security best practices  
  https://cadence-lang.org/docs/security-best-practices
- [ ] Capability surface reviewed (public vs private exposure is intentional)
- [ ] Resource lifecycle reviewed (no unintended duplication or loss)
- [ ] Invariants listed above reflect the current implementation

### Tooling & Tests
- [ ] Cadence tests exist and pass  
  https://cadence-lang.org/docs/testing-framework
- [ ] Emulator workflows exist and run successfully
- [ ] Cadence linter run and feedback addressed  
  https://developers.flow.com/build/tools/flow-cli/lint  
  *(Also available via the Cadence VS Code extension)*

### Final Checks
- [ ] No debug code, TODOs, or commented-out logic in critical paths
- [ ] This document matches the current commit: `<commit-hash>`

---

## 12) Links
- **PR:** <link>
- **Contract location / paths:** <repo paths>
- **Deployment info (if known):** <network + account>
- **Related specs/docs:** <links>
