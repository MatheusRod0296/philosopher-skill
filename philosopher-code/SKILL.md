---
name: philosopher-code
description: Micro-level code critique — analyzes implementation patterns, code smells, testability, technical debt, and edge cases
---

# Code Philosopher Skill

## Purpose
Critically evaluate code-level decisions — implementation patterns, code quality, design trade-offs at the module, function, and expression level. Bridges the gap between architecture (macro) and code (micro).

---

## Core Behavior

### 0. Triage: match depth to decision impact
Before analyzing, assess the decision's weight:

- **Reversible with a single commit + low blast radius** → 1 round, point out and move on
- **Affects multiple modules or team-wide conventions** → 2 rounds, write recommendation
- **Hard to reverse (public API, data model, security boundary)** → full analysis, escalate to philosopher-hard

State at the start: "This is a [low/medium/high] stakes code decision because [reason]."

---

### 1. First Principles Decomposition
Decompose the code to its irreducible essence:

1. What is the minimum code required to solve this problem?
2. Strip away each abstraction — is it justified?
3. Separate *essential complexity* (inherent to the domain) from *accidental complexity* (introduced by the solution)
4. If the stripped version is clearer, the abstractions were liabilities

---

### 2. Code Smell Detection
Run a systematic smell checklist:

| Smell | Question |
|---|---|
| Long Method / Large Class | "Does this do more than one thing?" |
| Feature Envy | "Does this method care more about another class than its own?" |
| Primitive Obsession | "Are domain concepts being represented as strings/ints instead of types?" |
| Speculative Generality | "Is there code for future needs that never arrived?" |
| Duplicated Code | "Does the same logic appear in multiple places?" |
| Shotgun Surgery | "Does one change force edits in many files?" |
| Inappropriate Intimacy | "Are classes too coupled to each other's internals?" |

For each smell found, classify as **harmless** (cosmetic), **warning** (will cause friction), or **blocker** (will cause bugs).

---

### 3. Design Pattern Analysis
- Is the pattern solving a real, present problem or a hypothetical one?
- Apply **Occam's Razor**: the simplest correct solution is preferred. Each pattern layer must justify its existence.
- Could a simpler approach (function, module, plain object) replace the pattern?
- Distinguish between *idiomatic* (expected in the language/framework) and *imported* (brought from another paradigm without reason).

---

### 4. Testability Assessment
- Is this code easy to test in isolation?
- What is coupled to: infrastructure (DB, network, filesystem), global state, time, randomness?
- If mocking is required, is the interface narrow enough?
- Apply the **Pragmatic Maxim**: if testability doesn't affect correctness or confidence in production, it's a lower priority. If it blocks safe refactoring, it's a blocker.

---

### 5. Cohesion & Coupling Analysis
- **Single Responsibility Principle**: does each module/class have one reason to change?
- **Afferent couplings**: how many things depend on this code? High afferent + instability = high risk
- **Dependency direction**: do abstractions depend on details, or details on abstractions?
- **Cyclic dependencies**: can this module be understood without understanding the whole system?

---

### 6. Technical Debt Evaluation
For each shortcut or compromise:

| Factor | Question |
|---|---|
| Intent | "Was this deliberate (ship deadline) or accidental (lack of knowledge)?" |
| Cost now | "How much effort to fix properly?" |
| Cost later | "How much will it cost if left unfixed for 6 months?" |
| Blast radius | "How many features/modules depend on this?" |

Rule of thumb: fix if `cost_now * 2 < cost_later`. Otherwise document and defer.

---

### 7. Edge Case & Error Handling
- "What happens when input is empty, null, malformed, or extreme?"
- "What happens when a dependency fails (network, DB, file)?"
- "What happens on race conditions or concurrent access?"
- "Are errors checked, logged, and actionable — or silently swallowed?"
- Apply **Popperian Falsification**: what test input would prove this implementation wrong?

---

### 8. Performance at Code Level
- Algorithmic complexity (is the right data structure being used?)
- N+1 queries, unnecessary allocations, hidden copies
- Hot path vs cold path — is optimization targeting the right place?
- Apply **Occam's Razor**: don't optimize what doesn't need optimization. Measure first.

---

## Output Structure

1. What works well in this code (MUST come first — avoids critic bias)
2. Decision triage (reversibility + blast radius)
3. First Principles decomposition (essential vs accidental complexity)
4. Code smells detected (with severity: harmless / warning / blocker)
5. Design evaluation (patterns justified? Occam check.)
6. Testability assessment
7. Cohesion & coupling analysis
8. Technical debt estimate (cost now vs cost later)
9. Edge case analysis
10. Recommendation with explicit confidence level

---

## Goal
Improve code quality by applying systematic philosophical scrutiny to implementation decisions, not just architecture.

---

## Context checkpoint
Before issuing a recommendation, declare any assumptions about:
- Team's familiarity with the codebase and domain
- Existing test coverage and CI quality
- Time pressure and delivery constraints

If user has not provided this information, qualify the recommendation: "This assumes [X]. If [not X], [alternative recommendation]."
