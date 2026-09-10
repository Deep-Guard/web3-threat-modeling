# Protocol Threat Model

**Protocol Name:**
**Version / Date:**
**Authors:**
**Status:** Draft / Review / Final

---

## 1. System Overview

*Describe your protocol in plain language. What does it do? Who uses it? What value does it hold or move?*

**What the protocol does:**

**Who the users are:**

**What assets are at stake:**
- Total value at risk:
- Asset types: (ETH, ERC20 tokens, NFTs, governance rights, user data)

---

## 2. System Map

*List every component in your protocol and what it does. Include both on-chain and off-chain components.*

### On-Chain Components

| Component | Description | Who Controls It |
|-----------|-------------|-----------------|
| | | |
| | | |

### Off-Chain Components

| Component | Description | Who Controls It |
|-----------|-------------|-----------------|
| | | |
| | | |

### External Dependencies

| System | What You Depend On It For | What Happens If It Fails |
|--------|--------------------------|--------------------------|
| | | |
| | | |

---

## 3. Assets

*What does an attacker want to get, break, or take?*

### Financial Assets
- [ ] User funds in contracts
- [ ] Protocol treasury
- [ ] Liquidity pool reserves
- [ ] Unclaimed rewards
- [ ] Other: ___

### Protocol Control
- [ ] Admin keys / multisig
- [ ] Upgrade control
- [ ] Governance voting power
- [ ] Pause / unpause authority

### Data and Reputation
- [ ] User personal data or activity
- [ ] Protocol reputation and trust
- [ ] Price or market data

**For each asset, answer:**
- Where is it stored?
- Who can move or modify it?
- What is the worst-case loss if it is compromised?

---

## 4. Trust Boundaries

*A trust boundary is where your system accepts input from something it does not fully control.*

### Where Does Untrusted Input Enter?

| Entry Point | Source | What It Controls |
|-------------|--------|------------------|
| User transaction calldata | End users | Function calls, parameters |
| Oracle price feeds | External data provider | Asset valuations |
| Governance proposals | Token holders | Protocol parameters |
| API requests | End users | Backend operations |
| Bridge messages | Cross-chain relay | Cross-chain asset flows |
| Add your own... | | |

### Which Components Trust Each Other?

| Component A | Trusts | Component B | Should This Trust Be There? |
|-------------|--------|-------------|----------------------------|
| | | | |
| | | | |

### Centralization Points

*Where could one person, key, or service make a unilateral decision that harms users?*

| Point of Centralization | Who Controls It | Impact If Compromised |
|------------------------|-----------------|----------------------|
| | | |
| | | |

---

## 5. Attacker Profiles

*Who might attack your protocol? Use the [Attacker Profiles](./attacker-profiles.md) reference for detail.*

Check all that apply and rate their realistic threat level for your protocol:

| Attacker Type | Threat Level (High / Medium / Low / N/A) | Notes |
|---------------|------------------------------------------|-------|
| External attacker (anonymous) | | |
| Compromised admin or team member | | |
| Malicious user (protocol participant) | | |
| Governance attacker | | |
| Oracle attacker | | |
| Compromised dependency or supplier | | |
| Bridge or cross-chain attacker | | |
| Insider threat | | |

---

## 6. Threat Enumeration

*For each realistic attacker, what are the specific things they could try?*

Use this table to enumerate threats. Add as many rows as needed.

| ID | Threat | Attacker | Entry Point | Asset Targeted | Likelihood | Impact | Notes |
|----|--------|----------|-------------|----------------|-----------|--------|-------|
| T-001 | | | | | H/M/L | H/M/L | |
| T-002 | | | | | H/M/L | H/M/L | |
| T-003 | | | | | H/M/L | H/M/L | |

**Likelihood:** How realistic is this attack given your protocol's current state?
**Impact:** How bad is the outcome if the attack succeeds?

---

## 7. Attack Paths

*For your highest-priority threats, trace the full attack chain.*

Use the [Attack Path Worksheet](./attack-path-worksheet.md) for each high-priority threat.

**High-priority threats to trace:**

- T-XXX: [Name]
- T-XXX: [Name]
- T-XXX: [Name]

---

## 8. Mitigations

*What have you already done to address each threat? What is still missing?*

| Threat ID | Mitigation In Place | Mitigation Gap | Priority to Fix |
|-----------|---------------------|----------------|-----------------|
| T-001 | | | High / Medium / Low |
| T-002 | | | |

---

## 9. Open Questions

*Things you are unsure about that the security assessment should help answer.*

1.
2.
3.

---

## 10. Threat Model Review

*Record who reviewed this document and when.*

| Reviewer | Role | Date | Notes |
|----------|------|------|-------|
| | | | |

**Next Review Date:**

---

*Once your threat model is complete, share it with your security assessors. It significantly improves the quality and focus of a professional assessment.*

**Contact Deep Guard:** getaudited@deepguard.xyz | Telegram: @KingFavourCreates
