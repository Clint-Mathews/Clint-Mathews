# Clint Mathews

**Backend lead for connected device fleets.** I build the systems that keep physical hardware online — Go, Kafka, gRPC, IoT protocols.

At Ford Pro I lead the platform behind **8,200 EV chargers**: **6M+ telemetry messages/day** at 99.9% data integrity, **99.95% uptime**. I architected the OCPP gateway that replaced the legacy monolith — migrated the full fleet, decommissioned ~2,150 servers (~$9,000/mo), and cut observability spend 60%.

Open to remote, worldwide — I anchor to your team's core hours. Contractor/USD invoicing.
[LinkedIn](https://www.linkedin.com/in/clint-mathews/) · [Site](https://clint-mathews.github.io) · mathewsclint28@gmail.com

---

## What I'm good at

**High-throughput event pipelines.** Kafka consumers designed for the failure case, not the happy path — circuit breakers, regional bulkhead isolation, Redis-backed per-partition backpressure, transactional offset commits so an offset only advances after replica confirmation. Sized for 2–4x growth without OOM.

**Reliability as an owned responsibility.** L3 production support on critical services. Rearchitected a synchronous reporting pipeline — 30+ minute blocking requests, 91.3% success — into an async Celery/Redis job queue targeting 99.9% with sub-second response.

**Cost as a design constraint.** ~$9,000/mo from a server decommission, 60% off observability spend. Both were architecture decisions, not cleanup passes.

**The cloud/hardware seam.** OCPP 1.6 and 2.x compliance, cloud-to-charger integration debugging with firmware teams, device simulators covering 2,000+ chargers so fleet-scale problems surface before production.

---

## Repositories

### [PhotonicOps](https://github.com/Clint-Mathews/PhotonicOps) — Go · gRPC · offline telemetry ingestion

Offline, air-gapped telemetry ingestion engine for silicon photonic biosensors in HIPAA-sensitive clinical environments. Sustains **10,000 samples/sec** over client-streaming gRPC on a zero-allocation hot path.

> **Status: Phase 1 of 5 shipped.** Phases 0 and 1 — infra harness and Go ingestion engine — are built and tested. Everything beyond that (agentic LLM triage, mTLS, DSP service, dashboard) is specified in ADRs and **not implemented**. The README says exactly which is which.

Built: `sync.Pool` buffer reuse for a low-GC hot path · lock-free/mutex-protected ring buffer for fixed-memory long-running ingestion · fixed goroutine worker pool with buffered-channel backpressure · Protobuf telemetry contract · synthetic 10kHz sensor client with Gaussian noise and thermal drift modeling · `pprof` instrumentation to verify GC-pause SLAs · GitHub Actions CI with `go test -race`, coverage gating, and static cross-compiled Linux artifacts · fully offline ARM64 Docker Compose stack (Postgres, Prometheus, Grafana, Langfuse, Ollama) behind a health-gate script.

Zero cloud API dependencies anywhere, by design.

### [EchoGate](https://github.com/Clint-Mathews/EchoGate) — Go · Python · LLM traffic

A split-plane AI API gateway and reverse proxy for upstream LLM traffic. Intercepts prompt streams on the data plane to cut latency and cost on calls that don't need to reach a frontier model.

### [Distributed-System-Project-Uno](https://github.com/Clint-Mathews/Distributed-System-Project-Uno) — Go

Pub/sub taken from system-design concept to working implementation — connection management, message serialization, reliable delivery. The counterpart to my [Redis pub/sub write-up](https://dev.to/clintmathews).

### [File-To-BinaryVideo-BackTo-File](https://github.com/Clint-Mathews/File-To-BinaryVideo-BackTo-File) — Go

Encodes an arbitrary file into a binary video format and losslessly decodes it back. An exercise in binary data representation and encoding pipelines.

---

## In progress

- **PhotonicOps Phase 1.5** — mTLS transport (ADR decided; current transport is still `insecure.NewCredentials()` and the repo says so).
- **OCPP protocol notes** — a write-up of what actually breaks between cloud and charger across 1.6 → 2.0.1, from fleet experience.

<!--
TODO Clint: keep this to two items you'll genuinely push in the next 30 days,
and delete the rest. An unfulfilled roadmap ages into a list of things you
didn't do. The OCPP write-up is the highest-leverage one on here — nobody
else can write it, and it's the single best proof of the niche claim above.
-->

---

## Stack

**Languages** Go · TypeScript · Python · C#
**Backend** Kafka · gRPC/Protobuf · NestJS · Node.js · Flask · Celery
**Data** PostgreSQL · MongoDB · Redis
**Infra** Docker · AWS · GitHub Actions · Datadog · Prometheus/Grafana
**Protocols** OCPP 1.6 / 2.x
**Patterns** Event-driven architecture · circuit breakers · bulkhead isolation · backpressure · async job queues · RFC authorship

---

## Elsewhere

8 RFCs authored at Ford Pro defining core platform services, the OCPP 2.x adoption path, and simulator architecture. Hackathon finalist, Retail & Pro Services Technology Q4 2025 — a React/Flask/GPT-4 platform over 100,000+ Jira issues, 70% faster analysis via intelligent caching and parallel processing.
