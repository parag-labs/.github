# parag-labs

Small, focused tools for building systems you can actually trust in production -
verifiable retrieval, agent guardrails, drift and cost monitoring, rate limiting and
consensus, a few CI gates that turn "we should really check that" into "the build
fails if we don't," and - to tie it together - full-stack apps, a set of mobile and
on-device-AI apps, and the odd GPU visualization.

Most of these started as a problem I hit at work and couldn't find a clean, small
answer for, so I wrote one. Each project is real, tested code with a README that
explains the why - and, where it earns one, a design doc on the trade-offs and
benchmarks with actual numbers. Where something is a scaffold or a deliberate
shortcut, I say so instead of pretending it's production-grade.

A lot of the cores are written three times - Python, C#, and Java. That's not for
show: they're plain algorithms (a Merkle proof, a point-in-time join, a drift
statistic), and porting them keeps me honest that the logic is the logic, not a
trick of one language's libraries.

## Start here

New to all this? **[llm-in-production](https://github.com/parag-labs/llm-in-production)**
is the field guide that ties these tools together - short notes on the seven things
that will bite an LLM feature in production (cost, evals, prompt injection, drift,
grounding, rate limits, agent guardrails), each with the pattern that fixes it, a
runnable example, and a link to the tool below that implements it properly. If you
only read one file, read its pre-launch checklist.

## Projects

Grouped by what each thing *is*. Anything with a **[live demo]** runs in the browser -
no install. When a new repo ships, it goes under the right heading below.

<!-- PROJECTS:START -->

### AI agents & agent platforms

The LLM proposes and reasons; deterministic code validates and executes. Apps,
services, and runtimes for building, running, watching, and governing agents.

- **[agent-canvas](https://github.com/parag-labs/agent-canvas)** - a visual, type-safe platform for designing, running, debugging and evaluating ai-agent workflows - the llm proposes, deterministic code validates and executes
- **[AgentForge](https://github.com/parag-labs/agentforge-dashboard)** - register, monitor, and deeply compare ai agents - a seeded simulation engine, a comparison cockpit with radar + trade-off insights, and a spatial agent map, all in the browser ([live demo](https://parag-labs.github.io/agentforge-dashboard/))
- **[agent-trace](https://github.com/parag-labs/agent-trace)** - visual timeline and replay for agent runs: see where a run spent time, tokens, and money, then diff two runs ([live demo](https://parag-labs.github.io/agent-trace/))
- **[agent-run-dashboard](https://github.com/parag-labs/agent-run-dashboard)** - a small full-stack dashboard (fastapi + react) for recording ai agent runs and watching cost, tokens, and failures over time
- **[operations-agent](https://github.com/parag-labs/operations-agent)** - a multi-agent operations assistant - the planner proposes, deterministic code validates and executes, and dangerous actions wait for human approval (typescript, next.js, postgres)
- **[incident-commander](https://github.com/parag-labs/incident-commander)** - an autonomous incident-response agent in go - state machine, concurrent tools, a safety gate, mcp, and an eval harness, with the llm proposing and deterministic code executing
- **[infra-optimizer](https://github.com/parag-labs/infra-optimizer)** - an ai infrastructure optimizer in rust - rust computes and validates every plan and enforces every constraint; the llm only chooses among candidates already proven safe (property tests, criterion benchmarks, mcp)
- **[guardianforge](https://github.com/parag-labs/guardianforge)** - runtime governance for multi-agent systems, in go and c# - watch agent fleets, enforce policy, score anomalies and trust, intervene, and keep a hash-chained audit trail
- **[knowledge-workspace](https://github.com/parag-labs/knowledge-workspace)** - an evidence-grounded knowledge-graph workspace - the llm plans the query, deterministic code traverses the graph and cites its sources (graph rag with per-claim citations, typescript/next.js)
- **[meeting-execution](https://github.com/parag-labs/meeting-execution)** - turn meeting transcripts into decisions, owners, deadlines and executed actions - the llm extracts and proposes, deterministic code validates and executes, external actions wait for approval (typescript, next.js)
- **[mobile-assistant](https://github.com/parag-labs/mobile-assistant)** - an offline-first react native / expo ai life assistant - the ai proposes a plan, deterministic code fits it to your time window and reserves a travel buffer, with conflict-resolved sync

### LLM production tooling & guardrails

Small, drop-in libraries and CI gates for the unglamorous parts - grounding, cost,
quotas, injection, drift, breaking changes - each solving one problem well.

- **[LedgerRAG](https://github.com/parag-labs/ledger-rag)** - verifiable RAG with a tamper-evident cryptographic ledger - every answer ships a proof (python/c#/java, design doc + benchmarks)
- **[PromptShield](https://github.com/parag-labs/prompt-shield)** - firewall for llm apps: block prompt injection inbound, redact pii/secrets outbound
- **[AgentGuard](https://github.com/parag-labs/agent-guard)** - zero-trust runtime sandbox for tool-calling ai agents: least-privilege policy + signed audit log
- **[TokenLens](https://github.com/parag-labs/token-lens)** - attribute llm cost and latency to feature/tenant/model, with budget and anomaly gates (python/c#/java, design doc + benchmarks)
- **[QuotaGate](https://github.com/parag-labs/quota-gate)** - rate limiter for llm api traffic: per-model token & request budgets across sliding windows, per tenant/user scope, reserve-then-reconcile (python/c#/java, design doc + benchmarks)
- **[EvalForge](https://github.com/parag-labs/eval-forge)** - eval-driven ci gate for llm quality - fail the build when a prompt change regresses
- **[SchemaGuard](https://github.com/parag-labs/schema-guard)** - catch breaking api/schema changes at the pull request, not in production
- **[DriftWatch](https://github.com/parag-labs/drift-watch)** - data-drift detection (psi + kl-divergence) for ml monitoring, in three languages
- **[FeatureVault](https://github.com/parag-labs/feature-vault)** - a mini feature store with point-in-time-correct joins that never leak the future
- **[ChaosMeshLite](https://github.com/parag-labs/chaos-mesh-lite)** - resilience testing as a ci slo gate: inject faults, assert the slo still holds
- **[DeployKit](https://github.com/parag-labs/deploy-kit)** - one command to deploy an llm app into any cloud or on-prem, secure by default

### Mobile apps (Flutter)

On-device, privacy-first Flutter apps. The first six are interaction and UI concepts;
the last four put small, deterministic AI on the device. Each has a tested pure-Dart
core and runs live in the browser.

- **[IntentCanvas](https://github.com/parag-labs/intent-canvas)** - an intent-first mobile home: express a goal in plain language and get a living workspace of modules instead of an app grid, from a deterministic on-device intent engine ([live demo](https://parag-labs.github.io/intent-canvas/))
- **[MorphUI](https://github.com/parag-labs/morph-ui)** - a real-time generative interface engine: the ui continuously morphs its layout, density, and components between modes as context changes ([live demo](https://parag-labs.github.io/morph-ui/))
- **[DepthFlow](https://github.com/parag-labs/depth-flow)** - a spatial depth + soft-glass interface for flat screens: content on depth planes, pointer/tilt parallax, and depth-driven blur/scale/shadow - non-ar, 60fps ([live demo](https://parag-labs.github.io/depth-flow/))
- **[ThumbSphere](https://github.com/parag-labs/thumb-sphere)** - a thumb-zone-first design system: ambient content up top, all primary interaction in a curved bottom sphere along the natural thumb arc, with a tested reachability model ([live demo](https://parag-labs.github.io/thumb-sphere/))
- **[AuraSurface](https://github.com/parag-labs/aura-surface)** - an emotion-responsive visual language: the ui adapts tone, motion and density to on-device signals, subtly and transparently, with a tested affect engine ([live demo](https://parag-labs.github.io/aura-surface/))
- **[SenseGuard](https://github.com/parag-labs/sense-guard)** - an adaptive accessibility system: the ui transforms in real time across text, contrast, spacing, targets, motion and language, from a profile plus live conditions ([live demo](https://parag-labs.github.io/sense-guard/))
- **[AetherMesh](https://github.com/parag-labs/aether-mesh)** - on-device personal intelligence: local specialist agents (calendar, focus, comms, finance, health) collaborate on your intent and fuse a unified response ([live demo](https://parag-labs.github.io/aether-mesh/))
- **[VitalSwarm](https://github.com/parag-labs/vital-swarm)** - an on-device continuous health companion: multi-signal features, anomaly detection against personal baselines, and calm fused insights - fully local ([live demo](https://parag-labs.github.io/vital-swarm/))
- **[CrossForge](https://github.com/parag-labs/cross-forge)** - a privacy-respecting multi-device personal mesh: device discovery, secure pairing, and consent-gated context and task hand-off across your own devices ([live demo](https://parag-labs.github.io/cross-forge/))
- **[PolicyLens](https://github.com/parag-labs/policy-lens)** - a personal on-device ai governance layer: user-defined policies, allow/warn/block evaluation with explanations, and a readable audit trail ([live demo](https://parag-labs.github.io/policy-lens/))

### Distributed systems & algorithms

Weekend attempts to really understand the systems I rely on, by building the smallest
honest version of each - and, where the behavior is a plain algorithm, porting it
across languages to keep the logic honest.

- **[coracle](https://github.com/parag-labs/coracle)** - a small, readable raft consensus implementation - leader election + log replication with a deterministic simulator
- **[flotilla](https://github.com/parag-labs/flotilla)** - run thousands of independent raft consensus groups on one set of nodes - a shared scheduler instead of a thread per group, and cross-group rpc batching instead of an rpc per group
- **[ConsistentHash](https://github.com/parag-labs/consistent-hash)** - a consistent-hash ring with virtual nodes in three languages - minimal remap on membership change
- **[deterministic-sim-testing](https://github.com/parag-labs/deterministic-sim-testing)** - deterministic simulation testing for distributed code - replay any run from a single 64-bit seed, and shrink a failing fault schedule to a minimal reproducer (foundationdb / tigerbeetle style)
- **[durable-execution](https://github.com/parag-labs/durable-execution)** - durable execution - workflows written as ordinary code that survive crashes by replaying an append-only history, so a completed step never runs twice (temporal style)

### Graphics

- **[gpu-flock](https://github.com/parag-labs/gpu-flock)** - thousands of boids computed and rendered entirely on the gpu with webgpu compute shaders, with an automatic webgl2 fallback so it runs anywhere - zero dependencies, no build step ([live demo](https://parag-labs.github.io/gpu-flock/))

### Field notes

- **[llm-in-production](https://github.com/parag-labs/llm-in-production)** - field notes on shipping llm features you can trust: the seven problems that bite in production, each with a pattern, a runnable example, and the tool that fixes it - plus a pre-launch checklist

<!-- PROJECTS:END -->

Also maintained, outside this org: **[flatwire](https://github.com/flatwire-io/flatwire)** -
streaming serialization that keeps memory flat and time linear, with one identical API
across Python, Node, .NET, Rust, Go, and Java (published to PyPI, npm, crates.io, NuGet,
Maven Central, and Go).

## What you'll find in each repo

- **A README that explains the why**, not just the how - the problem it solves and
  where it stops.
- **Tests that actually assert the hard part** - and, for the systems repos, chaos or
  stress suites that prove behavior under partitions, packet loss, memory pressure,
  and out-of-order input.
- **A [DESIGN.md](https://github.com/parag-labs/token-lens/blob/main/DESIGN.md) where the
  design has trade-offs worth defending** - constraints, decisions, and explicit
  non-goals.
- **BENCHMARKS.md with real, reproducible numbers** where performance is a claim -
  measured on a plain machine from a committed script, with graphs, compared against
  an honest baseline (e.g. consistent hashing vs `hash % N`, a bounded window vs an
  exact log).

## Running things

Most repos follow the same shape, so the commands are predictable:

- **Python libraries / cores:** `pip install -r requirements.txt` (or `pip install
  pytest`) then `pytest -q`.
- **Tri-language cores** (Merkle proofs, rings, limiters, drift stats): the same
  behavior in three languages - `pytest -q`, `dotnet test` (.NET 10), and `mvn test`
  (JDK 17+).
- **Web / UI** (e.g. agent-trace): `npm ci` then `npm run dev` for the app, `npm test`
  for the suite, `npm run build` for a static bundle. Some ship a live demo on GitHub
  Pages.
- **Flutter apps:** `flutter pub get`, then `flutter test` for the suite and
  `flutter run` for the app (`-d chrome` for web). Each also ships a live demo on
  GitHub Pages.
- **Benchmarks**, where a repo has them: `pip install -r bench/requirements.txt` then
  `python bench/benchmark.py`, which writes graphs and a JSON summary under
  `bench/results/`.

## Contact

Parag Sawant - [linkedin.com/in/paragsawant](https://www.linkedin.com/in/paragsawant/)
