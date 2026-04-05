# Sentra

> A system that determines whether infrastructure is truly stable — not just operational.  
> Sentra prevents systems from acting on false recovery.

![Status](https://img.shields.io/badge/status-active--development-blue)
![Access](https://img.shields.io/badge/access-limited-lightgrey)
![Layer](https://img.shields.io/badge/layer-control--plane-purple)

<p align="left">
  <strong>Status:</strong> Active Development<br/>
  <strong>Layer:</strong> Control Plane / Decision System<br/>
  <strong>Part of:</strong> Trellis Systems
</p>

Sentra is a control layer developed within Trellis Systems.

It determines system posture and governs when action is safe.

---

## One-Minute Understanding

Most systems answer:
> "Is it up?"

Sentra answers:
> **"Is it safe to act?"**

---

A system can be:

- **STABLE** → safe to act  
- **UNSTABLE** → actively failing  
- **DEGRADED** → recovered, but not yet trustworthy  

---

The difference:

- Traditional systems allow action as soon as something is “up”  
- Sentra requires **proof of stability over time**

---

Example:

A service restarts and reports healthy.

- Traditional → deploy allowed  
- Sentra → **deploy blocked until stability is proven**

---

Sentra introduces:
- state-based reasoning  
- time-aware recovery validation  
- action gating under uncertainty  

---

## Contents

- [One-Minute Understanding](#one-minute-understanding)
- [The Problem](#the-problem)
- [The Shift](#the-shift)
- [Core Concepts](#core-concepts)
- [Architecture](#conceptual-architecture)
- [State Model](#state-model)
- [Decision Model](#decision-model)
- [Use Cases](#use-cases)

---

## The Problem

Modern systems are rich in signals but poor in judgment.

They can report whether something is up or down, healthy or unhealthy, reachable or unreachable. But they still leave teams to answer the question that matters most:

> **Is this system actually safe to act on right now?**

That gap creates real operational risk:

- systems appear recovered before stability is proven  
- actions are taken on partial or misleading signals  
- “green” dashboards hide degraded reality  
- instability spreads because systems are treated as ready too soon  

---

## The Shift

Sentra introduces a different model:

> **State over status.**

Instead of asking whether a component is merely available, Sentra determines whether the system is:

- actually stable  
- still in recovery  
- operating under unresolved uncertainty  
- safe to act on  

This shifts infrastructure from passive reporting to active operational judgment.

---

## Core Concepts

### State, not status
Sentra evaluates systems as:

- **STABLE**
- **DEGRADED**
- **UNSTABLE**

These states reflect operational truth, not superficial availability.

---

### Recovery is not resolution
A system returning to service does not mean it has regained trust.

Sentra treats recovery as a phase that must be validated over time before stability is restored.

---

### Safe-to-act gating
Actions are governed by posture, not optimism.

If the system is degraded or unstable, Sentra can block or delay downstream actions until conditions are truly safe.

---

### Multi-signal evaluation
Sentra evaluates posture across multiple signal domains:

- application  
- infrastructure  
- network  
- physical  

This allows decisions to reflect system reality rather than isolated signals.

---

## Conceptual Architecture

```mermaid
flowchart TD
    A[Application Signals] --> S[Sentra Control Layer]
    I[Infrastructure Signals] --> S
    N[Network Signals] --> S
    P[Physical Signals] --> S

    S --> E[State Evaluation]
    E --> D[Decision Logic]
    D --> G[Safe-to-Act Gating]
    G --> O[Allowed or Blocked Actions]
```

---

## Design Principles

- **Separation of control and execution**
- **Explicit state modeling**
- **Time-aware validation**
- **Multi-domain signal evaluation**
- **Conservative decision-making under uncertainty**

---

## System Characteristics

- Deterministic state transitions
- Observable decision reasoning
- Controlled action boundaries
- Independence from execution environments

---

## State Model

```mermaid
stateDiagram-v2
    [*] --> STABLE
    STABLE --> UNSTABLE: failure detected
    UNSTABLE --> DEGRADED: recovery begins
    DEGRADED --> STABLE: validation passes
    DEGRADED --> UNSTABLE: instability returns
```
A system can be back, but not yet trustworthy.

---

## Example Operational Flow

```mermaid
flowchart TD
    A[System healthy] --> B[STABLE]
    B --> C[Failure detected]
    C --> D[UNSTABLE]
    D --> E[Service restarts]
    E --> F[DEGRADED]
    F --> G{Stable over time?}
    G -- Yes --> H[STABLE]
    G -- No --> I[UNSTABLE]
```

During **DEGRADED:**

- recovery is observed, not assumed,
- action remains constrained
- trust is rebuilt through sustained evidence

---

## Decision Model

```mermaid
flowchart LR
    A[Incoming Signals] --> B[Normalize Evidence]
    B --> C[Evaluate Posture]
    C --> D{Safe to Act?}
    D -- Yes --> E[Allow Action]
    D -- No --> F[Block or Delay Action]
```

Sentra answers a question most systems leave unresolved:

> **What should happen next, given the current level of confidence?**

---

## What This Enables
	
- Preventing actions during unstable recovery windows
- Detecting degraded reality behind healthy-looking systems
- Coordinating behavior across inconsistent signals
- Introducing time-based trust restoration
- Moving from reactive monitoring to controlled decision-making

---

## Use Cases

### Deployment Safety

A service appears healthy after restart.

- Traditional → deploy allowed
- Sentra → **blocked until stability is proven**

---

### Hidden Network Degradation

Services report healthy, but network conditions
degrade.

- Traditional → remain green
- Sentra → **maintains DEGRADED posture**

---

### Flapping Systems

A service repeatedly fails and recovers.

- Traditional → oscillates
- Sentra → **prevents premature trust**

---

### Node Loss and Recovery

A node disappears and later returns.

- Traditional → marked healthy
- Sentra → **validation required before STABLE**

---

### Action Governance

A downstream action is requested.
	
- If not STABLE → **action is blocked or delayed**

---

## Positioning

Sentra introduces a missing layer in modern infrastructure:

**decision-making under uncertainty**

---

## Non-Goals

Sentra is not intended to:

- replace observability platform
- act as a monitoring or alerting system
- execute arbitrary automation without control logic
- infer system state from a single signal source

Sentra is focused on decision-making under uncertainty, not signal collection.

---

## Why It Matters

Systems fail not because they lack data,
but because they act on it incorrectly.

Sentra introduces:

- confidence-aware evaluation
- time-based validation of recovery
- decision control under uncertainty

This represents a shift from reporting conditions to governing operational trust.

Sentra ensures systems act on truth, not appearance.

---

## Status

Active development.

Current focus:

- state modeling
- signal evaluation
- recovery validation
- action gating

---

## About Trellis Systems

Sentra is being developed within Trellis Systems,
a platform for intelligent system orchestration and decision-making.

---

## Security

This repository does not expose implementation details or production systems.

If you believe you have identified a security concern, please contact the maintainers directly.

---

## Contributing

Contributions are not currently being accepted.

This repository provides a high-level view of the system.

---

## Note

Implementation details and internal architecture are not publicly exposed.
