

Notes:
- Includes **adjacent infra/tooling** when explicitly named in memos.
- Includes relevant (but not private) defi project

| Project / system                         | One-line description (from memos)                                                                                    | Rough category                 |
| ---------------------------------------- | -------------------------------------------------------------------------------------------------------------------- | ------------------------------ |
| **Aave**                                 | Public lending protocol referenced as a target for private overlays / private-mode integrations.                     | Lending protocol               |
| **Arbitrum**                             | Referenced as a target rollup in a boundary example (“private bridging … to Arbitrum”).                              | L2 rollup                      |
| **Astria**                               | Named as a shared sequencer option enabling cross-rollup atomic actions + privacy-aware ordering.                    | Shared sequencer               |
| **Aztec**                                | Ethereum-aligned privacy L2 (Noir/“Ignition” mentioned); natural home for private swaps/lending/liquidations.        | Privacy-native L2              |
| **Aztec Connect**                        | (Past) connector/overlay model for private calls into public L1 DeFi; referenced as “Connect-like overlays.”         | Overlay / connectors           |
| **Celestia**                             | Modular DA layer named as enabling cheap app-specific rollups (“rollup-as-a-service stacks”).                        | DA / modular infra             |
| **CowSwap**                              | Referenced as MEV-protected / partially obfuscated batch auctions (privacy-adjacent execution).                      | DEX / batch auctions           |
| **EigenDA**                              | Modular DA mentioned as enabling cheap app-specific rollups (“rollup-as-a-service stacks”).                          | DA / modular infra             |
| **ERC-4337**                             | Account abstraction standard cited alongside stealth/meta-address infra for per-write privacy / unlinkability.       | Wallet / AA infra              |
| **Espresso**                             | Named as a shared sequencer option for cross-rollup atomicity and privacy-aware ordering.                            | Shared sequencer               |
| **Flashbots**                            | Mentioned as MEV/orderflow infra (PBS/SUAVE context; infra, not “DeFi writes”).                                      | MEV / orderflow infra          |
| **GMX**                                  | Used as example of “GMX-style perps” in-scope when decomposed into collateral + swap + liquidation.                  | Perps / margin DEX             |
| **Halo2**                                | Named as ZK proving / circuit tooling shaping feasibility and developer workflow for private DeFi.                   | ZK tooling                     |
| **Incognito pDEX**                       | Example of cross-chain shielded DEXes / privacy overlays (“Incognito pDEX / similar”).                               | Shielded DEX / overlay         |
| **Kohaku (meta-address infra)**          | Wallet toolchains / stealth meta-address patterns enabling per-write and cross-write unlinkability.                  | Wallet / stealth infra         |
| **Lido**                                 | Mentioned in a boundary example (“private staking of ETH into Lido for stETH”).                                      | LSD / staking                  |
| **Manta Network**                        | Polkadot parachain offering private transfers + private DEX using zkSNARKs.                                          | Privacy chain / DEX            |
| **Matter Labs**                          | Mentioned around prototype zk-lending systems targeting private collateral & debt (plus academic prototypes).        | ZK/L2 org / prototypes         |
| **MEV-Share**                            | Named as “MEV-share / private auction-style orderflow relays” in the infra cluster.                                  | MEV / orderflow infra          |
| **MEV-PBS / PBS**                        | Mentioned as MEV/PBS research relevant to private orderflow envelope (infra, not DeFi writes).                       | MEV / block-building infra     |
| **Namada**                               | Multi-asset shielded pool + privacy-preserving bridge hub; framed as important for cross-domain unlinkability.       | Privacy chain / bridge hub     |
| **Noir**                                 | Named as ZK dev tooling (language/framework) likely to shape what private DeFi circuits are feasible.                | ZK tooling                     |
| **Oasis Sapphire / Oasis Privacy Layer** | Confidential EVM infra via TEEs (“sidecar confidentiality” approach for existing EVM DeFi).                          | Confidential EVM / TEE infra   |
| **Obscuro / TEN**                        | Ethereum L2 using TEEs for confidential smart contract execution; targets MEV reduction and state privacy.           | Confidential L2 / TEE          |
| **OP Stack**                             | Named as part of rollup-as-a-service stacks enabling app-specific rollups (incl. privacy variants).                  | Rollup stack                   |
| **Panther Protocol**                     | Cross-chain z-asset burn-and-mint system with compliance/selective disclosure hook.                                  | z-asset / privacy asset system |
| **Penumbra**                             | Cosmos app-chain implementing a fully private DEX + staking; showcases default-shielded AMM + LP writes.             | Privacy app-chain / DEX        |
| **Plonky2**                              | Named as “better proving systems” shaping whether private DeFi bundles are practical on consumer hardware.           | ZK tooling                     |
| **Polygon CDK**                          | Named as part of rollup-as-a-service stacks enabling app-specific rollups.                                           | Rollup stack                   |
| **Polygon Nightfall**                    | Hybrid optimistic/ZK rollup focused on enterprise private transfers; noted as capable of hosting private DeFi flows. | L2 rollup                      |
| **Polygon zkEVM**                        | Cited as a maturing zkEVM environment making zk-proved DeFi writes cheaper.                                          | L2 zkEVM                       |
| **Railgun**                              | ZK shielded pool / overlay enabling private DeFi interactions via adapters/relayers into public protocols.           | Shielded pool / overlay        |
| **Scroll**                               | Cited as a maturing zkEVM environment making zk-proved DeFi writes cheaper.                                          | L2 zkEVM                       |
| **Secret Bridge**                        | Mentioned as a bridge example for moving assets into Secret’s private token environment.                             | Bridge                         |
| **Secret Network**                       | TEE-based privacy chain where DeFi dApps run with encrypted state (AMM, lending, stablecoin).                        | Privacy chain / TEE            |
| **Shade Lending**                        | Secret Network DeFi app named as an example of private lending / leverage / liquidations cluster.                    | Lending dApp                   |
| **Shade Swap**                           | Secret Network DeFi app named as an example DEX/AMM (Shade).                                                         | DEX dApp                       |
| **Shutter Network**                      | Threshold-encrypted mempools / encrypted orderflow infra to reduce pre-trade leakage and sandwiching.                | Encrypted orderflow infra      |
| **SiennaSwap**                           | Secret Network DeFi app named as an example DEX/AMM (Sienna).                                                        | DEX dApp                       |
| **StarkNet**                             | Cited as a maturing zk-rollup environment; also referenced as hosting privacy dApps.                                 | L2 zk-rollup                   |
| **SUAVE (Flashbots)**                    | “SUAVE-style architectures” / private orderflow relays cited as key orderflow privacy infrastructure.                | MEV / orderflow infra          |
| **Uniswap**                              | Public AMM referenced as an underlying liquidity target for privacy overlays/adapters.                               | AMM / DEX                      |
| **Yearn**                                | Referenced as yield aggregator example for private deposit flows (entry/exit privacy).                               | Vault / aggregator             |
| **Zcash ecosystem**                      | Named as a non-Ethereum privacy ecosystem relevant for coordination and bridging experiments.                        | Privacy ecosystem              |
| **zkSync Era**                           | Cited as a maturing zk-rollup environment; also referenced as hosting privacy dApps.                                 | L2 zk-rollup                   |
