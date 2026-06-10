# Philosopher Skills — Critical Thinking Lenses for Opencode

A set of specialized reasoning skills that turn the [opencode](https://opencode.ai) agent into a philosophical-critical thinker. Instead of just answering, the agent questions assumptions, exposes hidden logic flaws, and stress-tests ideas before conclusions are drawn.

## Skills Overview

| Skill | Domain | Purpose |
|---|---|---|
| **philosopher** *(meta)* | General | Classifies the problem and selects/combines the appropriate lenses |
| **philosopher-general** | General | Constructive skepticism — exposes assumptions, blind spots, contradictions |
| **philosopher-hard** | Stress test | Aggressively tries to break the idea — worst-case reasoning, falsification |
| **philosopher-engineering** | Technology | Evaluates architecture, trade-offs, scalability, over-engineering |
| **philosopher-business** | Business | Analyzes market demand, competition, monetization, execution risk |
| **philosopher-code** | Code | Analyzes implementation quality, code smells, testability, technical debt |
| **philosopher-psychology** | Human behavior | Identifies cognitive biases, motivation gaps, real vs stated behavior |

## Architecture

```
User request
    │
    ▼
┌─────────────────────────────────────┐
│        philosopher (meta-skill)      │
│   • Classifies problem domain        │
│   • Selects 1+ specialized lenses    │
│   • Adjusts critique intensity       │
└─────────────────────────────────────┘
    │
    ├──→ philosopher-general     (simple / early ideas)
    ├──→ philosopher-engineering (technical systems)
    ├──→ philosopher-code        (code quality / implementation)
    ├──→ philosopher-business    (market / monetization)
    ├──→ philosopher-psychology  (user behavior)
    └──→ philosopher-hard        (high-risk ideas)
```

For complex problems, multiple lenses are combined and cross-perspective conflicts are surfaced.

## Installation

Copy the skill folders to your opencode skills directory:

```bash
cp -r skills/* ~/.config/opencode/skills/
```

Then reference them from your `.opencode.jsonc` or agent configuration.

## Usage Examples

**"I want to build a SaaS for X"** → activates *philosopher-business* + *philosopher-hard*  
**"Should I use microservices?"** → activates *philosopher-engineering*  
**"Is this code well-structured?"** → activates *philosopher-code*  
**"Why aren't users converting?"** → activates *philosopher-psychology*  
**"I have an idea for a startup"** → activates *philosopher-general* first, escalates if needed

## Inspirations

- **Socratic method** — questioning assumptions, exposing contradictions
- **Karl Popper's falsificationism** — treating ideas as hypotheses to be broken
- **Charlie Munger's mental models** — applying multiple lenses to a single problem
- **Cynefin framework** — classifying problem domains before acting
- **Kahneman & Tversky** — cognitive biases and heuristics
- **First-principles thinking** (Feynman, Musk) — questioning fundamental premises
- **Systems thinking** — trade-offs, coupling, feedback loops
- **Lean Startup / Business Model Canvas** — market validation

## License

MIT © 2026 Matheus. See [LICENSE](./LICENSE).
