# parag-labs

Small, focused tools for building AI systems you can actually trust in production â€”
verifiable retrieval, agent guardrails, drift and cost monitoring, and a few CI
gates that turn "we should really check that" into "the build fails if we don't."

Most of these started as a problem I hit at work and couldn't find a clean, small
answer for, so I wrote one. Each project is real, tested code with a README that
explains the why. Where something is a scaffold or a deliberate shortcut, I say so
instead of pretending it's production-grade.

A lot of the cores are written three times â€” Python, C#, and Java. That's not for
show: they're plain algorithms (a Merkle proof, a point-in-time join, a drift
statistic), and porting them keeps me honest that the logic is the logic, not a
trick of one language's libraries.

## Projects

<!-- PROJECTS:START -->
<!-- The list below grows as repositories are published. -->
- **[LedgerRAG](https://github.com/parag-labs/ledger-rag)** — verifiable RAG with a tamper-evident cryptographic ledger - every answer ships a proof (python/c#/java)
<!-- PROJECTS:END -->

## Running things

- Python: `pip install pytest && pytest -q`
- C#: `dotnet test` (targets .NET 10)
- Java: `mvn test` (JDK 17+)

## Contact

Parag Sawant â€” [linkedin.com/in/paragsawant](https://www.linkedin.com/in/paragsawant/)

