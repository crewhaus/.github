<h1 align="center">CrewHaus</h1>

<p align="center"><strong>One spec. Every agent shape.</strong></p>

<p align="center"><em>The open-source meta-harness compiler for AI agents.</em></p>

<p align="center">
  <a href="https://crewhaus.ai">Website</a> ·
  <a href="https://crewhaus.ai/docs">Docs</a> ·
  <a href="https://github.com/crewhaus/docs/blob/main/GETTING-STARTED.md">Getting started</a> ·
  <a href="https://github.com/crewhaus/docs/blob/main/COMPILER-ARCHITECTURE.md">Compiler architecture</a> ·
  <a href="https://github.com/crewhaus/docs/blob/main/whitepaper/crewhaus-meta-harness-compiler.pdf">Whitepaper</a>
</p>

<p align="center">
  <a href="https://github.com/crewhaus/factory/blob/main/LICENSE"><img alt="License: Apache-2.0" src="https://img.shields.io/badge/license-Apache--2.0-2ECC8B" /></a>
  <img alt="Runtime: TypeScript + Bun" src="https://img.shields.io/badge/runtime-TypeScript%20%2B%20Bun-2ECC8B" />
</p>

---

## What is CrewHaus?

An agent's runtime is normally hand-written per shape. The same research assistant is one thing as a terminal CLI, another as a Slack bot, another again as an eval bundle that grades it. Each shape is a separate harness with its own wiring, and the prompts that drive the agent are duplicated across all of them with no single place to tune them.

CrewHaus lifts that one level up. You write the agent once, as a spec — a `crewhaus.yaml` — and the compiler emits a runtime-thin bundle for whichever shape you need: a CLI, a channel bot, a RAG pipeline, a multi-agent crew, an eval harness, a voice/realtime agent, a browser/computer-use agent, and more as the IR grows. Each one is emitted as code idiomatic to its runtime, not a generic wrapper. Change the spec and every shape recompiles. Run the eval loop and `crewhaus optimize` rewrites the spec from its own failures, so the fix lands in all of them at once.

It helps to be precise about the layer. Agent frameworks like LangGraph, CrewAI, and AutoGen are runtimes — each bakes its own runtime assumptions into its API. CrewHaus is the compiler that emits *to* runtimes; it does not compete with them. Its IR carries those shapes as target variants (`IrGraphV0`, `IrCrewV0`), so the same spec can compile to either one, or to a third shape entirely, without rewriting your agent logic. The reference class is build tools and IR-based compilers — LLVM, Bazel, Terraform — not agent frameworks. CrewHaus is the layer above the runtimes.

Apache-2.0. Built in TypeScript on Bun.

## The three pillars

Three things make CrewHaus more than a build tool.

1. **The compiler is the protagonist.** Specs flow through `parseSpec → lower → applyPasses → emit`. The IR is a discriminated union of target-shape variants, and each emitter consumes its own typed variant. Adding a new shape starts at the IR, not at codegen.

2. **Eval is active, not passive.** Eval failures produce *spec patches*, not just dashboards. `crewhaus optimize` searches the mutation space — rule-based or Claude-driven — and writes back through a YAML CST that preserves comments and key order. The loop closes, and because it optimizes the spec rather than any single output, every emitted shape improves together.

3. **Security is a fabric, not a perimeter.** Untrusted content — MCP responses, sub-agent returns, channel inbound messages, federation payloads, skill bodies, compaction summaries — passes through a single boundary classifier and is tagged with `TrustOrigin` before it reaches a model call. Authentication verifies who; classification verifies what.

The canonical, always-current list of target shapes lives in the [compiler-architecture reference](https://github.com/crewhaus/docs/blob/main/COMPILER-ARCHITECTURE.md) and the [module catalog](https://github.com/crewhaus/docs/blob/main/MODULE-CATALOG.md). The set grows over time, so those are the source of truth.

## Getting started

Requires [Bun](https://bun.sh) ≥ 1.2.

```bash
bun add -d @crewhaus/cli

# Create a new agent project — writes a minimal crewhaus.yaml
bun x crewhaus init my-agent
cd my-agent

# Add a model credential (Anthropic by default), in a .env file
echo 'ANTHROPIC_AUTH_TOKEN=sk-ant-oat01-...' > .env   # Pro/Max OAuth
# or: echo 'ANTHROPIC_API_KEY=sk-ant-...'    > .env    # pay-per-token

# Compile crewhaus.yaml to a runnable bundle, then run it
bun x crewhaus compile crewhaus.yaml -o build
bun x crewhaus run crewhaus.yaml
```

To compile the same agent to a different shape, change `target:` in `crewhaus.yaml` to another value from the targets table and re-run `crewhaus compile`. The agent logic stays the same; only the emitted runtime changes.

From there, read the [getting-started guide](https://github.com/crewhaus/docs/blob/main/GETTING-STARTED.md) — a guided tour from first principles to a runnable agent.

## Projects

| Repo | What it is |
|---|---|
| [`factory`](https://github.com/crewhaus/factory) | The compiler. Parse, lower, optimize, emit — the typed IR, every target emitter, the eval loop, and the boundary classifier. Apache-2.0. |
| [`docs`](https://github.com/crewhaus/docs) | Documentation source: the getting-started guide, the compiler-architecture reference, the module catalog and briefs, and the whitepaper (CC-BY-4.0). |
| [`demos`](https://github.com/crewhaus/demos) | Runnable, copy-pasteable starters for every target shape, plus task-oriented walkthroughs. |
| [`utilities`](https://github.com/crewhaus/utilities) | Studio and IDE tooling around the compiler: the spec-authoring studio daemon and UI, a guided wizard, trace and graph visualizers, a browser playground, and VS Code and JetBrains integrations. |

CrewHaus Forge — a community registry for shared harnesses, skills, tools, and recipes — is on the way.

## Whitepaper

*CrewHaus: A Meta-Harness Compiler for AI Agents* — the positioning and architecture paper. Read it in the docs repo: [`whitepaper/crewhaus-meta-harness-compiler.pdf`](https://github.com/crewhaus/docs/blob/main/whitepaper/crewhaus-meta-harness-compiler.pdf) ([Markdown source](https://github.com/crewhaus/docs/blob/main/whitepaper/crewhaus-meta-harness-compiler.md)). The whitepaper is licensed [CC-BY-4.0](https://github.com/crewhaus/docs/blob/main/whitepaper/LICENSE).

## License

The compiler and all supporting code are open source under [Apache-2.0](https://github.com/crewhaus/factory/blob/main/LICENSE). The [whitepaper](https://github.com/crewhaus/docs/tree/main/whitepaper) is [CC-BY-4.0](https://github.com/crewhaus/docs/blob/main/whitepaper/LICENSE). CrewHaus is fully usable on your own machine.

**CrewHaus**, **CrewHaus Factory**, and the logo are trademarks; see [TRADEMARK.md](https://github.com/crewhaus/factory/blob/main/TRADEMARK.md) for the use-of-marks policy. The trademarks are not granted by the code license.

## Built by [StudioMax](https://studiomax.io)

CrewHaus is built and maintained by [StudioMax](https://studiomax.io). The open source is genuinely useful on its own — clone it, run `crewhaus init`, and ship a real agent without paying.
