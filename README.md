# Sogno AgentFlow

**Deterministic Software Engineering for AI Coding Agents.**

AgentFlow is an open-source workflow engine that brings **executable specifications, test-driven development, verifiable quality gates, and human approvals** to AI-assisted software engineering.

AI coding agents can write code quickly. AgentFlow is designed to make the *process* of accepting that code explicit, repeatable, and reviewable.

> **AI writes. Tests verify. Humans decide.**

## Why AgentFlow?

An agent's claim that a feature is complete is not evidence that it behaves correctly. AgentFlow structures implementation as a sequence of controlled transitions, backed by real test execution rather than the agent's self-assessment.

The project combines:

- **BDD / acceptance testing** to define observable behavior before implementation.
- **TDD** to guide implementation through small red–green–refactor steps.
- **Deterministic workflow transitions** enforced by scripts and verifiable checks.
- **Quality gates** for architecture, coverage, and mutation testing.
- **Human approval points** for scope and key decisions.
- **Traceability** from scenarios to implementation iterations and reports.

AgentFlow is **not** another coding agent, an LLM orchestration framework, or a replacement for Claude Code, Codex, Gemini CLI, or OpenCode. It is a workflow layer intended to work *with* coding agents.

## How it works

```text
Business specification (Gherkin)
             │
             ▼
      Plan implementation
             │
             ▼
     Human review of plan
             │
             ▼
    Scope / iteration framing
             │
             ▼
        Acceptance RED
             │
             ▼
       ┌──────────────┐
       │   Unit RED   │
       │      ↓       │
       │  Unit GREEN  │
       │      ↓       │
       │   REFACTOR   │◄── repeat as needed
       └──────────────┘
             │
             ▼
     Verification gates
             │
             ▼
      Report + review
```

The outer BDD loop defines *what must work*. The inner TDD loop guides *how the behavior is implemented*. AgentFlow's state machine controls when an iteration may advance.

## Current implementation

The initial implementation is a **Claude Code plugin** targeting **Java 21 / Quarkus 3** projects. It is being prepared for a public open-source release.

Its current design includes:

| Area | Current approach |
| --- | --- |
| Agent integration | Claude Code skills, agents, and hooks |
| Workflow control | Shell-based deterministic state machine |
| Acceptance tests | Cucumber / Gherkin |
| Unit tests | JUnit |
| Architecture checks | ArchUnit |
| Coverage | JaCoCo |
| Mutation testing | PIT |
| Project metadata | `.bddtdd/` plan, state, reports, and iteration records |

The workflow covers scenario planning, iteration framing, acceptance-test failure, unit-test red/green/refactor cycles, and completion checks. Some checks and protections are still being hardened and validated for public use.

**Status: pre-release.** The architecture and commands may change. No general-purpose, multi-agent support is claimed yet.

## Design principles

1. **Evidence over assertions.** An agent saying “tests pass” is not a quality gate; the tests must actually run.
2. **Deterministic transitions.** Workflow advancement is decided by executable checks, not model judgment alone.
3. **Human ownership.** People approve meaningful changes in scope and remain responsible for accepting outcomes.
4. **Small, reviewable increments.** Implement one behavioral slice at a time.
5. **Specifications before implementation.** Behavioral examples and applicable constraints guide the work.
6. **Defense in depth.** Agent hooks help guide behavior, but are not a security boundary. Independent CI checks are essential.
7. **Agent independence.** The workflow engine should not be coupled to one coding agent.
8. **Technology adapters.** Language- and framework-specific checks belong outside the core workflow model.

## Planned architecture

```text
agentflow/
├── core/                 # State machine, transitions, verification contracts
├── agents/               # Coding-agent integrations
│   ├── claude-code/
│   ├── codex/             # Planned
│   ├── opencode/          # Planned
│   └── gemini-cli/        # Planned
├── stacks/               # Language/framework test adapters
│   └── java-quarkus/
├── docs/
└── tests/
```

This is a **target architecture**, not a statement that every directory or integration is already implemented.

## Roadmap

- [ ] Harden the existing Claude Code / Java–Quarkus implementation.
- [ ] Add self-tests for workflow transitions, failure paths, and guardrails.
- [ ] Run independent CI checks against a reproducible example project.
- [ ] Publish installation and end-to-end usage instructions.
- [ ] Separate the deterministic core from agent and technology adapters.
- [ ] Add Codex, OpenCode, and Gemini CLI integrations incrementally.
- [ ] Expand support for specification-driven development, contracts, and architecture decisions where they add verifiable value.

Roadmap items are intentions, not release commitments.

## Installation

AgentFlow is **not yet published as a supported release**. Installation instructions and a minimal example project will be provided once the initial public version is validated.

## Security and limitations

AgentFlow is a **development workflow control system**, not a sandbox or a guarantee of secure code.

- Agent-specific hooks and shell-command restrictions can be incomplete or bypassable.
- Passing tests, coverage thresholds, and mutation scores do not prove correctness or security.
- Generated tests require meaningful assertions and review.
- Independent CI should rerun relevant checks outside the agent's control.
- Human review remains necessary for architecture, security-sensitive behavior, and releases.

Please do not rely on the pre-release implementation as the sole enforcement mechanism for sensitive repositories.

## Contributing

Contributions and design discussions are welcome as the project opens up. Contribution guidelines and a security-reporting process will be added before the first supported release.

## License

AgentFlow is intended to be released under the **Apache License, Version 2.0**. The repository's `LICENSE` file will contain the authoritative license text when the public release is prepared.

## About Sogno.ai

**Sogno.ai** is an open-source initiative exploring practical tools for AI-assisted software engineering.

AgentFlow is its current focus. Other experiments, including Romano and Llumn, are paused.
