# parag-labs

Small, focused tools for building systems you can actually trust in production -
verifiable retrieval, agent guardrails, drift and cost monitoring, rate limiting and
consensus, a few CI gates that turn "we should really check that" into "the build
fails if we don't," and the odd full-stack app, UI, or GPU visualization to tie it
together.

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

<!-- PROJECTS:START -->
<!-- The list below grows as repositories are published. Keep it flat: the publisher appends one bullet here per new repo. -->
- **[llm-in-production](https://github.com/parag-labs/llm-in-production)** - field notes on shipping llm features you can trust: the seven problems that bite in production, each with a pattern, a runnable example, and the tool that fixes it - plus a pre-launch checklist
- **[LedgerRAG](https://github.com/parag-labs/ledger-rag)** - verifiable RAG with a tamper-evident cryptographic ledger - every answer ships a proof (python/c#/java, design doc + benchmarks)
- **[EvalForge](https://github.com/parag-labs/eval-forge)** - eval-driven ci gate for llm quality - fail the build when a prompt change regresses
- **[SchemaGuard](https://github.com/parag-labs/schema-guard)** - catch breaking api/schema changes at the pull request, not in production
- **[AgentGuard](https://github.com/parag-labs/agent-guard)** - zero-trust runtime sandbox for tool-calling ai agents: least-privilege policy + signed audit log
- **[TokenLens](https://github.com/parag-labs/token-lens)** - attribute llm cost and latency to feature/tenant/model, with budget and anomaly gates (python/c#/java, design doc + benchmarks)
- **[QuotaGate](https://github.com/parag-labs/quota-gate)** - rate limiter for llm api traffic: per-model token & request budgets across sliding windows, per tenant/user scope, reserve-then-reconcile (python/c#/java, design doc + benchmarks)
- **[agent-trace](https://github.com/parag-labs/agent-trace)** - visual timeline and replay for agent runs: see where a run spent time, tokens, and money, then diff two runs ([live demo](https://parag-labs.github.io/agent-trace/))
- **[FeatureVault](https://github.com/parag-labs/feature-vault)** - a mini feature store with point-in-time-correct joins that never leak the future
- **[PromptShield](https://github.com/parag-labs/prompt-shield)** - firewall for llm apps: block prompt injection inbound, redact pii/secrets outbound
- **[DriftWatch](https://github.com/parag-labs/drift-watch)** - data-drift detection (psi + kl-divergence) for ml monitoring, in three languages
- **[ChaosMeshLite](https://github.com/parag-labs/chaos-mesh-lite)** - resilience testing as a ci slo gate: inject faults, assert the slo still holds
- **[DeployKit](https://github.com/parag-labs/deploy-kit)** - one command to deploy an llm app into any cloud or on-prem, secure by default
- **[gpu-flock](https://github.com/parag-labs/gpu-flock)** - thousands of boids computed and rendered entirely on the gpu with webgpu compute shaders, with an automatic webgl2 fallback so it runs anywhere - zero dependencies, no build step ([live demo](https://parag-labs.github.io/gpu-flock/))
- **[MiniRaft](https://github.com/parag-labs/mini-raft)** - a small, readable raft consensus implementation - leader election + log replication with a deterministic simulator
- **[ConsistentHash](https://github.com/parag-labs/consistent-hash)** - a consistent-hash ring with virtual nodes in three languages - minimal remap on membership change
- **[agent-run-dashboard](https://github.com/parag-labs/agent-run-dashboard)** - a small full-stack dashboard (fastapi + react) for recording ai agent runs and watching cost, tokens, and failures over time
- **[deterministic-sim-testing](https://github.com/parag-labs/deterministic-sim-testing)** - deterministic simulation testing for distributed code - replay any run from a single 64-bit seed, and shrink a failing fault schedule to a minimal reproducer (foundationdb / tigerbeetle style)
- **[multi-raft](https://github.com/parag-labs/multi-raft)** - run thousands of independent raft consensus groups on one set of nodes - a shared scheduler instead of a thread per group, and cross-group rpc batching instead of an rpc per group
- **[durable-execution](https://github.com/parag-labs/durable-execution)** - durable execution - workflows written as ordinary code that survive crashes by replaying an append-only history, so a completed step never runs twice (temporal style)
<!-- PROJECTS:END -->

More are on the way - a Raft implementation, a consistent-hash ring, a full-stack
agent-ops dashboard, and drift/chaos/deploy tooling - published as they're ready.

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
- **Benchmarks**, where a repo has them: `pip install -r bench/requirements.txt` then
  `python bench/benchmark.py`, which writes graphs and a JSON summary under
  `bench/results/`.

## Contact

Parag Sawant - [linkedin.com/in/paragsawant](https://www.linkedin.com/in/paragsawant/)



