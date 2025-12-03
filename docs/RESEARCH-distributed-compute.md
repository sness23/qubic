# Distributed Computing for Molecular Modeling

## The Idea

Allow users to earn rewards by contributing their browser's computing power to run molecular modeling calculations (docking, crystallography, simulations) for projects on the platform.

**User Experience:**
1. User opens platform in browser
2. Opts in to "Compute for Rewards"
3. Leaves tab open while browsing/working
4. Browser runs molecular simulations in background
5. User earns tokens for compute contributed

This is like **Folding@Home meets crypto** - but runs entirely in the browser via WebAssembly.

---

## Why This is Brilliant

### 1. Solves Real Problem for Projects
- Molecular docking is **computationally expensive**
- Virtual screening can require millions of docking runs
- Cloud GPU time is expensive ($1-3/hr for decent GPUs)
- Projects on our platform may lack compute budget

### 2. Creates Token Utility
- Platform token has real use case (paying for compute)
- Users earn tokens for passive contribution
- Creates circular economy within platform

### 3. Differentiates from Competitors
- No other DeSci platform has browser-based distributed compute
- VitaDAO, Molecule, etc. just fund research - don't provide infrastructure
- We provide funding AND compute resources

### 4. Ties into Qubic's Vision
- Qubic's "Useful Proof of Work" trains AI with mining energy
- Our approach: use browser cycles for actual science
- Philosophical alignment with Qubic's mission

---

## Technical Feasibility

### Proof of Concept: Webina

**Webina already exists** - AutoDock Vina compiled to WebAssembly, running in browsers.

> "Webina is a JavaScript/WebAssembly library that runs AutoDock Vina entirely in a web browser. The docking calculations take place on the user's own computer rather than a remote server."

**Performance:**
- Near-identical results to native Vina (poses differ by max 0.21 Å)
- WebAssembly runs at **80% of native C++ speed** for scientific computing
- 20-fold speedup over pure JavaScript implementations

**Resources:**
- GitHub: https://github.com/durrantlab/webina
- Paper: Kochnev et al., *Bioinformatics* 2020
- Live demo: http://durrantlab.com/webina

### WebAssembly Performance for Science

| Metric | WebAssembly vs Native |
|--------|----------------------|
| General compute | 80-100% of native speed |
| Scientific kernels | 50-80% depending on memory patterns |
| Molecular docking | ~80% (validated by Webina) |
| vs JavaScript | 1.3x - 20x faster |

### Existing Browser-Based Compute Projects

| Project | Tech | Status |
|---------|------|--------|
| **Webina** | AutoDock Vina + WASM | Production |
| **BoomerangJS** | JS distributed compute middleware | Active |
| **dis.io** | Browser + Node.js compute | Active |
| **Pando** | WebRTC + WebSockets volunteers | Research |

---

## Scientific Software to Port

### Priority 1: Molecular Docking

| Software | Purpose | Status |
|----------|---------|--------|
| **AutoDock Vina** | Ligand docking | ✅ WASM exists (Webina) |
| **AutoDock-GPU** | GPU-accelerated docking | Needs porting |
| **SMINA** | Scoring-focused docking | C++, portable |
| **rDock** | High-throughput docking | Open source |

**Why Docking First:**
- Embarrassingly parallel (each ligand independent)
- Well-defined input/output (ligand + receptor → score + pose)
- Clear scientific value (drug discovery)
- Webina proves it works

### Priority 2: Molecular Dynamics Prep

| Software | Purpose | Portability |
|----------|---------|-------------|
| **OpenMM** | MD simulations | Python/C++, complex |
| **GROMACS** | MD simulations | Very complex |
| **ParmEd** | Parameter manipulation | Python, simpler |

### Priority 3: Crystallography

| Software | Purpose | Complexity |
|----------|---------|------------|
| **CCP4** | Suite of crystallography tools | Very large, modular |
| **PHENIX** | Automated structure solution | Python + C++, huge |
| **cctbx** | Core crystallography library | ✅ Python, most portable |

**Reality Check:** Full crystallography suites are massive. Focus on:
- Specific algorithms (molecular replacement, refinement)
- cctbx core library (already well-structured)

---

## Crypto Compute Networks: Lessons Learned

### Golem Network (GLM)

**Model:** Peer-to-peer CPU compute marketplace

**How Rewards Work:**
- Providers register compute capacity
- Requestors submit jobs + payment in GLM
- Jobs broken into subtasks, distributed to providers
- Providers complete work, receive GLM

**Tokenomics:**
- Fixed supply: 1 billion GLM
- Token used for: payments, staking, governance
- No inflation/emission schedule

**Key Innovation:** Octant platform lets users lock GLM to fund open source projects

### Render Network (RNDR)

**Model:** Distributed GPU rendering for graphics/video

**How Rewards Work:**
- Artists submit render jobs
- GPU owners complete renders
- Payment in RNDR tokens

**Difference from Golem:** Focused on specific use case (rendering) vs general compute

### io.net

**Model:** GPU marketplace for ML/AI training

**Scale:** 300,000+ verified GPUs
**Focus:** Machine learning workloads
**Tech:** Ray-native orchestration for distributed ML

### Akash Network (AKT)

**Model:** Decentralized cloud (like decentralized AWS)

**How it Works:**
- Reverse auction: deployers specify needs, providers bid
- Docker container deployment
- 1/3 the cost of traditional cloud

---

## Our Model: Browser-Based Compute Rewards

### Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        USER'S BROWSER                            │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │                    COMPUTE WORKER                        │    │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────────┐  │    │
│  │  │   Webina    │  │   Future    │  │    Task         │  │    │
│  │  │   (WASM)    │  │   Modules   │  │    Manager      │  │    │
│  │  └─────────────┘  └─────────────┘  └─────────────────┘  │    │
│  └─────────────────────────────────────────────────────────┘    │
│                              │                                   │
│                              │ WebSocket                         │
└──────────────────────────────┼──────────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────────┐
│                      COMPUTE COORDINATOR                         │
│  ┌─────────────┐  ┌─────────────┐  ┌───────────────────────┐   │
│  │    Task     │  │   Result    │  │      Verification     │   │
│  │    Queue    │  │   Collector │  │      & Rewards        │   │
│  └─────────────┘  └─────────────┘  └───────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────────┐
│                      QUBIC BLOCKCHAIN                            │
│  ┌─────────────────┐  ┌─────────────────┐                       │
│  │  Compute Pool   │  │  Reward         │                       │
│  │  Contract       │  │  Distribution   │                       │
│  └─────────────────┘  └─────────────────┘                       │
└─────────────────────────────────────────────────────────────────┘
```

### User Flow

```
1. OPT-IN
   └── User toggles "Contribute Compute" switch
   └── Sets preferences (CPU %, active hours)
   └── Connects wallet for rewards

2. RECEIVE WORK
   └── Browser connects to Coordinator via WebSocket
   └── Receives task (ligand + receptor files)
   └── Downloads task data

3. COMPUTE
   └── Webina (WASM) runs docking in Web Worker
   └── Runs in background (doesn't block UI)
   └── Progress shown in platform UI

4. SUBMIT RESULTS
   └── Docking scores + poses sent to Coordinator
   └── Results verified (spot-checked for correctness)
   └── Recorded on-chain

5. EARN REWARDS
   └── Tokens credited based on compute contributed
   └── Can claim or reinvest in projects
```

### Task Distribution

**Challenge:** How to fairly distribute work and prevent cheating?

**Solution: Redundant Computation + Verification**

```
For each docking task:
1. Send same task to 3 random workers
2. Collect all 3 results
3. If 2/3 agree → accept result, reward those 2
4. If all 3 disagree → flag for manual review
5. Periodically re-verify random past results
```

**Anti-Gaming Measures:**
- Reputation scores (more accurate = more work)
- Random spot-checks with known-good results
- Rate limiting per browser session
- Proof of browser (prevent fake clients)

### Reward Economics

**Option A: Fixed Rate per Task**
```
1 docking run = 0.001 tokens
Average session: 100 dockings/hour = 0.1 tokens/hour
```

**Option B: Dynamic Pool**
```
Project deposits tokens into compute pool
Pool distributed proportionally to contributors
More contributors → smaller per-person reward (but faster results)
```

**Option C: Hybrid**
```
Base rate: Guaranteed minimum per compute unit
Bonus: Extra rewards from project-specific pools
Stake bonus: Higher rewards for token stakers
```

### Comparison to Alternatives

| Approach | Our Model | Golem/Akash | BOINC |
|----------|-----------|-------------|-------|
| **Install Required** | No (browser) | Yes | Yes |
| **Entry Barrier** | Very low | Medium | Low |
| **Compute Type** | Specific (docking) | General | Specific |
| **Payment** | Crypto tokens | Crypto tokens | None (volunteer) |
| **Verification** | Redundancy | Provider reputation | Volunteer trust |

---

## Implementation Roadmap

### Phase 1: Proof of Concept (Hackathon)

- [ ] Integrate Webina into platform UI
- [ ] Simple task queue (hardcoded test molecules)
- [ ] Mock reward display
- [ ] Demo: "Watch your browser dock molecules!"

### Phase 2: Basic Network

- [ ] WebSocket coordinator service
- [ ] Task distribution system
- [ ] Result collection + verification
- [ ] On-chain reward tracking
- [ ] User dashboard (tasks completed, earnings)

### Phase 3: Production

- [ ] Redundant verification system
- [ ] Reputation scores
- [ ] Multiple WASM modules (Vina, SMINA, etc.)
- [ ] Project-specific compute pools
- [ ] Auto-scaling task distribution

### Phase 4: Expansion

- [ ] GPU compute via WebGPU (when browser support matures)
- [ ] More scientific software ports
- [ ] Mobile browser support
- [ ] Desktop app for heavy contributors

---

## Technical Challenges

### 1. Browser Limitations
- **Memory:** WASM limited to 32-bit addresses (~4GB max)
- **CPU:** Single-threaded unless using Web Workers
- **Background:** Tabs throttled when not visible

**Mitigations:**
- Keep tasks small (<100MB memory)
- Use multiple Web Workers
- Tell users to keep tab visible, or use Service Workers

### 2. Verification
- **Problem:** How to know results are correct without redoing work?
- **Solution:** Redundant computation + spot-checking

### 3. Network Effects
- **Problem:** Need enough users to be useful
- **Solution:** Start with project communities, offer bonus rewards early

### 4. Task Granularity
- **Too small:** Network overhead dominates
- **Too large:** Users leave before completion
- **Sweet spot:** ~30 seconds to 5 minutes per task

---

## Why This is Perfect for Our Platform

### Natural Integration

1. **Projects need compute** → Create compute bounties
2. **Community members have browsers** → Earn while engaging
3. **Token has utility** → Pay for compute, earn for contributing
4. **Science gets done** → Actual molecules get docked

### Virtuous Cycle

```
Projects Fund Compute
        ↓
Users Contribute → Earn Tokens
        ↓
Users Stake/Vote → Govern Projects
        ↓
Projects Get Funded → Need More Compute
        ↓
(cycle continues)
```

### Unique Value Proposition

**For Projects:**
- Cheap distributed compute
- Pay only for results
- No cloud infrastructure to manage

**For Contributors:**
- Earn passive income
- Contribute to real science
- No special hardware needed

**For Platform:**
- Strong token utility
- User retention (earning = staying)
- Technical moat (competitors can't easily copy)

---

## Sources

### WebAssembly Scientific Computing
- [Nature: How WebAssembly is changing scientific computing](https://www.nature.com/articles/d41586-024-00725-1)
- [Webina Paper](https://academic.oup.com/bioinformatics/article/36/16/4513/5860016)
- [Webina GitHub](https://github.com/durrantlab/webina)

### Distributed Computing
- [Folding@Home Wikipedia](https://en.wikipedia.org/wiki/Folding@home)
- [BoomerangJS](https://www.boomerangjs.org/)
- [dis.io GitHub](https://github.com/tomgco/dis.io)

### Crypto Compute Networks
- [Golem Network](https://www.golem.network/)
- [Akash Network](https://akash.network/)
- [io.net Overview](https://www.coingecko.com/learn/what-is-io-net-io-token)

### Molecular Docking Software
- [AutoDock Vina](https://vina.scripps.edu/)
- [CCP4 Suite](https://www.ccp4.ac.uk/)
- [PHENIX](https://phenix-online.org/)
