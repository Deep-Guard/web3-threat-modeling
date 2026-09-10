# Web3 Threat Modeling

**by [Deep Guard](https://deepguard.xyz)**

Most Web3 protocols are built without ever asking: *who would attack us and how?*

Threat modeling answers that question before an attacker does.

This repository gives protocol teams practical templates and guides to model threats across their entire system — not just their smart contracts. Teams that work through this process consistently discover risks they had never considered, and arrive at security assessments far better prepared.

---

## What Is Threat Modeling?

Threat modeling is a structured way of thinking about security from an attacker's perspective. It asks four questions:

1. **What are we building?** — Map the system
2. **What can go wrong?** — Identify threats
3. **What are we doing about it?** — Apply mitigations
4. **Did we do a good job?** — Review and iterate

In Web3, threat modeling is especially valuable because your attack surface is wider than most teams realize. It spans smart contracts, backend services, frontend applications, key management, oracles, economics, and the humans operating the protocol.

---

## Contents

### Templates
- [Protocol Threat Model Template](./templates/protocol-threat-model-template.md) — The main document to fill out for your protocol
- [Attacker Profiles](./templates/attacker-profiles.md) — Who might attack a Web3 protocol and what they want
- [Attack Path Worksheet](./templates/attack-path-worksheet.md) — Structure for mapping specific attack chains

### Examples
- [DeFi Lending Protocol Example](./examples/defi-lending-protocol.md) — A worked example of a complete threat model

---

## The Web3 Protocol Attack Surface

```
                    WEB3 PROTOCOL
                         |
       +-----------------+-----------------+
       |                 |                 |
    Frontend           Backend          Contracts
       |                 |                 |
       v                 v                 v
    Wallets            APIs             Admin
       |                 |                 |
       +-----------------+-----------------+
                         |
                    External Systems
                         |
            +------------+------------+
            |            |            |
         Oracle        Bridge       RPC
```

Each node in this diagram is a potential entry point. Each connection is a trust relationship that can be exploited. A threat model traces the paths from attacker entry to protocol damage.

---

## How to Use This Repo

1. **Start with the [Protocol Threat Model Template](./templates/protocol-threat-model-template.md)**
   Fill it out for your protocol. It takes 2–4 hours for a small protocol, longer for a complex one.

2. **Use the [Attacker Profiles](./templates/attacker-profiles.md)**
   Think through each attacker type and whether they have a realistic path to causing damage.

3. **Map specific threats using the [Attack Path Worksheet](./templates/attack-path-worksheet.md)**
   For each realistic threat, trace the full chain from initial action to final impact.

4. **Review the [DeFi Lending Example](./examples/defi-lending-protocol.md)**
   See what a completed threat model looks like in practice.

---

## What to Do After Threat Modeling

A threat model is not a security audit. It identifies what could go wrong — a security assessment verifies whether those threats are actually realized in your implementation.

After completing your threat model, share it with your security assessors. It dramatically improves the quality of the assessment by letting reviewers focus on your highest-priority risks rather than building a picture of your system from scratch.

---

## Need a Professional Assessment?

If working through this template surfaces risks you are not sure how to evaluate, or if you want expert eyes on your threat model, reach out to Deep Guard.

**Email:** getaudited@deepguard.xyz
**Telegram:** @KingFavourCreates
**Website:** https://deepguard.xyz

---

## Support Open-Source Security Education

**ETH:** `YOUR_ETH_ADDRESS`

---

## License

MIT
