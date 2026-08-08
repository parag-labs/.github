# parag-labs

Small, focused tools for building AI systems you can actually trust in production -
verifiable retrieval, agent guardrails, drift and cost monitoring, and a few CI
gates that turn "we should really check that" into "the build fails if we don't."

Most of these started as a problem I hit at work and couldn't find a clean, small
answer for, so I wrote one. Each project is real, tested code with a README that
explains the why. Where something is a scaffold or a deliberate shortcut, I say so
instead of pretending it's production-grade.

A lot of the cores are written three times - Python, C#, and Java. That's not for
show: they're plain algorithms (a Merkle proof, a point-in-time join, a drift
statistic), and porting them keeps me honest that the logic is the logic, not a
trick of one language's libraries.

## Projects

<!-- PROJECTS:START -->
<!-- The list below grows as repositories are published. -->
- **[LedgerRAG](https://github.com/parag-labs/ledger-rag)** - verifiable RAG with a tamper-evident cryptographic ledger - every answer ships a proof (python/c#/java)
- **[EvalForge](https://github.com/parag-labs/eval-forge)** - eval-driven ci gate for llm quality - fail the build when a prompt change regresses
- **[SchemaGuard](https://github.com/parag-labs/schema-guard)** - catch breaking api/schema changes at the pull request, not in production
- **[AgentGuard](https://github.com/parag-labs/agent-guard)** - zero-trust runtime sandbox for tool-calling ai agents: least-privilege policy + signed audit log
- **[TokenLens](https://github.com/parag-labs/token-lens)** - attribute llm cost and latency to feature/tenant/model, with budget and anomaly gates
- **[QuotaGate](https://github.com/parag-labs/quota-gate)** - rate limiter for llm api traffic: per-model token & request budgets across sliding windows, per tenant/user scope, reserve-then-reconcile
- **[agent-trace](https://github.com/parag-labs/agent-trace)** - visual timeline and replay for agent runs: see where a run spent time, tokens, and money, then diff two runs ([live demo](https://parag-labs.github.io/agent-trace/))
<!-- PROJECTS:END -->

## Running things

- Python: `pip install pytest && pytest -q`
- C#: `dotnet test` (targets .NET 10)
- Java: `mvn test` (JDK 17+)

## Contact

Parag Sawant - [linkedin.com/in/paragsawant](https://www.linkedin.com/in/paragsawant/)



