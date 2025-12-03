# Platform Specification

## Vision

A Discord-style platform for funding, collaborating on, and commercializing biochemistry projects. Born from the "How To Grow Almost Anything" community - makers and researchers with commercially viable ideas who need funding, collaborators, and a path to market.

---

## Problem Statement

### Current Pain Points

1. **Funding Gap**: Early-stage biotech ideas struggle to get traditional VC/grant funding
2. **Collaboration Friction**: Researchers use scattered tools (email, Slack, Google Docs)
3. **IP Uncertainty**: Unclear ownership when multiple contributors are involved
4. **No Path to Market**: Great ideas die because creators don't know how to commercialize
5. **Investor Access**: Regular people can't invest in early-stage science

### Why Existing Solutions Fall Short

| Solution | Limitation |
|----------|-----------|
| VitaDAO/BioDAOs | Specialized focus (longevity, hair, etc.) |
| Experiment.com | No ongoing collaboration, one-time funding |
| Discord | No funding/revenue mechanics |
| Traditional grants | Slow, bureaucratic, no community |

---

## Solution Overview

### Core Concept

Each project gets its own "server" (like Discord) with:
- Real-time chat channels
- Integrated funding
- Built-in governance
- Revenue sharing when products sell

### Key Differentiators

1. **Discord UX** - Familiar interface, real-time engagement
2. **General Purpose** - Not limited to one research area
3. **Full Lifecycle** - Idea → Funding → Development → Product → Revenue
4. **Inclusive** - Makers + researchers + hobbyists (not just academics)
5. **Simple Onboarding** - Lower barrier than typical DAOs
6. **Browser-Based Compute** - Earn tokens by contributing CPU for molecular modeling (unique feature!)

---

## User Personas

### 1. Project Creator
**"I have a cool biotech idea from HTGAA that could be commercial"**
- Wants to share idea and get feedback
- Needs funding to prototype/develop
- Looking for collaborators with complementary skills
- Wants fair compensation if product succeeds

### 2. Funder/Investor
**"I want to support interesting science and share in upside"**
- Interested in specific research areas
- Willing to contribute small-medium amounts
- Wants transparency on how funds are used
- Expects returns if project commercializes

### 3. Contributor
**"I have skills to offer and want to work on cool projects"**
- Scientist, engineer, designer, marketer
- Wants meaningful work outside day job
- Expects compensation (tokens/equity)
- Values community and learning

### 4. Community Member
**"I want to follow interesting projects and participate"**
- Curious about biotech/science
- Engages in discussions
- May fund small amounts
- Helps spread the word

### 5. Compute Contributor
**"I want to earn passive income while helping science"**
- Has a computer/browser they leave open
- Wants easy way to contribute to research
- Interested in earning tokens without active work
- May not have money to invest, but has CPU cycles

---

## Features

### Phase 1: MVP (Hackathon)

#### Project Servers
- [ ] Create new project (name, description, category)
- [ ] Project "server" with channels (general, announcements, research, etc.)
- [ ] Real-time chat (Discord-style)
- [ ] Project info sidebar (description, team, funding status)
- [ ] Public/private channels

#### Discovery
- [ ] Browse all projects
- [ ] Filter by category (lab equipment, bio products, consumer, etc.)
- [ ] Search projects
- [ ] Featured/trending projects

#### Basic Funding
- [ ] Display funding goal and progress
- [ ] Contribution button (mock for hackathon)
- [ ] Contributor list with amounts
- [ ] Funding milestones display

#### User Profiles
- [ ] Wallet connection
- [ ] Basic profile (name, bio, avatar)
- [ ] Projects created/joined/funded

### Phase 2: Post-Hackathon

#### Quadratic Funding
- [ ] Funding rounds (time-boxed)
- [ ] Matching pool display
- [ ] QF formula implementation
- [ ] Round results visualization

#### Conviction Voting
- [ ] Stake tokens on projects
- [ ] Conviction accumulation over time
- [ ] Threshold-based allocation
- [ ] Real-time conviction display

#### Governance
- [ ] Create proposals
- [ ] Quadratic voting for major decisions
- [ ] Snapshot integration or native voting
- [ ] Proposal history

### Phase 3: Full Platform

#### IP-NFT Integration
- [ ] Mint IP-NFT for project IP
- [ ] Fractionalize into project tokens
- [ ] Token holder governance
- [ ] Licensing workflow

#### Revenue Distribution
- [ ] Smart contract revenue splits
- [ ] Automatic distribution to token holders
- [ ] Revenue dashboard
- [ ] Claim/withdraw interface

#### Milestones & Verification
- [ ] Define project milestones
- [ ] Oracle integration for verification
- [ ] Milestone-based fund release
- [ ] Progress tracking

#### Distributed Compute Network
- [ ] Webina (AutoDock Vina WASM) integration
- [ ] Compute opt-in UI with settings
- [ ] Task distribution via WebSocket
- [ ] Result verification (redundant computation)
- [ ] Reward tracking and claiming
- [ ] Project-specific compute pools
- [ ] Compute contributor leaderboards
- [ ] Multiple WASM modules (Vina, SMINA, etc.)

---

## Technical Architecture

### High-Level Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                         FRONTEND                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐  │
│  │   Project   │  │  Discovery  │  │      Funding        │  │
│  │   Server    │  │   & Search  │  │    Dashboard        │  │
│  │   (Chat)    │  │             │  │                     │  │
│  └─────────────┘  └─────────────┘  └─────────────────────┘  │
│                                                              │
│  ┌─────────────────────────────────────────────────────┐    │
│  │              COMPUTE WORKER (Web Worker)             │    │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  │    │
│  │  │   Webina    │  │   Task      │  │   Results   │  │    │
│  │  │   (WASM)    │  │   Manager   │  │   Reporter  │  │    │
│  │  └─────────────┘  └─────────────┘  └─────────────┘  │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                              │
│  Tech: React/Next.js + WebSocket + Web Workers              │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                         BACKEND                              │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐  │
│  │    API      │  │   WebSocket │  │   Indexer           │  │
│  │   Server    │  │   Server    │  │   (Blockchain)      │  │
│  └─────────────┘  └─────────────┘  └─────────────────────┘  │
│                                                              │
│  ┌─────────────────────────────────────────────────────┐    │
│  │              COMPUTE COORDINATOR                     │    │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  │    │
│  │  │   Task      │  │   Result    │  │   Reward    │  │    │
│  │  │   Queue     │  │   Verifier  │  │   Calculator│  │    │
│  │  └─────────────┘  └─────────────┘  └─────────────┘  │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                              │
│  Tech: Node.js/Python + PostgreSQL + Redis                  │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                      QUBIC BLOCKCHAIN                        │
│                                                              │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐   │
│  │   Project    │  │   Funding    │  │    Revenue       │   │
│  │   Registry   │  │   Pool       │  │    Splitter      │   │
│  │   Contract   │  │   Contract   │  │    Contract      │   │
│  └──────────────┘  └──────────────┘  └──────────────────┘   │
│                                                              │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐   │
│  │  Conviction  │  │   Quadratic  │  │    Compute       │   │
│  │   Voting     │  │   Voting     │  │    Rewards       │   │
│  └──────────────┘  └──────────────┘  └──────────────────┘   │
│                                                              │
│  Tech: C++ Smart Contracts + Qubic Oracles                  │
└─────────────────────────────────────────────────────────────┘
```

### Smart Contract Architecture

#### 1. Project Registry Contract
```
Functions:
- createProject(name, description, creator)
- updateProject(projectId, updates)
- getProject(projectId)
- listProjects(filters)

State:
- projects: Map<ProjectId, Project>
- projectCount: uint64
```

#### 2. Funding Pool Contract
```
Functions:
- contribute(projectId, amount)
- withdrawContribution(projectId)  // if goal not met
- releaseFunds(projectId, milestone)  // milestone-based
- getContributions(projectId)

State:
- contributions: Map<ProjectId, Map<Address, Amount>>
- fundingGoals: Map<ProjectId, Goal>
- fundingStatus: Map<ProjectId, Status>
```

#### 3. Conviction Voting Contract
```
Functions:
- stake(projectId, amount)
- unstake(projectId, amount)
- getConviction(projectId)
- allocateFunds()  // called periodically

State:
- stakes: Map<ProjectId, Map<Address, StakeInfo>>
- convictionScores: Map<ProjectId, Score>
- lastUpdate: Map<ProjectId, Timestamp>
```

#### 4. Revenue Splitter Contract
```
Functions:
- receiveRevenue(projectId)  // payable
- claimShare(projectId)
- getSplit(projectId)

State:
- splits: Map<ProjectId, SplitConfig>
- balances: Map<ProjectId, Map<Address, Balance>>
- totalRevenue: Map<ProjectId, Amount>
```

#### 5. Compute Rewards Contract
```
Functions:
- createComputePool(projectId, amount)  // project funds compute
- submitWorkProof(taskId, resultHash, worker)
- verifyAndReward(taskId, workers[])  // coordinator calls after verification
- claimComputeRewards()
- getComputeStats(worker)

State:
- computePools: Map<ProjectId, PoolBalance>
- pendingRewards: Map<Address, Amount>
- workerStats: Map<Address, {tasksCompleted, totalRewards}>
- taskResults: Map<TaskId, {resultHash, workers[], verified}>
```

### Database Schema (Off-chain)

```sql
-- Projects
CREATE TABLE projects (
  id UUID PRIMARY KEY,
  chain_id VARCHAR,  -- Qubic contract reference
  name VARCHAR NOT NULL,
  description TEXT,
  category VARCHAR,
  creator_address VARCHAR NOT NULL,
  created_at TIMESTAMP
);

-- Channels
CREATE TABLE channels (
  id UUID PRIMARY KEY,
  project_id UUID REFERENCES projects(id),
  name VARCHAR NOT NULL,
  type VARCHAR,  -- 'text', 'announcement', 'governance'
  is_public BOOLEAN DEFAULT true
);

-- Messages
CREATE TABLE messages (
  id UUID PRIMARY KEY,
  channel_id UUID REFERENCES channels(id),
  sender_address VARCHAR NOT NULL,
  content TEXT,
  created_at TIMESTAMP
);

-- Users
CREATE TABLE users (
  address VARCHAR PRIMARY KEY,
  username VARCHAR,
  bio TEXT,
  avatar_url VARCHAR
);

-- Memberships
CREATE TABLE memberships (
  user_address VARCHAR REFERENCES users(address),
  project_id UUID REFERENCES projects(id),
  role VARCHAR,  -- 'creator', 'contributor', 'member'
  joined_at TIMESTAMP,
  PRIMARY KEY (user_address, project_id)
);
```

---

## User Flows

### Flow 1: Create a Project

```
1. User connects wallet
2. Clicks "Create Project"
3. Fills form:
   - Project name
   - Description
   - Category
   - Funding goal
   - Milestones
4. Submits → Creates on-chain record
5. Project "server" created with default channels
6. User becomes project admin
```

### Flow 2: Fund a Project

```
1. User browses/searches projects
2. Clicks into project server
3. Reviews project info, chat history
4. Clicks "Fund" button
5. Enters contribution amount
6. Confirms transaction
7. Receives project tokens proportionally
8. Shows as contributor in project
```

### Flow 3: Contribute Work

```
1. User joins project server
2. Discusses in channels
3. Proposes contribution (code, research, design)
4. Project team reviews
5. Work merged/accepted
6. User receives tokens for contribution
7. Shown as contributor with role
```

### Flow 4: Receive Revenue

```
1. Project launches product
2. Sales revenue flows to Revenue Splitter contract
3. User sees "Claimable Balance" in dashboard
4. Clicks "Claim"
5. Receives proportional share based on tokens held
```

### Flow 5: Contribute Compute (Earn by Docking)

```
1. User toggles "Contribute Compute" switch in navbar
2. Sets preferences:
   - CPU usage (25%, 50%, 75%, 100%)
   - Active hours (always, or specific times)
3. Connects wallet for rewards
4. Browser connects to Compute Coordinator via WebSocket
5. Receives docking task (ligand + receptor files)
6. Webina (WASM) runs docking in Web Worker
7. Progress indicator shows in corner of screen
8. Results submitted to Coordinator
9. Same task sent to 2 other workers for verification
10. If 2/3 results agree → task verified → rewards credited
11. User sees earnings accumulate in real-time
12. Can claim rewards anytime
```

### Flow 6: Request Compute (Project Needs Docking)

```
1. Project needs virtual screening (dock 10,000 ligands)
2. Project admin goes to "Compute" tab in project server
3. Uploads ligand library + receptor structure
4. Sets reward pool (e.g., 1000 tokens for the job)
5. Compute Coordinator breaks into individual tasks
6. Tasks distributed to available workers
7. Results stream back as completed
8. Project admin downloads results (scores + poses)
9. Can filter/sort by docking score
```

---

## Token Economics

### Platform Token ($GROW or similar)

**Utility:**
- Governance voting (platform-level decisions)
- Matching pool participation
- Staking for conviction voting
- Platform fee discounts
- **Pay for distributed compute** (projects buy compute with tokens)
- **Earn from compute contribution** (contributors receive tokens)

**Distribution:**
- Community sale/airdrop: 35%
- Team & contributors: 20%
- Treasury: 20%
- Ecosystem grants: 15%
- **Compute rewards pool: 10%** (reserved for early compute contributors)

### Project Tokens

Each project has its own token representing:
- Governance rights for that project
- Revenue share when commercialized
- Proof of contribution/funding

**Minting:**
- On funding: tokens to funders (proportional to contribution)
- On contribution: tokens to contributors (value of work)
- Creator allocation: set at project creation

---

## Hackathon Scope

### What We'll Build (3 Days)

**Day 1:**
- [ ] Project structure setup
- [ ] Basic UI shell (Discord-style layout)
- [ ] Project creation flow (mock)
- [ ] Channel/chat UI (mock data)

**Day 2:**
- [ ] Discovery/browse page
- [ ] Wallet connection
- [ ] Funding display
- [ ] **Integrate Webina WASM library**
- [ ] **Basic "Contribute Compute" toggle**

**Day 3:**
- [ ] **Compute demo: show docking running in browser**
- [ ] **Mock earnings counter**
- [ ] Polish UI/UX
- [ ] Demo video
- [ ] Pitch deck
- [ ] Documentation

### Demo Scenario

**Part 1: Project Journey**
Show "Project: Enzyme for Plastic Degradation":
1. Creator posts idea
2. Community discusses in channels
3. Project enters funding round
4. Multiple small contributors fund it
5. Quadratic matching amplifies funding
6. Project hits goal

**Part 2: Compute Demo (The WOW Factor)**
7. Project needs to screen 1000 compounds for enzyme binding
8. Toggle "Contribute Compute" → Watch docking run live in browser
9. See earnings counter tick up as you contribute
10. Show molecule visualization of docking results
11. "Your browser just helped discover a potential plastic-eating enzyme!"

---

## Open Questions

1. **Identity**: How do we handle Sybil resistance for quadratic funding?
2. **Moderation**: Who moderates project channels? How?
3. **Disputes**: What happens if project fails or creator disappears?
4. **Legal**: IP ownership, securities regulations
5. **Qubic Integration**: How mature are Qubic smart contracts for our needs?
6. **Compute Verification**: How to efficiently verify results without redoing all work?
7. **Task Sizing**: What's the optimal docking task size for browser workers?
8. **Browser Limitations**: How to handle tab throttling when not in focus?

---

## Success Metrics

### Hackathon Success
- Working demo of core UX
- Clear value proposition communicated
- Technical architecture documented
- Positive judge feedback
- **Compute demo running live in browser**

### Long-term Success
- Number of projects created
- Total funding raised
- Products launched to market
- Revenue distributed to contributors
- Community growth (DAU/MAU)
- **Compute contributors (active browsers)**
- **Docking tasks completed**
- **Total compute rewards distributed**

---

## Next Steps

1. **Finalize tech stack** for hackathon
2. **Create wireframes** for core flows
3. **Set up project repo** with boilerplate
4. **Divide tasks** among team
5. **Build MVP** during hackathon
6. **Pitch and iterate** based on feedback
