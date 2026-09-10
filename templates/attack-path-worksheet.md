# Attack Path Worksheet

Use this worksheet to trace a specific threat from initial attacker action to final impact. Complete one worksheet per high-priority threat from your threat model.

---

## Threat Reference

**Threat ID:** T-XXX
**Threat Name:**
**Attacker Profile:** (External / Compromised Admin / Malicious User / Governance / Oracle / etc.)
**Date:**

---

## Step 1: Attacker Starting Position

*What does the attacker have when they begin? What access, capital, or knowledge do they need?*

**Starting access:**
- [ ] No special access — just a wallet and an internet connection
- [ ] A governance token position of approximately ___
- [ ] Flash loan access to ___ in capital
- [ ] Compromised key or credential: ___
- [ ] Other: ___

**Knowledge required:**
- [ ] Publicly readable on-chain state only
- [ ] Knowledge of internal implementation details
- [ ] Access to off-chain systems
- [ ] Other: ___

**Capital required:** Approximately ___

---

## Step 2: The Attack Chain

*Trace every step from the attacker's first action to the final outcome. Be specific.*

```
Step 1: [Attacker action]
    |
    v
Step 2: [System response or state change]
    |
    v
Step 3: [Next attacker action]
    |
    v
Step 4: [System response or state change]
    |
    v
...
    |
    v
Final: [Impact]
```

**Write it out in plain language below:**

1.
2.
3.
4.
5.

---

## Step 3: What Makes This Possible?

*What assumption, missing check, or design choice allows this attack to work?*

**Root cause:**

**Where in the system does it live?**
- [ ] Smart contract logic
- [ ] Protocol architecture / trust model
- [ ] Key management
- [ ] Oracle configuration
- [ ] Backend / API
- [ ] Frontend
- [ ] Infrastructure
- [ ] Economics / incentive design
- [ ] Other: ___

---

## Step 4: Impact Assessment

**What is lost or damaged?**

| Impact Type | Description | Estimated Magnitude |
|-------------|-------------|---------------------|
| User funds | | |
| Protocol treasury | | |
| Protocol reputation | | |
| User data | | |
| Protocol availability | | |

**Is the damage reversible?**
- [ ] Yes — fully reversible (e.g., pausing stops the attack)
- [ ] Partially — some recovery possible
- [ ] No — funds are permanently lost or damage is permanent

---

## Step 5: Is This Profitable for the Attacker?

*An attacker will weigh expected profit against cost and risk. If the attack is not profitable, it is less likely — but not impossible.*

**Estimated attacker profit:**
**Estimated attacker cost:** (gas, capital lockup, risk of failure)
**Is the attack profitable at current protocol scale?**
**At what TVL does it become profitable?**

---

## Step 6: Existing Mitigations

*What is already in place that makes this attack harder or impossible?*

| Mitigation | How It Helps | Does It Fully Block the Attack? |
|------------|-------------|--------------------------------|
| | | |
| | | |

---

## Step 7: Recommended Mitigations

*What should be added or changed to address this threat?*

1.
2.
3.

**Priority:** High / Medium / Low
**Who is responsible for implementing:**

---

## Step 8: Residual Risk

*After recommended mitigations are implemented, what risk remains?*

**Residual risk level:** High / Medium / Low / Acceptable

**Reason:**

---

*Completed worksheets should be shared with your security assessors and revisited whenever the protocol changes significantly.*

**Contact Deep Guard:** getaudited@deepguard.xyz | Telegram: [Message us](https://t.me/KingFavourCreates)
