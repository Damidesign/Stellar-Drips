StellarDrips 💧The real-time, linear asset streaming protocol for the Drips Stellar Wave.StellarDrips is a decentralized, non-custodial protocol built on Soroban. It transforms static balances into "Liquid Flows," allowing assets to drip from senders to receivers second-by-second based on the Stellar ledger timestamp.moving away from traditional lump-sum payments to provide instant liquidity for the Stellar ecosystem.🌊 The Concept: Money as a FluidTraditional payments are "frozen" blocks. StellarDrips treats capital as a fluid. Once a "Drip" is initialized, the Soroban smart contract unlocks a precise portion of funds every time a new ledger is closed.The Drip FormulaThe contract calculates the Claimable Flow using high-precision fixed-point math:$$Claimable = \frac{TotalAmount \times (CurrentTime - StartTime)}{EndTime - StartTime}$$CurrentTime: The timestamp of the latest ledger.StartTime: The moment the flow is activated.EndTime: The moment the drip reaches its total capacity.✨ Key Features1. Continuous LiquidityRecipients don't wait for "payday." They can trigger the withdraw function at any time to collect the accumulated drips accrued up to that exact ledger.2. Programmable Flow ControlTotal control for both parties:Sender: Can pause or cancel the drip, reclaiming unspent "future" funds instantly.Recipient: Receives the exact pro-rated amount earned up to the millisecond of cancellation.3. Native Stellar Asset IntegrationBuilt on the Soroban Token Interface, we support any SAC-compliant token:Stablecoins: USDC, BRLG, ARST.Network Assets: Native XLM (via Wrapped XLM contract).🛠 Project ArchitectureThis monorepo is structured to separate the core "Drip" logic from the analytics and user interface.Directory MappingPlaintextStellarDrips/
├── contracts/               # THE LIQUIDITY ENGINE (Rust + Soroban)
│   ├── src/
│   │   ├── lib.rs           # Drip entry points (init, withdraw, stop)
│   │   ├── types.rs         # Flow state and User profiles
│   │   ├── math.rs          # Fixed-point precision for flow rates
│   │   └── validation.rs    # Auth and ledger bounds enforcement
│
├── frontend/                # THE FLOW DASHBOARD (Next.js 14)
│   ├── src/
│   │   ├── components/      # "Live-Ticking" balance counters
│   │   ├── hooks/           # Soroban-Client & Freighter integration
│   │   └── store/           # Zustand state for active drips
│
├── backend/                 # THE FLOW-INDEXER (Node.js + TS)
│   ├── src/
│   │   ├── indexer/         # Listening for Drip events on-chain
│   │   └── api/             # Aggregated stats for the "Drip Feed"
│
└── docs/                    # Wave-specific specs and pitch deck
