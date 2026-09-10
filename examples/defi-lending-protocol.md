# Example: DeFi Lending Protocol Threat Model

This is a worked example of the [Protocol Threat Model Template](../templates/protocol-threat-model-template.md) applied to a fictional DeFi lending protocol called **VaultLend**.

VaultLend allows users to deposit collateral and borrow assets. Liquidators can liquidate undercollateralized positions for a fee. An admin multisig controls protocol parameters.

---

## 1. System Overview

**What the protocol does:** Users deposit ETH or ERC20 tokens as collateral and borrow stablecoins against them. Positions that fall below the collateralization ratio can be liquidated by anyone.

**Who the users are:** Retail DeFi users depositing collateral, borrowers seeking leverage or liquidity, and liquidation bots.

**What assets are at stake:**
- Total value at risk: $50M in deposited collateral
- Asset types: ETH, WBTC, USDC, USDT, protocol governance token

---

## 2. System Map

### On-Chain Components

| Component | Description | Who Controls It |
|-----------|-------------|-----------------|
| LendingPool.sol | Core borrowing and repayment logic | Immutable (admin for params) |
| CollateralManager.sol | Tracks deposited collateral and ratios | Admin multisig (parameters) |
| LiquidationEngine.sol | Handles liquidations and fee distribution | Immutable |
| PriceOracle.sol | Reads Chainlink feeds and TWAP fallback | Admin multisig |
| GovernanceToken.sol | Protocol governance and fee sharing | Token holders |
| Timelock.sol | 48-hour delay on admin actions | Admin multisig |

### Off-Chain Components

| Component | Description | Who Controls It |
|-----------|-------------|-----------------|
| Frontend (vaultlend.xyz) | User interface for deposits and borrows | Dev team (Vercel) |
| Backend API | Portfolio data, notifications | Dev team (AWS) |
| Liquidation bot | Automated liquidation keeper | Dev team |
| Price feed monitor | Alerts if oracle deviates | Dev team |

### External Dependencies

| System | What We Depend On It For | What Happens If It Fails |
|--------|--------------------------|--------------------------|
| Chainlink ETH/USD | Collateral valuation | Protocol falls back to TWAP; if both fail, borrows are paused |
| Chainlink WBTC/USD | Collateral valuation | Same as above |
| Uniswap v3 TWAP | Fallback price source | If Chainlink fails and TWAP is stale, new borrows pause |
| USDC (Circle) | Borrowed asset | USDC blacklist could freeze borrower positions |

---

## 3. Assets

### Financial Assets
- [x] User deposited collateral (~$50M)
- [x] Protocol treasury (~$2M in governance tokens)
- [x] Accrued interest in the protocol reserve

### Protocol Control
- [x] Admin multisig (3-of-5) — controls parameter changes via Timelock
- [x] Governance voting power — controls future upgrades

### Data and Reputation
- [x] Protocol reputation — a significant exploit would likely end the protocol

**Worst-case:** Admin key compromise + no timelock bypass = attacker sets collateral ratio to 0 and drains all deposits within 48 hours. (Mitigated by 48-hour Timelock.)

---

## 4. Trust Boundaries

### Where Does Untrusted Input Enter?

| Entry Point | Source | What It Controls |
|-------------|--------|------------------|
| deposit(), borrow(), repay() | Any user | Core protocol flows |
| Chainlink price feeds | Chainlink oracle network | All collateral valuations |
| Governance proposals | Any token holder | Protocol parameter changes |
| Liquidation calls | Any liquidator | Which positions are liquidated and for how much |
| Frontend calldata | User's browser | What transactions users sign |

### Centralization Points

| Point | Who Controls It | Impact If Compromised |
|-------|-----------------|----------------------|
| Admin multisig (3-of-5) | 5 team members | Can change collateral ratios, interest rates, oracle sources |
| Vercel deployment | 2 dev team members | Can push malicious frontend to all users |
| AWS backend | 2 dev team members | Can serve false data to users |
| Liquidation bot wallet | 1 team member | Bot could be used to front-run liquidations |

---

## 5. Attacker Profiles

| Attacker Type | Threat Level | Notes |
|---------------|-------------|-------|
| External attacker | **High** | Protocol holds $50M — high-value target |
| Compromised admin | **High** | Admin can change parameters; timelock provides partial protection |
| Malicious user | **Medium** | Could attempt to game liquidations or borrow edge cases |
| Governance attacker | **Medium** | Token distribution is relatively concentrated; feasible with OTC purchase |
| Oracle attacker | **High** | WBTC/USD feed has lower liquidity — potential manipulation target |
| Compromised dependency | **Medium** | USDC blacklist, Chainlink outage |
| Supply chain attacker | **Low** | Small team; low-profile npm packages in frontend |

---

## 6. Threat Enumeration

| ID | Threat | Attacker | Entry Point | Asset | Likelihood | Impact |
|----|--------|----------|-------------|-------|-----------|--------|
| T-001 | Flash loan oracle manipulation — borrow at inflated collateral value | External | borrow() + TWAP oracle | User deposits | Medium | Critical |
| T-002 | Admin key compromise — malicious collateral ratio change | Compromised admin | Admin multisig | All deposits | Low | Critical |
| T-003 | Frontend DNS hijack — users sign malicious transactions | External | DNS / Vercel | User wallet approvals | Low | High |
| T-004 | Governance attack — malicious upgrade proposal passed with flash-loaned votes | Governance attacker | Governance contract | Protocol control | Low | Critical |
| T-005 | Liquidation bot manipulation — force liquidations on positions the attacker controls | Malicious user | Liquidation + oracle | Protocol liquidation fee | Medium | Medium |
| T-006 | USDC blacklisting — borrowed USDC frozen, borrowers cannot repay | External (Circle) | USDC contract | Borrower positions | Low | High |

---

## 7. Attack Paths (Top Priority)

### T-001: Flash Loan Oracle Manipulation

See [full worksheet](../templates/attack-path-worksheet.md) — summarized below:

```
Attacker takes a large flash loan
    |
    v
Manipulates WBTC/USDC pool to inflate WBTC price
    |
    v
Calls borrow() — inflated collateral value allows excess borrowing
    |
    v
Repays flash loan
    |
    v
Walks away with borrowed USDC, leaving undercollateralized position
    |
    v
Protocol takes a loss when position is eventually liquidated
```

**Root cause:** TWAP observation window is only 5 minutes — manipulable within a single block on low-liquidity pools.

**Mitigation required:** Extend TWAP window to at least 30 minutes; add minimum liquidity threshold check before using TWAP.

---

## 8. Open Questions for the Security Assessment

1. Is our 5-minute TWAP window genuinely manipulation-resistant given current WBTC/USDC pool liquidity?
2. Does our Timelock fully protect against a compromised admin key, or are there functions it does not cover?
3. Is our governance token distribution concentrated enough to make a governance attack feasible today?
4. What happens to user positions if Circle blacklists our lending pool contract address?

---

*This example is simplified for illustration. A real threat model for a $50M protocol would require significantly more depth — and should be reviewed by a professional security team before launch.*

**Contact Deep Guard:** getaudited@deepguard.xyz | Telegram: [Message us](https://t.me/KingFavourCreates)
