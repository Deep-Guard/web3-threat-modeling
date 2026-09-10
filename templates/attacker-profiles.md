# Attacker Profiles for Web3 Protocols

Use this reference when filling out Section 5 of the [Protocol Threat Model Template](./protocol-threat-model-template.md).

For each attacker type, consider: do they have a realistic path to damaging your specific protocol?

---

## 1. External Attacker (Anonymous)

**Who they are:** Anyone on the internet — a financially motivated hacker, a nation-state actor, a competing protocol, or a hobbyist looking for a bug bounty or a quick profit.

**What they want:** Financial gain, usually. Sometimes reputation.

**What they can do:**
- Interact with any public-facing contract function
- Submit crafted transactions or calldata
- Monitor the mempool and front-run transactions
- Use flash loans to temporarily access large capital
- Probe the frontend and backend for web vulnerabilities
- Attempt phishing or social engineering attacks

**Why they are the most common threat:** No special access required. Anyone who finds a vulnerability can exploit it.

---

## 2. Compromised Admin or Team Member

**Who they are:** A current or former team member whose credentials have been stolen, or a team member who has turned malicious.

**What they want:** Direct theft of protocol funds or backdoor access for a future attack.

**What they can do:**
- Exercise any privileged contract function they have keys for
- Push malicious code to the frontend or backend
- Exfiltrate private keys or secrets they have access to
- Modify configuration to create new vulnerabilities

**Why this matters:** Admin access in DeFi is extraordinarily powerful. A single compromised admin key has been the root cause of hundreds of millions in losses.

---

## 3. Malicious Protocol Participant

**Who they are:** A user of the protocol — borrower, liquidity provider, governance voter — who is willing to operate at the edges of the rules to extract value.

**What they want:** Financial advantage at the expense of other participants or the protocol treasury.

**What they can do:**
- Manipulate their own position to trigger edge cases
- Game reward mechanics or incentive structures
- Perform griefing attacks that cost others more than they cost the attacker
- Use the protocol in ways the team did not intend but cannot prohibit

**Why this matters:** These attackers are indistinguishable from normal users until the damage is done.

---

## 4. Governance Attacker

**Who they are:** An entity that acquires or borrows enough governance tokens to pass a malicious proposal.

**What they want:** To redirect treasury funds, approve a malicious upgrade, or change protocol parameters in their favor.

**What they can do:**
- Accumulate or borrow governance tokens via flash loans or OTC markets
- Propose changes that appear benign but contain hidden malicious effects
- Exploit low voter turnout to pass a proposal with minimal token ownership
- Time an attack around governance windows when participation is low

**Why this matters:** Governance is often the most underprotected attack surface in a DAO-controlled protocol.

---

## 5. Oracle Attacker

**Who they are:** An attacker with sufficient capital to manipulate the price data your protocol relies on, or someone who can compromise the off-chain data provider itself.

**What they want:** To create artificially favorable conditions — a manipulated price that lets them borrow more, trigger favorable liquidations, or exploit settlement mechanisms.

**What they can do:**
- Temporarily move a low-liquidity pool price within a single transaction
- Compromise an off-chain data feed provider
- Exploit the window between a price move and your protocol's reaction

**Why this matters:** Oracle manipulation has been the attack vector in some of the largest DeFi exploits ever recorded.

---

## 6. Compromised Dependency

**Who they are:** Not a person directly, but a compromised external system your protocol relies on — an external contract that gets exploited, an npm package with a malicious update, a third-party API that is taken over.

**What they want:** Your protocol's funds or user data, accessed via the trust your protocol places in the compromised dependency.

**What they can do:**
- A compromised external contract can return malicious data your contracts act on
- A compromised npm package can exfiltrate private keys or redirect frontend transactions
- A compromised API can serve false data to your users

**Why this matters:** You inherit the security posture of everything you depend on.

---

## 7. Bridge or Cross-Chain Attacker

**Who they are:** An attacker targeting the messaging or asset transfer layer between chains.

**What they want:** To forge cross-chain messages, replay valid messages on the wrong chain, or exploit inconsistencies between what one chain records and what another chain acts on.

**What they can do:**
- Submit a forged or replayed bridge message to trigger an unintended state change
- Exploit finality differences to conduct a double-spend
- Compromise bridge validators or relayers

**Why this matters:** Cross-chain bridges have suffered the largest individual exploits in Web3 history.

---

## 8. Supply Chain Attacker

**Who they are:** An attacker who targets your protocol indirectly — by compromising the tools, libraries, or developers that build it.

**What they want:** To insert malicious code into your protocol before it is deployed or while it is running.

**What they can do:**
- Publish a typosquatted or compromised npm package
- Compromise a developer's machine and modify code before commit
- Inject malicious code into a CI/CD pipeline
- Compromise a third-party audit tool or deployment helper

**Why this matters:** Supply chain attacks are low-visibility and often not discovered until after deployment.

---

*Once you have assessed which attacker profiles are relevant to your protocol, return to the [Protocol Threat Model Template](./protocol-threat-model-template.md) to enumerate specific threats.*

**Contact Deep Guard:** getaudited@deepguard.xyz | Telegram: [Message us](https://t.me/KingFavourCreates)
