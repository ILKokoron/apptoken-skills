# Apptoken Skills

Claude Code skills for the [Apptoken](https://apptokens.com) ecosystem — AI-assisted code generators and protocol knowledge bases covering Limit Break's Apptoken Standards and surrounding protocols. Generate ready-to-use Solidity contracts and Foundry scripts for LBAMM, Transfer Validator, TokenMaster, Payment Processor, Wrapped Native, PermitC, and Creator Token Standards.

## Installation

### Skills CLI

```bash
npx skills add limitbreakinc/apptoken-skills
```

### Claude Code Plugin

```bash
claude plugin marketplace add https://github.com/limitbreakinc/apptoken-skills
claude plugin install apptokens@apptoken-skills
```

### Manual

Clone and use as a plugin directory:

```bash
git clone https://github.com/limitbreakinc/apptoken-skills.git
claude --plugin-dir /path/to/apptoken-skills
```

Or copy skills into your project:

```bash
cp -r /path/to/apptoken-skills/skills/ your-project/.claude/skills/
```

## Available Skills

This repository contains **17 user-invocable skills** (code generators) and **8 protocol knowledge bases** spanning 7 protocol areas. Skills are invoked in Claude Code with a `/` prefix (e.g., `/lbamm-pool`).

| Category | Skills | Description |
|---|---|---|
| **Apptoken** | `apptoken-general`, `/apptoken-designer` | Foundation knowledge + design assistant that maps your idea to protocols and skills |
| **LBAMM** | 11 skills | Limit Break AMM — modular DEX with pluggable pool types and multi-tier hook system |
| **Transfer Validator** | 2 skills | Modular transfer validation with composable rulesets and list management |
| **TokenMaster** | 4 skills | Fungible token protocol for onchain consumer economies |
| **Payment Processor** | 3 skills | Peer-to-peer NFT trading with mandatory royalty enforcement |
| **Wrapped Native** | 2 skills | Gas-efficient WETH9 replacement with deterministic cross-chain deployment, permits, and payable ERC-20 |
| **PermitC** | 1 skill | Time-bound token approval system used across Payment Processor, LBAMM, and TokenMaster |

### Getting Started

**"I want to launch an apptoken"** — Start with `/apptoken-designer` and describe what you want. It maps your requirements to protocols and tells you which skills to use.

**"I need to integrate with a specific protocol"** — Jump directly to the relevant generator skill.

**"I have a question about how something works"** — Just ask. Knowledge base skills load automatically.

## LBAMM

| Skill | Type | Description |
|---|---|---|
| `lbamm-protocol` | Knowledge base | Architecture, interfaces, pool types, hooks, fees, execution model |
| `/lbamm-pool` | Generator | Pool creation code for Dynamic, Fixed, and Single Provider pools |
| `/lbamm-integrator` | Generator | DEX integration contracts (routers, aggregators, frontends) |
| `/lbamm-token-hook` | Generator | `ILimitBreakAMMTokenHook` implementations with 10 configurable flags |
| `/lbamm-pool-hook` | Generator | `ILimitBreakAMMPoolHook` implementations (dynamic fees, access control) |
| `/lbamm-position-hook` | Generator | `ILimitBreakAMMLiquidityHook` implementations (time locks, LP gating, deposit fees) |
| `/lbamm-standard-hook` | Generator | AMM Standard Hook configuration via Creator Hook Settings Registry |
| `lbamm-handler-protocol` | Knowledge base | Transfer handler architecture, custom handler development |
| `/lbamm-permit-handler` | Generator | PermitTransferHandler integration — gasless swaps via EIP-712 permits |
| `/lbamm-clob` | Generator | CLOBTransferHandler integration — on-chain limit order book |
| `/lbamm-test` | Generator | Foundry test suites following LBAMM test patterns |

## Transfer Validator

| Skill | Type | Description |
|---|---|---|
| `transfer-validator-protocol` | Knowledge base | V5 modular rulesets, list management, validation logic |
| `/transfer-validator-config` | Generator | Configuration scripts — rulesets, lists, whitelisting, account freezing |

**Rulesets:** Whitelist, Vanilla, Soulbound, Blacklist

## TokenMaster

| Skill | Type | Description |
|---|---|---|
| `tokenmaster-protocol` | Knowledge base | Architecture, data structures, pool types, fee distribution |
| `/tokenmaster-deployer` | Generator | Token deployment scripts with pool type selection and deterministic addressing |
| `/tokenmaster-integrator` | Generator | Transaction integration code — buy, sell, spend flows with EIP-712 signing |
| `/tokenmaster-hook` | Generator | Buy, sell, and spend hook contracts |

**Pool Types:** Standard (flexible tokenomics), Stable (fixed price), Promotional (no market value)

## Payment Processor

| Skill | Type | Description |
|---|---|---|
| `payment-processor-protocol` | Knowledge base | V3 NFT trading architecture, data structures, fee model |
| `/payment-processor-creator` | Generator | Creator configuration — payment settings, pricing, royalties, trusted channels |
| `/payment-processor-exchange` | Generator | Exchange integration — EIP-712 signing, order filling, PermitC, bulk orders |

## Wrapped Native

| Skill | Type | Description |
|---|---|---|
| `wrapped-native-protocol` | Knowledge base | Architecture, interfaces, permits, gas benchmarks, integration patterns |
| `/wrapped-native-integrator` | Generator | Integration contracts — wrapping, unwrapping, permits, gas sponsorship |

**Address:** `0x6000030000842044000077551D00cfc6b4005900` (deterministic, same on all EVM chains)

## PermitC

| Skill | Type | Description |
|---|---|---|
| `permitc-protocol` | Knowledge base | Time-bound approvals, permit transfers, order fills, nonce management, EIP-712 signing |

**Used by:** Payment Processor (NFT listings), LBAMM (gasless swaps), TokenMaster (advanced buy orders)

## Usage

Invoke any generator skill by name with a `/` prefix in Claude Code. Each generator produces complete, ready-to-use Solidity contracts and Foundry scripts — not snippets.

### Design First

Not sure where to start? Describe what you want and the designer will map it to protocols and skills:

```
/apptoken-designer I want a gaming currency that players earn through quests,
can spend in-game on items, and optionally trade on a DEX with a price floor
```

### Single Skills

```
/lbamm-pool Create a Dynamic pool for my ERC-20C token paired with WETH,
1 ETH initial liquidity, 1% swap fee
```

```
/transfer-validator-config Set up Whitelist ruleset for my token, add LBAMM
and TokenMaster as whitelisted operators
```

```
/tokenmaster-deployer Deploy a Standard pool token with WETH backing,
10% creator fee, deterministic address
```

```
/payment-processor-creator Configure my ERC-721C collection with 5% royalties,
ETH payments, and set floor price to 0.1 ETH
```

### Multi-Step Workflows

**Launch a tradeable apptoken with custom swap fees:**
```
1. /apptoken-designer Tradeable fungible token with 2% buy fee, 1% sell fee
2. /transfer-validator-config Whitelist LBAMM as an operator
3. /lbamm-token-hook Token hook that charges 2% on buys and 1% on sells
4. /lbamm-pool Dynamic pool for token/WETH with the custom hook
5. /lbamm-test Test suite for the pool and hook
```

**Deploy a backed token with a price floor:**
```
1. /tokenmaster-deployer Standard pool token with WETH backing and 5% creator fee
2. /transfer-validator-config Whitelist TokenMaster and LBAMM as operators
3. /lbamm-pool Dynamic pool so the token can also trade on the AMM
```

**Set up an NFT collection with royalty enforcement:**
```
1. /transfer-validator-config Whitelist ruleset — only approved marketplaces can transfer
2. /payment-processor-creator 7.5% royalties, ETH and WETH payments, cosigner required
3. /payment-processor-exchange EIP-712 signing code for marketplace integration
```

### Knowledge Bases

Knowledge base skills (`*-protocol`, `apptoken-general`) load automatically when you invoke a generator or ask protocol questions. You don't need to invoke them directly — just ask:

```
How does the LBAMM fee system work?
What transfer validator rulesets are available?
How do TokenMaster pool types differ?
```

## Repository Structure

```
.claude-plugin/
├── plugin.json                        # Plugin manifest
└── marketplace.json                   # Marketplace metadata
skills/
├── apptoken-general/                  # Foundation ecosystem knowledge
│   ├── SKILL.md
│   └── references/
├── apptoken-designer/                 # Apptoken design assistant
│   └── SKILL.md
├── lbamm-protocol/                    # AMM architecture reference
│   ├── SKILL.md
│   └── references/
├── lbamm-pool/                        # Pool creation generator
│   ├── SKILL.md
│   └── references/
├── lbamm-integrator/                  # DEX integration generator
│   ├── SKILL.md
│   └── references/
├── lbamm-token-hook/                  # Token hook generator
│   ├── SKILL.md
│   └── references/
├── lbamm-pool-hook/                   # Pool hook generator
│   ├── SKILL.md
│   └── references/
├── lbamm-position-hook/               # Position hook generator
│   ├── SKILL.md
│   └── references/
├── lbamm-standard-hook/              # Standard hook configurator
│   ├── SKILL.md
│   └── references/
├── lbamm-handler-protocol/            # Transfer handler architecture reference
│   ├── SKILL.md
│   └── references/
├── lbamm-permit-handler/              # Permit handler integration generator
│   ├── SKILL.md
│   └── references/
├── lbamm-clob/                        # CLOB handler integration generator
│   ├── SKILL.md
│   └── references/
├── lbamm-test/                        # Test suite generator
│   ├── SKILL.md
│   └── references/
├── transfer-validator-protocol/       # Validation protocol reference
│   ├── SKILL.md
│   └── references/
├── transfer-validator-config/         # Configuration generator
│   ├── SKILL.md
│   └── references/
├── tokenmaster-protocol/              # TokenMaster protocol reference
│   ├── SKILL.md
│   └── references/
├── tokenmaster-deployer/              # Token deployment generator
│   ├── SKILL.md
│   └── references/
├── tokenmaster-integrator/            # Transaction integration generator
│   ├── SKILL.md
│   └── references/
├── tokenmaster-hook/                  # Hook contract generator
│   ├── SKILL.md
│   └── references/
├── payment-processor-protocol/        # Trading protocol reference
│   ├── SKILL.md
│   └── references/
├── payment-processor-creator/         # Creator config generator
│   ├── SKILL.md
│   └── references/
├── payment-processor-exchange/        # Exchange integration generator
│   ├── SKILL.md
│   └── references/
├── wrapped-native-protocol/           # Wrapped Native protocol reference
│   ├── SKILL.md
│   └── references/
├── wrapped-native-integrator/         # Wrapped Native integration generator
│   ├── SKILL.md
│   └── references/
└── permitc-protocol/                  # PermitC approval system reference
    ├── SKILL.md
    └── references/
```

Each skill directory contains a `SKILL.md` definition file and supporting reference documentation (`.md` files) that provide protocol details, interface specifications, and annotated code patterns.

## Key Contract Addresses

| Contract | Address |
|---|---|
| Transfer Validator V5 | `0x721C008fdff27BF06E7E123956E2Fe03B63342e3` |
| EOA Registry | `0xE0A0004Dfa318fc38298aE81a666710eaDCEba5C` |
| Payment Processor V3 | `0x9a1D00000000fC540e2000560054812452eB5366` |
| TokenMaster Router | `0x0E00009d00d1000069ed00A908e00081F5006008` |
| Wrapped Native | `0x6000030000842044000077551D00cfc6b4005900` |
| PermitC | `0x000000fCE53B6fC312838A002362a9336F7ce39B` |

## Disclaimer

These skills are provided as development accelerators, not as a substitute for engineering diligence. AI-assisted code should always be carefully reviewed, tested, and audited before production deployment.
