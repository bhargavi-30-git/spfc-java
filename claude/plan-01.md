# Java Senior Backend Engineering Curriculum

**Status: Syllabus Design Phase (Architecture Only — detailed lessons not yet included)**
**Version-verification date:** September 26, 2026 — verified against OpenJDK/Oracle JEP indexes, Spring Framework's official version-support wiki, Spring Boot release notes, and Spring AI's official release announcements.

> This document is a living registry. Module numbers below are fixed and will not be renamed or renumbered as detailed content (Part 4 onward) is added in later installments.

---

## PART 1 — ASSUMPTIONS AND INTERPRETATION

Since the learner's exact starting point wasn't specified, the following explicit, labeled assumptions were made. Any of these can be corrected to re-cut the plan.

**[ASSUMPTION-1] Learner level:** Can write basic procedural/OO code in *some* language (not necessarily Java) — variables, loops, functions, classes — but does not yet have professional Java experience. If the learner already has 1–3 years of Java experience, Phases 0–2 compress by roughly 40%.

**[ASSUMPTION-2] "Advanced Java" in this curriculum** means: JVM internals, concurrency at the memory-model level, performance engineering, framework internals (not just annotations), distributed-systems reasoning, and the ability to justify every technology choice with trade-offs — not just "knows Spring Boot annotations."

**[ASSUMPTION-3] "Senior-level" in this curriculum** means: independently taking an ambiguous business problem, producing a design with justified trade-offs, implementing it to production quality, securing it, testing it, operating it, and explaining every decision to both engineers and non-engineers. It does **not** mean having the judgment senior engineers only get from years of on-call pages, failed migrations, and postmortems — that requires real production time, which no curriculum replaces. This plan builds toward "hire-able as strong senior / staff-track," not "10-years-experienced."

**[ASSUMPTION-4] Learnable via study + projects:** language mastery, JVM/GC mechanics, Spring internals, SQL, concurrency, testing, security patterns, system design vocabulary and trade-off reasoning, Docker/Kubernetes mechanics, observability tooling, AI-integration patterns.

**[ASSUMPTION-5] Requires real production experience (this curriculum builds the *foundation*, not the substitute):** intuition for which incidents will recur, negotiating scope under real deadline pressure, organizational trade-offs (Conway's Law in practice), judgment on when to say no to a stakeholder, calibrated confidence in unfamiliar codebases, and the scar tissue of having been paged at 3 a.m. for a decision you made.

**[ASSUMPTION-6] Recommended primary Java learning baseline: Java 25 (LTS)** — released September 16, 2025, current LTS, supported to ~2030+. This is the version used for new code throughout the curriculum.

**[ASSUMPTION-7] Legacy versions studied in parallel/dedicated tracks:** **Java 8** (still dominant in large enterprises — pre-modularization, pre-`var`, pre-records) and **Java 17** (the prior enterprise-standard LTS baseline, still extremely common in "modern legacy" codebases). Java 21 is studied as the immediate predecessor LTS (virtual threads, pattern matching maturing) since most current job descriptions say "Java 17/21."

**[ASSUMPTION-8] Framework baseline:** Spring Framework **7.0.x** / Spring Boot **4.0.x** (current GA line as of the verification date) is the primary teaching baseline, since it targets JDK 17–25+ and the `jakarta` namespace exclusively. **Spring Boot 3.5.x / Spring Framework 6.2.x** (javax→jakarta transition already done, Java 17 baseline) is explicitly taught in parallel as the "legacy-maintenance" baseline, because most employers' *existing* production systems are still on 3.x — Spring Boot 3.5 community support runs to roughly mid-2026 with extended enterprise support beyond, so it will be encountered constantly for years.

**[ASSUMPTION-9]** Assumes a computer capable of running Docker/Kubernetes locally (or via a free-tier cloud sandbox) and the ability to allocate the stated 10 hrs/week consistently. If the weekly schedule is irregular, use the "catch-up week" mechanism (Part 8, to be delivered) rather than compressing content.

---

## PART 2 — EXECUTIVE ROADMAP

Total estimated duration is **not a bootcamp number** — it is the honest total for the full senior-capability path. Three checkpoints are given so the learner can stop earlier if the goal is narrower.

| Phase | Purpose | Hours | Weeks (@10h/wk) | Major Deliverable | Competency After |
|---|---|---|---|---|---|
| **0. Foundations & Tooling** | CS/OS/networking/Linux/Git basics, how programs run | 60 | 6 | Git-managed dev environment + CLI fluency | Can read a stack trace, use the shell, and manage source control like an engineer |
| **1. Core Java (8→25 curated)** | Full language mastery across eras | 140 | 14 | Console app portfolio + version-migration notes | Can write correct, idiomatic modern Java and read Java 8 legacy code |
| **2. JVM & Concurrency Internals** | Memory model, GC, threading, virtual threads | 90 | 9 | Profiling report + concurrency bug-fix log | Can diagnose OOM/deadlock/perf issues from first principles |
| **3. Clean Code, OOD & Design Patterns** | SOLID, patterns, refactoring | 60 | 6 | Refactored console app + pattern catalog | Designs maintainable OO systems, reviews code meaningfully |
| **4. Build Tools & Testing** | Maven/Gradle, full test pyramid | 50 | 5 | CI-tested multi-module build | Ships code with automated quality gates |
| **5. Databases & Persistence** | SQL → JDBC → Hibernate/JPA | 100 | 10 | JDBC project + JPA-based data layer | Designs schemas, writes performant queries, avoids ORM traps |
| **6. Spring Core + Spring Boot** | DI, AOP, Boot production features | 90 | 9 | Production-configured Spring Boot service | Builds real Spring apps, not "magic annotations" |
| **7. Web/API Engineering + Security** | REST, reactive, Spring Security, OAuth2/JWT | 90 | 9 | Secure REST API project | Designs and secures production APIs |
| **8. Productivity Tooling** | Lombok, MapStruct, codegen mechanics | 20 | 2 | Refactor pass across earlier projects | Uses codegen tools without being mystified by them |
| **9. Distributed Systems & Microservices** | DDD, resilience, saga, service boundaries | 80 | 8 | Modular monolith w/ extraction analysis | Reasons about service boundaries and failure modes |
| **10. Messaging & Event-Driven Arch** | Kafka, event design, stream processing | 60 | 6 | Event-driven order-processing service | Builds reliable async systems |
| **11. Caching & NoSQL** | Redis, Caffeine, Mongo, Elasticsearch | 50 | 5 | Caching layer + polyglot-persistence demo | Picks the right store for the right data shape |
| **12. DevOps, Containers, Cloud-Native** | Docker, Kubernetes, CI/CD | 80 | 8 | Containerized, CI/CD-deployed service | Ships and operates containerized systems |
| **13. Observability & Production Support** | Logging, tracing, metrics, incident response | 50 | 5 | Full observability stack on a live project | Debugs production incidents methodically |
| **14. Application Security (deep)** | Threat modeling, OWASP, supply chain | 40 | 4 | Security audit of own project | Thinks like an attacker before shipping |
| **15. Architecture & System Design** | HLD/LLD, ADRs, scalability patterns | 70 | 7 | 3 written system-design docs | Passes system-design interviews and writes real ADRs |
| **16. AI for Java Engineers** | LLMs, RAG, Spring AI, agents | 70 | 7 | Java-based GenAI service | Ships a production-grade AI-backed API responsibly |
| **17. Legacy & Modernization** | Java EE/Jakarta, javax→jakarta, strangler pattern | 40 | 4 | Modernization plan for a legacy sample app | Can work inside old enterprise codebases and migrate them |
| **18. Professional Engineering Skills** | Code review, ADRs, communication | 30 | 3 (interleaved) | Portfolio of PRs/ADRs/design docs | Operates like a professional team member, not a solo coder |
| **19. Capstone** | Senior-level integrated system | 120 | 12 | Full capstone system | Demonstrates hire-ready, senior-track capability |
| **20. Interview Preparation** | DSA, mock interviews, behavioral | 90 | 9 (interleaved in final third) | Mock interview log + resume/GitHub polish | Interview-ready for senior Java backend roles |

**Totals (Core Path, Phases 0–20 as scoped):** ≈ **1,330 hours**, ≈ **133 weeks** at 10 hrs/week ≈ **~2.6 years of part-time study**, including revision, projects, and assessments already folded into each phase's hours (not on top of them).

This is the **full senior-capability path**. Three honest checkpoints inside it:

- **Minimum job-ready (junior/entry backend Java role):** Phases 0–7 + basic parts of 12, 18, 20 ≈ **560 hours ≈ 56 weeks (~13 months)**
- **Strong mid-level backend engineer:** Phases 0–13 + 18 + partial 20 ≈ **920 hours ≈ 92 weeks (~21 months)**
- **Senior-capability curriculum complete:** all phases above ≈ **1,330 hours ≈ 133 weeks (~2.6 years)**
- **Optional specialization add-ons** (deep AI specialization, deep Kubernetes/SRE, or deep performance engineering) each add **60–100 hours (~6–10 weeks)** on top, pursued *after* the core senior path, not instead of it.

Finishing week 133 does not by itself make someone "a senior engineer" — it provides the full *toolkit* a senior engineer needs. The judgment layer on top comes from shipping real systems under real constraints, which is why Phase 19 (capstone) and Phase 18 (professional skills) are deliberately experience-simulating rather than pure tutorial.

---

## PART 3 — CURRICULUM DEPENDENCY MAP

```
Phase 0 (Foundations/Tooling)
   │  [hard prerequisite for everything]
   ▼
Phase 1 (Core Java, curated across versions)
   │  [hard prerequisite for everything Java-specific]
   ├──────────────────────────────────────────────┐
   ▼                                               ▼
Phase 2 (JVM & Concurrency)                Phase 3 (Clean Code/OOD/Patterns)
   │   [can run in PARALLEL with Phase 3]           │
   └───────────────┬────────────────────────────────┘
                    ▼
           Phase 4 (Build Tools & Testing)
                    │  [testing knowledge needed from here on — do not defer]
                    ▼
           Phase 5 (Databases & Persistence)
                    │
                    ▼
           Phase 6 (Spring Core + Boot)
                    │  [depends on 1,2,3,4,5 — do NOT start Spring before SQL/JDBC]
        ┌───────────┼───────────────┐
        ▼           ▼               ▼
   Phase 7        Phase 8       (parallel: revisit Phase 3 patterns
 (Web/API+Sec)  (Productivity     in Spring context — DI is Strategy/
                 tooling)         Factory in disguise)
        │
        ▼
Phase 9 (Distributed Systems/Microservices)
        │  [depends on 6,7; conceptually needs Phase 3 DDD-adjacent ideas]
   ┌────┼─────────────┐
   ▼    ▼             ▼
Phase 10   Phase 11    (parallel: 10 and 11 can interleave;
(Messaging) (Caching/     both depend on 9's service-boundary thinking)
             NoSQL)
   │        │
   └───┬────┘
       ▼
Phase 12 (DevOps/Containers/Cloud-Native)
       │  [can actually START in parallel with Phase 6 at a basic Docker level —
       │   full K8s content depends on Phase 9's service model]
       ▼
Phase 13 (Observability & Production Support)
       │  [depends on 12; conceptually threads back through 2,6,9,10]
       ▼
Phase 14 (Application Security, deep)
       │  [depends on 7's security basics; deepens them]
       ▼
Phase 15 (Architecture & System Design)
       │  [synthesizes 3,5,6,7,9,10,11,12,13,14 — cannot be front-loaded]
       ▼
Phase 16 (AI for Java Engineers)
       │  [depends on 6,7,9,13 — needs a real backend to attach AI features to]
       ▼
Phase 17 (Legacy & Modernization)
       │  [depends on 1,5,6 — best studied after "modern" is known so legacy gaps
       │   are visible; can run PARALLEL with 15/16]
       ▼
Phase 18 (Professional Engineering Skills) — INTERLEAVED from Phase 4 onward,
       not a discrete block; intensifies from Phase 9 onward
       ▼
Phase 19 (Capstone) — draws on ALL prior phases
       ▼
Phase 20 (Interview Prep) — DSA runs in parallel from Phase 2 onward
       (little and often, ~2hrs/week), intensifies in final third
```

**What can be deferred safely:** deep Kubernetes (basic Docker is enough until Phase 9 is done), GraphQL/gRPC depth, Elasticsearch depth, event sourcing depth, native-image/AOT tuning, deep Vector API/Panama-era JVM internals.

**What must never be skipped:** SQL before ORM (Phase 5 before 6), concurrency fundamentals before virtual threads (Phase 2 before touching Loom-era features), testing fundamentals before microservices (Phase 4 before 9), security basics before distributed systems (Phase 7 before 9 — a monolith must be securable first before securing a distributed system).

**Modules that must remain strictly sequential:** Core Java → JVM Internals → Spring Core → Spring Boot → Web/API. **Modules safe to interleave:** DSA/interview prep (from Phase 2 onward), professional skills (from Phase 4 onward), legacy-Java-8 reading exercises (can shadow Phase 1 concept-by-concept).

---

## PROJECT CHECKPOINTS (mapped to phases)

| Project | Description | Checkpoint |
|---|---|---|
| P1 | Core Java exercises | End of Phase 1 |
| P2 | OO console application | End of Phase 3 |
| P3 | JDBC-based project | End of Phase 5 |
| P4 | Spring Core project | Mid Phase 6 |
| P5 | Spring Boot REST API | End of Phase 7 |
| P6 | Secure database-backed application | End of Phase 7/8 |
| P7 | Production-quality modular monolith | End of Phase 9 |
| P8 | Distributed / event-driven application | End of Phase 10 |
| P9 | Cloud-native, observable, containerized backend | End of Phase 13 |
| P10 | Java-based generative AI application | End of Phase 16 |
| P11 | Final capstone (senior-level integrated system) | Phase 19 |

---

## MODULE REGISTRY (authoritative index — numbers fixed for all future installments)

| # | Phase | Module |
|---|---|---|
| 0.1 | 0 | How Programs Execute (CPU/memory/process/thread model) |
| 0.2 | 0 | Operating Systems & Linux Essentials |
| 0.3 | 0 | Networking Fundamentals (TCP/UDP/HTTP/DNS/Client-Server) |
| 0.4 | 0 | Command Line & Shell Fluency |
| 0.5 | 0 | Git & GitHub Workflows |
| 0.6 | 0 | Data Structures & Algorithms Primer + Complexity Analysis |
| 0.7 | 0 | SDLC, Agile Practice, Requirements Analysis, Technical Docs |
| 1.1 | 1 | Java Platform Architecture (JDK/JRE/JVM/bytecode, compilation model) |
| 1.2 | 1 | Syntax Core: Variables, Operators, Control Flow, Methods, Arrays, Strings |
| 1.3 | 1 | OOP I: Encapsulation, Abstraction, Inheritance, Polymorphism, Composition |
| 1.4 | 1 | OOP II: Interfaces, Abstract Classes, Nested/Inner Classes, Enums |
| 1.5 | 1 | Modern Data Carriers: Records, Sealed Classes, Pattern Matching |
| 1.6 | 1 | Generics In Depth |
| 1.7 | 1 | Collections Framework In Depth |
| 1.8 | 1 | Exceptions, Assertions, Error-Handling Strategy |
| 1.9 | 1 | Object Contracts: equals/hashCode/Comparable/Comparator/Immutability |
| 1.10 | 1 | Functional Java: Lambdas, Method References, Functional Interfaces |
| 1.11 | 1 | Streams, Optional, Parallel Streams |
| 1.12 | 1 | I/O, NIO.2, Serialization & Its Risks |
| 1.13 | 1 | Annotations & Reflection |
| 1.14 | 1 | Date/Time API, Regex, i18n/l10n |
| 1.15 | 1 | Java Platform Module System (JPMS) |
| 1.16 | 1 | Java Version Evolution Workshop (8→11→17→21→25 diffing exercise) |
| 2.1 | 2 | Class Loading & Bytecode Fundamentals |
| 2.2 | 2 | JVM Memory Areas: Stack, Heap, Metaspace, Object Layout |
| 2.3 | 2 | Garbage Collection: Algorithms & Collectors |
| 2.4 | 2 | Diagnosing OOM/StackOverflow/Memory Leaks |
| 2.5 | 2 | Java Memory Model: Happens-Before, Visibility, Atomicity |
| 2.6 | 2 | Synchronization, Locks, Volatile, ThreadLocal |
| 2.7 | 2 | Executors, Futures, CompletableFuture, Fork/Join |
| 2.8 | 2 | Concurrent Collections & Concurrency Bugs (deadlock/race/starvation) |
| 2.9 | 2 | Virtual Threads, Structured Concurrency, Scoped Values (Project Loom) |
| 2.10 | 2 | Profiling & Benchmarking: JFR, JMC, JMH, Thread/Heap Dumps |
| 3.1 | 3 | SOLID Principles In Practice |
| 3.2 | 3 | DRY/KISS/YAGNI/Tell-Don't-Ask/Law of Demeter/Cohesion-Coupling |
| 3.3 | 3 | Domain Modeling: Value Objects, Entities, Services |
| 3.4 | 3 | Defensive Programming & Design by Contract |
| 3.5 | 3 | Refactoring, Code Smells, Technical Debt |
| 3.6 | 3 | Effective Code Reviews & API Design Principles |
| 3.7 | 3 | Creational Patterns (Factory, Builder, Singleton, Prototype) |
| 3.8 | 3 | Structural Patterns (Adapter, Decorator, Proxy, Facade, Composite) |
| 3.9 | 3 | Behavioral Patterns (Strategy, Observer, Template Method, Chain of Responsibility, Command, State) |
| 3.10 | 3 | Enterprise Patterns (Repository, Unit of Work, Specification, DI) |
| 3.11 | 3 | Distributed-System Patterns Preview (Circuit Breaker, Saga, Outbox, CQRS, Event Sourcing — conceptual only, deepened in Phase 9/10) |
| 4.1 | 4 | Maven In Depth |
| 4.2 | 4 | Gradle In Depth |
| 4.3 | 4 | Multi-Module Projects, BOMs, Dependency Management |
| 4.4 | 4 | Dependency Vulnerability Scanning & Supply-Chain Hygiene |
| 4.5 | 4 | Test Strategy & the Test Pyramid |
| 4.6 | 4 | JUnit 5, Mockito, AssertJ |
| 4.7 | 4 | Testcontainers, WireMock, Integration Testing |
| 4.8 | 4 | Static Analysis: Checkstyle, SpotBugs, SonarQube, ArchUnit |
| 4.9 | 4 | Parameterized/Property-Based/Mutation Testing, Flaky Tests |
| 5.1 | 5 | Relational Modeling & SQL Fundamentals |
| 5.2 | 5 | Joins, Subqueries, Aggregations, Window Functions |
| 5.3 | 5 | Normalization, Indexing, Query Plans |
| 5.4 | 5 | Transactions, ACID, Isolation Levels, Locking Strategies |
| 5.5 | 5 | JDBC, DataSource, PreparedStatement, Connection Pooling, Batch Ops |
| 5.6 | 5 | Schema Migrations: Flyway/Liquibase |
| 5.7 | 5 | JPA/Hibernate: Entity Lifecycle, Mapping, Relationships, Fetching |
| 5.8 | 5 | JPA Advanced: N+1, Caching Layers, JPQL/Criteria/Native Queries |
| 5.9 | 5 | Spring Data JPA/JDBC; When Not To Use an ORM (jOOQ/plain JDBC) |
| 6.1 | 6 | IoC & DI Fundamentals (Spring Core, framework-agnostic first) |
| 6.2 | 6 | Bean Lifecycle, Scopes, Configuration Styles |
| 6.3 | 6 | AOP, Proxies, Transaction Management Internals |
| 6.4 | 6 | Spring Events, Validation, SpEL, Scheduling, Caching, Async |
| 6.5 | 6 | Spring Boot Auto-Configuration Mechanics (how "magic" actually works) |
| 6.6 | 6 | Configuration Properties, Profiles, Externalized Config |
| 6.7 | 6 | Actuator, Custom Health Indicators, Metrics |
| 6.8 | 6 | Packaging, Containerization, Graceful Shutdown, Native-Image Awareness |
| 6.9 | 6 | Spring Boot Upgrade Strategy & Custom Starters |
| 7.1 | 7 | Servlets, Filters, Interceptors, Spring MVC Foundations |
| 7.2 | 7 | REST API Design: Methods, Status Codes, Content Negotiation |
| 7.3 | 7 | Validation, Error Formats, Pagination/Sorting/Filtering, Versioning, Idempotency |
| 7.4 | 7 | OpenAPI/Swagger, File Upload/Download, SSE |
| 7.5 | 7 | Reactive Fundamentals: Reactor, WebFlux, Backpressure — and When Not To Use It |
| 7.6 | 7 | gRPC & GraphQL Fundamentals; API Gateway Concepts |
| 7.7 | 7 | Spring Security Architecture & Filter Chain |
| 7.8 | 7 | Authentication, Password Handling, Sessions, CSRF/CORS |
| 7.9 | 7 | OAuth2, OIDC, JWT, Resource Servers, Method Security |
| 7.10 | 7 | Security Testing & OWASP Top 10 (applied) |
| 8.1 | 8 | Lombok Mechanics (annotation processing, what it hides, debugging implications) |
| 8.2 | 8 | MapStruct, Records-as-DTOs, Jackson/Bean Validation/JPA annotation mechanics |
| 8.3 | 8 | Codegen Tools: OpenAPI Generator, jOOQ Codegen, IDE-assisted refactoring |
| 9.1 | 9 | Monolith vs Modular Monolith vs Microservices — decision framework |
| 9.2 | 9 | Domain-Driven Design: Bounded Contexts, Aggregates, Ubiquitous Language |
| 9.3 | 9 | Inter-Service Communication: Sync vs Async, Service Discovery |
| 9.4 | 9 | Resilience: Timeouts, Retries, Circuit Breakers, Bulkheads (Resilience4j) |
| 9.5 | 9 | Distributed Transactions: Saga, Outbox, Idempotency, Eventual Consistency |
| 9.6 | 9 | CAP Theorem, Consistency Models, Distributed Locking |
| 9.7 | 9 | Distributed Tracing Fundamentals; Relevant vs Deprecated Spring Cloud Components |
| 10.1 | 10 | Messaging Fundamentals: Queues/Topics/Delivery Guarantees/Ordering |
| 10.2 | 10 | Apache Kafka Deep Dive + Spring for Apache Kafka |
| 10.3 | 10 | Schema Evolution: Avro/Protobuf/JSON, Event Versioning |
| 10.4 | 10 | Dead-Letter Queues, Idempotent Consumers, Retry Strategies |
| 10.5 | 10 | Event Sourcing Fundamentals; Kafka Streams / Stream Processing Concepts |
| 11.1 | 11 | Caching Strategies: Cache-Aside/Read-Through/Write-Through/Write-Behind |
| 11.2 | 11 | Redis + Spring Cache Abstraction + Caffeine |
| 11.3 | 11 | Cache Invalidation, Stampede, Observability, When Caching Hurts |
| 11.4 | 11 | NoSQL Fundamentals: Document/KV/Wide-Column/Graph Models |
| 11.5 | 11 | MongoDB Practical; Elasticsearch/OpenSearch Fundamentals |
| 12.1 | 12 | Docker: Images, Dockerfiles, Multi-Stage Builds, Container Security |
| 12.2 | 12 | Docker Compose for Local Multi-Service Development |
| 12.3 | 12 | Kubernetes Fundamentals: Pods, Deployments, Services, ConfigMaps/Secrets |
| 12.4 | 12 | K8s Operations: Ingress, Probes, Resource Limits, Scaling, Helm Awareness |
| 12.5 | 12 | CI/CD Pipelines (GitHub Actions), Deployment Strategies (rolling/blue-green/canary) |
| 12.6 | 12 | Twelve-Factor App, IaC Awareness, Cloud Fundamentals (provider-agnostic) |
| 13.1 | 13 | Structured Logging, Correlation IDs, Log Levels |
| 13.2 | 13 | Metrics & Tracing: Micrometer, OpenTelemetry, Prometheus, Grafana |
| 13.3 | 13 | Centralized Logging (ELK/OpenSearch), SLIs/SLOs, Alerting/Dashboards |
| 13.4 | 13 | Incident Response, RCA, Postmortems, Production Debugging Playbooks |
| 14.1 | 14 | Secure Coding & Threat Modeling |
| 14.2 | 14 | Injection/XSS/CSRF/SSRF/Deserialization/Path Traversal Deep Dive |
| 14.3 | 14 | Dependency & Supply-Chain Security, Secrets Management, Encryption/TLS |
| 14.4 | 14 | Zero-Trust Concepts, Audit Logging, Data Privacy |
| 15.1 | 15 | Architectural Styles: Layered, Hexagonal, Clean, Onion, Ports & Adapters |
| 15.2 | 15 | Scalability/Availability/Reliability Patterns (replication, sharding, LB, CDN) |
| 15.3 | 15 | ADRs, C4 Diagrams, Trade-off Analysis, Cost & Build-vs-Buy |
| 15.4 | 15 | Low-Level Design Workshop |
| 15.5 | 15 | High-Level System Design Workshop |
| 16.1 | 16 | GenAI Foundations: LLMs, Tokens, Embeddings, Vector Search |
| 16.2 | 16 | Prompt Engineering, Structured Output, Tool/Function Calling |
| 16.3 | 16 | RAG: Chunking, Retrieval, Reranking, Conversation Memory |
| 16.4 | 16 | AI Agents & Model Context Protocol Awareness |
| 16.5 | 16 | Spring AI & LangChain4j (version-verified) |
| 16.6 | 16 | AI Safety Engineering: Hallucination, Guardrails, Prompt Injection, Cost/Latency |
| 16.7 | 16 | Testing & Securely Deploying AI-Backed Java Services |
| 17.1 | 17 | Java EE vs Jakarta EE vs Spring Framework vs Spring Boot — Relationship Map |
| 17.2 | 17 | javax→jakarta Migration; Legacy Servlet/JSP/EJB/JAX-RS/JAX-WS Awareness |
| 17.3 | 17 | Strangler Pattern & Incremental Modernization Planning |
| 17.4 | 17 | Java Version Upgrade Playbook (8→17→21→25) |
| 18.x | 18 | Professional Skills (interleaved: code review, PRs, ADRs, estimation, stakeholder comms) — delivered as recurring mini-modules, not a single block |
| 19.x | 19 | Capstone (system spanning Phases 1–17) |
| 20.x | 20 | DSA + Interview Tracks (Java/JVM/Spring/DB/API/Concurrency/Testing/Security/Microservices/System Design/Behavioral) |

---

## VERSION & FRAMEWORK SNAPSHOT (verified September 26, 2026)

- **Java 25** — current LTS (GA Sept 16, 2025; EOL ~2030+). Primary teaching baseline. Key finalized JEPs: 506 (Scoped Values), 511 (Module Import Declarations), 512 (Compact Source Files/Instance Main), 513 (Flexible Constructor Bodies), 519 (Compact Object Headers), 521 (Generational Shenandoah). Preview/incubator in 25 (not stable): 470 (PEM Encodings), 502 (Stable Values), 505 (Structured Concurrency, 5th preview), 507 (Primitive Types in Patterns, 3rd preview), 508 (Vector API, 10th incubator).
- **Java 21** — prior LTS (2023); virtual threads/record patterns finalized; still the baseline in most current job postings — treated as a "read and maintain" track alongside 25.
- **Java 17 / Java 8** — legacy tracks, taught explicitly as "what will actually be found in enterprise codebases."
- **Spring Framework 7.0.x** — current production line (Nov 2025), JDK 17–25+, Jakarta EE 11–12 namespace only. **Spring Framework 6.2.x** (Jakarta EE 9–10) is the legacy-maintenance track; **5.3.x** (javax, Java EE 7–8) is the "found in old enterprise apps" track.
- **Spring Boot 4.0.x** — current GA (4.0.6 as of this verification), pairs with Spring Framework 7.x. **Spring Boot 3.5.x** — still widely deployed, community support winding down around mid-2026 with extended enterprise support beyond; this is the practical "legacy maintenance" baseline encountered on the job.
- **Spring AI 2.0.x** — GA (June 2026), requires Spring Boot 4.x. **Spring AI 1.1.x** targets Spring Boot 3.4/3.5 — used only as a legacy-compatibility note in Phase 16, not the primary teaching version.

This matrix will be expanded into the full Part 5 deliverable (with every deprecated/removed API mapping) in a future installment.

---

## STILL TO COME (future installments — module numbering above will not change)

- **Part 4:** Full detailed treatment of every module (20-point template: objectives, prerequisites, sections, exercises, debugging drills, testing activities, common mistakes, deprecated-vs-current guidance, tools, hours, weeks, deliverable, assessment, interview relevance, production relevance, completion criteria, advanced-optional material) — delivered phase-by-phase across numbered installments, starting with Phase 0 and Phase 1.
- **Part 5:** Full Java & Framework Version Matrix
- **Part 6:** Technology Prioritization Matrix
- **Part 7:** Full Project Portfolio specs
- **Part 8:** Weekly Study System
- **Part 9:** Assessment Framework
- **Part 10:** Career Readiness Map
- **Part 11:** Gap and Coverage Audit
- **Part 12:** Final Learning Metrics
