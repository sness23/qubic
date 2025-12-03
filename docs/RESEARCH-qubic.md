# Qubic Blockchain & Hackathon Research

## Hackathon Overview

### Qubic Hack the Future

**Dates:** December 5-7, 2025
**Prize Pool:** $44,550
**Platform:** https://lablab.ai/event/qubic-hack-the-future

### Two Competition Tracks

#### Track 1: Nostromo Launchpad
Build high-impact protocols including:
- **DeFi** - lending, DEXs, derivatives
- **Payments/RWAs** - real-world asset integration
- **Infrastructure/Middleware** - tooling and services
- **Experimental Applications** - novel use cases

#### Track 2: EasyConnect Integrations
Create no-code solutions using Make, Zapier, n8n:
- Airdrops
- Gamified community systems
- Token dashboards
- Market monitors
- Whale-tracking alerts

### Requirements
- Apply for a seat on lablab.ai
- Create or join a team
- Submit project through platform
- **Technical deployment is optional** - can focus on concept validation and design

---

## Qubic Blockchain

### Overview

Qubic is a high-performance Layer 1 blockchain built for speed, scalability, and real-world integrations. Founded by Come-from-Beyond (CfB) - the creator of:
- **NXT** - first Proof of Stake blockchain
- **IOTA** - first DAG architecture

### Performance

| Metric | Value |
|--------|-------|
| Peak TPS | **15.52 million** (CertiK verified) |
| Smart Contract TPS | **55+ million** transfers/second |
| Transaction Fees | **Feeless** |
| Finality | **Instant** |

Qubic is the fastest CertiK-verified blockchain ever.

### Consensus: Useful Proof of Work (UPoW)

Unlike traditional PoW that wastes energy on arbitrary puzzles, Qubic's UPoW directs computational power toward meaningful tasks - specifically **AI training** (Aigarth).

This means:
- Mining contributes to useful work
- No wasted energy on meaningless hashes
- Network security + AI development combined

### Smart Contracts

**Language:** C++ (unique - most chains use Solidity/Rust)

**Structure:**
```cpp
// Input struct
struct MyInput {
    uint64 amount;
    id destinationAddress;
};

// Output struct
struct MyOutput {
    uint64 result;
};
```

**How They Work:**
- Functions receive C++ struct as input, emit struct as output
- Transactions trigger functions by setting `destinationPublicKey` to contract index
- Integration with real-world data via **Oracles**

**Deployment Process:**
1. Proposal vote: requires **451 of 676 computors** to participate with majority approval
2. **Dutch auction IPO** - innovative launch mechanism where contracts self-finance

**Economics:**
- Uses **Qubic Units (QUs)** as "energy"
- QUs are **burned** during execution (deflationary)
- Generally cost-free for users due to IPO self-financing
- Contracts can charge for specialized services

### Token: QUBIC ($QUBIC)

- Native token measuring computational energy
- Essential for running smart contracts and services
- **Burned upon use** - permanently removed from circulation (deflationary)

### Ecosystem Components

| Component | Description |
|-----------|-------------|
| **MSVault** | Multi-signature smart contract |
| **ETH Bridge** | Cross-chain connectivity |
| **Staking** | Earn rewards by locking $QUBIC |
| **Prediction Markets** | Create bets and predictions |
| **Aigarth** | Decentralized AI integration |
| **Oracles** | Real-world data feeds |

### Use Cases

- High-frequency DeFi & trading
- Real-time multiplayer gaming
- IoT data streams with instant settlement
- Decentralized AI applications
- Enterprise blockchain solutions

---

## Building on Qubic

### Technology Stack for Hackathon

| Layer | Options |
|-------|---------|
| **Blockchain** | Qubic (optional testnet deployment) |
| **Launch Platform** | Nostromo Launchpad |
| **No-Code** | EasyConnect + Make/Zapier/n8n |
| **Smart Contracts** | C++ |
| **Data** | Qubic Oracles |

### Key Advantages for Our Project

1. **Feeless transactions** - Great for community engagement, voting, micro-contributions
2. **Instant finality** - Real-time updates in Discord-style UI
3. **Oracle integration** - Verify milestones, import external data
4. **Deflationary model** - Token burning creates scarcity over time
5. **Quorum-based governance** - Built-in voting for contract deployment

### Challenges to Consider

1. **C++ smart contracts** - Less common skillset than Solidity
2. **451/676 computor vote** - High bar for contract deployment
3. **Newer ecosystem** - Fewer examples and tooling compared to Ethereum
4. **Documentation** - Less comprehensive than established chains

---

## Hackathon Strategy

### Given: 3-Day Hackathon + Strong Full-Stack Team

**Recommended Approach:**

1. **Day 1: Design & Architecture**
   - Finalize user flows
   - Design smart contract architecture
   - Create UI mockups/wireframes

2. **Day 2: Build MVP**
   - Discord-style frontend
   - Mock blockchain integration
   - Core features working

3. **Day 3: Polish & Pitch**
   - Demo video
   - Pitch deck
   - Documentation

### What to Prioritize

| Priority | Focus |
|----------|-------|
| **Must Have** | Working UI demo, clear concept, compelling pitch |
| **Should Have** | Mock data showing full user journey |
| **Nice to Have** | Actual Qubic testnet integration |
| **Skip** | Production-ready smart contracts |

### Judging Likely Criteria

Based on typical hackathons:
- **Innovation** - Is it novel?
- **Utility** - Does it solve a real problem?
- **Execution** - How complete is the demo?
- **Presentation** - Can you explain it clearly?
- **Qubic Integration** - How does it leverage the platform?

---

## Resources

### Official Qubic
- Website: https://qubic.org
- Documentation: https://docs.qubic.org
- Smart Contracts: https://docs.qubic.org/learn/smart-contracts/
- Ecosystem: https://qubic.org/ecosystem

### Hackathon
- Event Page: https://lablab.ai/event/qubic-hack-the-future
- Nostromo Launchpad: Referenced in hackathon materials
- EasyConnect: No-code integration layer

### Community
- Check Qubic Discord/Telegram for developer support during hackathon
