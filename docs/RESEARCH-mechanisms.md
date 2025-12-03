# Governance, Funding & Revenue Mechanisms Research

This document explains the different mechanisms we can use for voting, funding projects, and sharing revenue when products go to market.

---

## 1. Voting/Governance Mechanisms

### Token-Weighted Voting

**How it works:** 1 token = 1 vote

**Example:**
- Alice has 100 tokens → 100 votes
- Bob has 10 tokens → 10 votes
- Alice's vote counts 10x more than Bob's

**Pros:**
- Simple to understand and implement
- Fast decision-making
- Clear incentive alignment (more stake = more say)

**Cons:**
- **Plutocracy** - wealthy users dominate
- Small holders feel powerless
- Can be gamed by buying tokens before votes

**Used by:** Most basic DAOs, early DeFi governance

---

### Quadratic Voting (QV)

**How it works:** Cost of votes increases quadratically

| Votes | Cost |
|-------|------|
| 1 | 1 token |
| 2 | 4 tokens |
| 3 | 9 tokens |
| 4 | 16 tokens |
| 5 | 25 tokens |

**Example:**
- With 100 tokens, you can cast 10 strong votes (10² = 100)
- OR cast 1 vote on 100 different proposals
- Expressing preference intensity costs more

**Pros:**
- Reduces whale dominance
- Allows expressing **how strongly** you feel
- Protects minority viewpoints
- Mathematically optimal for preference aggregation

**Cons:**
- Complex for users to understand
- **Requires identity verification** (prevents splitting into multiple wallets)
- Slow voting process
- Credit budget setting is tricky

**Used by:** Gitcoin, CityDAO, some experimental DAOs

**Proposed by:** Vitalik Buterin, Glen Weyl, Zoë Hitzig (2018)

---

### Conviction Voting

**How it works:** Vote strength grows over time while staked

```
Day 1: Stake 100 tokens → 100 conviction
Day 7: Same stake → 500 conviction
Day 30: Same stake → 2000 conviction
```

When collective conviction crosses a threshold, the proposal passes.

**Key Properties:**
- **Continuous** - vote anytime, no deadlines
- **Accumulating** - longer commitment = stronger voice
- **No quorum needed** - passes when threshold reached
- **Changing vote resets** - prevents last-minute swings

**Pros:**
- No governance fatigue (don't need to vote on everything)
- **Turns vote buying into vote renting** (must maintain stake over time)
- Natural filter for engaged community members
- Protects against new members gaining instant power

**Cons:**
- **Slow** - not suitable for urgent decisions
- Complex to explain
- May need secondary mechanism for time-sensitive issues

**Used by:** 1Hive (Honey), Giveth, Commons Stack, Panvala

---

### Comparison Table

| Mechanism | Speed | Fairness | Complexity | Best For |
|-----------|-------|----------|------------|----------|
| Token-Weighted | Fast | Low | Simple | Quick decisions |
| Quadratic | Medium | High | Complex | High-stakes votes |
| Conviction | Slow | High | Medium | Ongoing funding allocation |

### Recommendation for Our Platform

**Hybrid approach:**
- **Conviction voting** for ongoing project funding (fits Discord-style continuous engagement)
- **Quadratic voting** for major decisions (platform upgrades, large treasury movements)
- **Simple majority** for project-internal decisions (project creators decide)

---

## 2. Funding Mechanisms

### All-or-Nothing (Kickstarter Model)

**How it works:**
- Project sets funding goal and deadline
- If goal reached → project gets all funds
- If goal not reached → all funds returned

**Pros:**
- Clear success/failure
- Protects backers from underfunded projects
- Creates urgency

**Cons:**
- Binary outcome may not reflect partial value
- Projects may set artificially low goals
- Good projects can fail by small margins

**Used by:** Kickstarter, Experiment.com

---

### Milestone-Based Funding

**How it works:**
- Total funding divided into milestones
- Each milestone has deliverables
- Funds released upon milestone completion
- Often includes oracle/verification step

**Example:**
```
Milestone 1: Literature review    → $5,000 (released on completion)
Milestone 2: Prototype           → $15,000
Milestone 3: Testing             → $20,000
Milestone 4: Publication         → $10,000
```

**Pros:**
- Reduces risk for funders
- Accountability throughout project
- Early termination if project fails

**Cons:**
- Overhead of verification
- May not suit exploratory research
- Rigid structure vs. scientific discovery

**Used by:** Traditional grants, VitaDAO for larger proposals

---

### Quadratic Funding (QF)

**How it works:**
1. **Matching pool** raised from sponsors/treasury
2. **Community donates** to projects (any amount)
3. **Quadratic formula** allocates matching funds:
   - More contributors = more matching (not more dollars)
   - 10 people × $1 gets MORE match than 1 person × $10

**The Math:**
```
Matching = (√contribution₁ + √contribution₂ + ... + √contributionₙ)² - total_contributions

Example:
Project A: 100 people give $1 each
  = (100 × √1)² = 10,000 - 100 = $9,900 matching

Project B: 1 person gives $100
  = (√100)² = 100 - 100 = $0 matching
```

**Pros:**
- **Democratizes funding** - small donors have huge impact
- **Reveals community preference** at scale
- Matching amplifies grassroots support
- Proven at scale ($67M+ via Gitcoin)

**Cons:**
- Requires Sybil resistance (fake accounts gaming system)
- Need matching pool sponsors
- Complex to explain to users

**Used by:** Gitcoin Grants, Optimism RetroPGF, various ecosystem grant programs

---

### Bonding Curve Funding (Pump.Science Model)

**How it works:**
1. Token created with bonding curve (price increases with supply)
2. Early buyers get lower prices
3. Trading generates LP fees
4. LP fees fund research milestones

**Example (Pump.Science):**
```
$500 in LP fees   → Worm testing unlocked
$1,500 in LP fees → Fly testing unlocked
$7,000 in LP fees → Mouse testing unlocked
$25,000 in LP fees → Human trials unlocked
```

**Pros:**
- Self-sustaining (trading funds research)
- Continuous funding (not one-time)
- Price discovery built-in
- Early supporters rewarded

**Cons:**
- Speculative element
- Regulatory concerns
- May attract traders not scientists

**Used by:** Pump.Science, various token launches

---

### Comparison Table

| Mechanism | Risk Distribution | Complexity | Continuous? | Best For |
|-----------|------------------|------------|-------------|----------|
| All-or-Nothing | Binary | Simple | No | Clear-goal projects |
| Milestone-Based | Staged | Medium | No | Long-term R&D |
| Quadratic Funding | Spread | Complex | Rounds | Community goods |
| Bonding Curve | Market | Complex | Yes | Speculative research |

### Recommendation for Our Platform

**Quadratic Funding** as primary mechanism because:
- Fits our diverse audience (makers, researchers, hobbyists)
- Democratizes what gets funded
- Small contributions from HTGAA community get amplified
- Proven model we can adapt

**Milestone-based releases** for funded projects:
- Protects funders
- Creates accountability
- Qubic oracles can verify milestones

---

## 3. Revenue Sharing Mechanisms

### IP-NFT Model (Molecule/VitaDAO)

**How it works:**
1. Project's IP (patents, data, rights) wrapped in NFT
2. NFT represents full legal ownership
3. NFT can be sold, licensed, or held

**For Funding:**
- Researchers mint IP-NFT for their project
- Sell/auction IP-NFT to raise funds
- Buyer owns resulting IP

**For Revenue:**
- IP-NFT owner can license IP
- Revenue from licensing goes to owner
- Owner can be a DAO (collective ownership)

---

### IP Tokens (IPTs) - Fractionalization

**How it works:**
1. IP-NFT exists (represents full IP)
2. Owner mints fungible tokens (IPTs) representing shares
3. IPT holders have governance rights over the IP
4. Revenue distributed proportionally to IPT holders

**Example:**
```
Project X IP-NFT mints 1,000,000 $IPT-X tokens
- Creator keeps 200,000 (20%)
- DAO treasury gets 300,000 (30%)
- Community sale: 500,000 (50%)

When licensing deal pays $100,000:
- Creator: $20,000
- DAO: $30,000
- Community holders: $50,000 (proportional)
```

**IPT Holder Rights:**
- Vote on licensing deals
- Vote on development direction
- Share in revenue
- Participate in IP governance

---

### Royalty Distribution (NFT Model)

**How it works:**
- Smart contract automatically splits payments
- Every sale/license triggers distribution
- Percentages fixed at creation

**Example:**
```solidity
Revenue Split:
- Original researcher: 30%
- Contributors: 20%
- DAO treasury: 20%
- Token holders: 30%
```

**Pros:**
- Automatic, trustless
- Transparent on-chain
- No manual accounting

**Cons:**
- Rigid (hard to change splits)
- Gas costs on distributions
- Complexity with many recipients

---

### Token Buyback & Burn

**How it works:**
1. Project generates revenue
2. Revenue used to buy project tokens from market
3. Bought tokens are burned (destroyed)
4. Remaining tokens worth more (deflation)

**Pros:**
- Simple mechanism
- Benefits all holders equally
- Creates buy pressure

**Cons:**
- Indirect value distribution
- Timing of buybacks matters
- May not feel like "income"

---

### Dividend Distribution

**How it works:**
1. Revenue accumulates in treasury
2. Periodically distributed to token holders
3. Can be claimed or auto-sent

**Pros:**
- Direct income for holders
- Feels like traditional investment
- Regular, predictable

**Cons:**
- Tax implications
- Securities regulation concerns
- Requires active treasury management

---

### Comparison Table

| Mechanism | Directness | Complexity | Regulatory Risk | Best For |
|-----------|-----------|------------|-----------------|----------|
| IP-NFT Licensing | Direct | High | Medium | Major IP deals |
| IPT Revenue Share | Direct | High | Medium | Community ownership |
| Royalty Splits | Direct | Medium | Low | Ongoing sales |
| Buyback & Burn | Indirect | Low | Low | Token appreciation |
| Dividends | Direct | Medium | High | Passive income |

### Recommendation for Our Platform

**Tiered approach based on project stage:**

1. **Early Stage (Funded Project)**
   - Project tokens minted
   - Funders receive tokens proportional to contribution
   - No revenue yet

2. **Development Stage**
   - Milestone completions unlock treasury
   - Contributors earn tokens for work
   - IP-NFT minted when IP created

3. **Revenue Stage (Product Sales)**
   - Revenue flows to smart contract
   - Automatic split:
     - 40% to token holders (proportional)
     - 30% to active contributors
     - 20% to platform treasury
     - 10% to original creator

---

## 4. Putting It All Together

### Complete Flow for Our Platform

```
1. PROJECT CREATION
   └── Creator posts idea
   └── Gets own "server" (Discord-style space)
   └── Initial discussion & refinement

2. FUNDING PHASE
   └── Project enters funding round (Quadratic Funding)
   └── Community contributes (small amounts amplified)
   └── Matching pool tops up popular projects
   └── Funding goal met → Project tokens minted

3. DEVELOPMENT PHASE
   └── Conviction voting allocates ongoing resources
   └── Milestone-based releases from treasury
   └── Contributors earn tokens for work
   └── IP-NFT minted when IP created

4. COMMERCIALIZATION
   └── Product developed & launched
   └── Revenue flows to smart contract
   └── Automatic distribution to stakeholders
   └── Reinvestment into next projects

5. GOVERNANCE (Throughout)
   └── Project-level: Simple voting by project token holders
   └── Platform-level: Quadratic voting for major decisions
   └── Funding allocation: Conviction voting
```

---

## Sources

### Voting Mechanisms
- [DAO Voting Mechanisms Explained](https://limechain.tech/blog/dao-voting-mechanisms-explained-2022-guide)
- [Conviction Voting - Giveth](https://medium.com/giveth/conviction-voting-34019bd17b10)
- [Quadratic Voting vs Conviction Voting](https://markaicode.com/quadratic-vs-conviction-voting/)

### Funding Mechanisms
- [Quadratic Funding - Gitcoin](https://www.gitcoin.co/blog/quadratic-funding)
- [WTF is Quadratic Funding?](https://www.wtfisqf.com/)
- [Experiment.com - How It Works](https://experiment.com/how-it-works)

### Revenue Sharing
- [IP-NFT V2 - Molecule](https://www.molecule.to/blog/introducing-ip-nft-v2)
- [IPTs - Molecule](https://www.molecule.to/blog/ipts-a-gain-of-function)
- [VitaDAO Tokenomics](https://gov.vitadao.com/t/vitadao-tokenomics-treasury/818)
