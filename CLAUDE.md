# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Qubic hackathon project** building a Discord-style platform for funding and collaborating on biochemistry projects. The unique feature is browser-based distributed computing using Webina (AutoDock Vina compiled to WebAssembly) - users can earn tokens by contributing CPU cycles for molecular docking calculations.

**Hackathon**: https://lablab.ai/event/qubic-hack-the-future

## Repository Structure

```
qubic/
├── test-webina/     # Webina molecular docking web app (Vue.js + TypeScript)
└── docs/            # Project documentation and specifications
    ├── IDEA.md      # Project vision
    ├── SPEC.md      # Full platform specification
    └── RESEARCH-*.md # Technical research documents
```

## Webina Application (test-webina/)

### Tech Stack
- **Language**: TypeScript 5.0.4
- **Framework**: Vue.js 2.6.11 + Vuex 3.1.3
- **UI**: Bootstrap Vue 2.11.0
- **Build**: Webpack 5.85.0 + Google Closure Compiler
- **3D Visualization**: 3Dmol.js
- **Molecular Editor**: Kekule.js

### Build Commands

```bash
cd test-webina
npm install
npm start          # Development server with hot reload
npm run build      # Production build (requires 4GB memory)
```

### Source Architecture

```
test-webina/src/
├── index.ts                    # Entry point
├── Vue/
│   ├── Store.ts               # Vuex state (docking params, results)
│   └── Setup.ts               # Vue initialization
├── UI/
│   ├── Tabs/                  # Main workflow tabs
│   │   ├── VinaParams.ts      # Input parameters
│   │   ├── VinaOutput.ts      # Results display
│   │   └── VinaRunning.ts     # Progress tracking
│   ├── Forms/                 # Form components
│   ├── Modal/                 # Dialog boxes
│   ├── ThreeDMol.ts          # 3D structure viewer
│   └── UI.ts                  # Main orchestrator
├── Webina/
│   └── Webina.ts             # AutoDock Vina WASM interface
├── pdbqt_convert/            # File format conversion
└── mol_editor/               # 2D→3D structure editor
```

### Key Technical Notes

- Uses `SharedArrayBuffer` for multi-threaded WebAssembly - requires COOP/COEP headers
- **Browser requirement**: Chromium-based (Chrome, Edge, Brave)
- All docking runs locally in browser - no data sent to servers
- Production build output goes to `dist/`

## Platform Vision (docs/SPEC.md)

The full platform will include:
- Discord-style project servers with real-time chat
- Quadratic funding and conviction voting
- Revenue sharing via smart contracts
- **Distributed compute network**: Users contribute CPU for molecular docking and earn Qubic tokens

### Compute Flow
1. Projects upload ligand libraries + receptor structures
2. Compute Coordinator distributes tasks via WebSocket
3. Browser workers run Webina (WASM) docking
4. Results verified by redundant computation (2/3 agreement)
5. Workers receive token rewards

## Development Focus

For the hackathon MVP:
1. Basic Discord-style UI shell
2. Project creation and discovery
3. Wallet connection (Qubic)
4. **Webina compute integration** - the key demo feature
5. Mock earnings counter showing token rewards
