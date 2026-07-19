# Agent Capability Intake

[English](README.md) · [繁體中文](i18n/zh-Hant/README.md) · [日本語](i18n/ja/README.md)

> **A direction, not a runbook.**
>
> This repository gives people and AI agents a model for reasoning about external agent capabilities. It does not prescribe every step, runtime, or implementation. Start with [GUIDE.md](GUIDE.md), then read only the next document your question needs.

An evidence-first governance kit for deciding whether an external AI-agent capability may enter a local environment.

It treats a skill, prompt, hook, MCP server, plugin, agent, CLI wrapper, or runtime package as **untrusted until reviewed**. The central rule is simple:

```text
external source -> digest -> absorb | no-absorb
```

## Why this exists

Installing an agent capability changes what an agent can know, invoke, or mutate. A popular repository, vendor documentation, or a successful demo is not sufficient authorization to enable it.

This kit separates three actions that are often accidentally collapsed:

1. **Digest** — establish provenance, understand the source, assess fit and risk, and preserve a reusable conclusion. It grants no execution authority.
2. **Absorb** — materialize only the approved behavior into a named local surface, then verify it and retain a rollback path.
3. **No-absorb** — explicitly decline activation, including the reason, alternative, and a re-review trigger if one is useful. This is a successful outcome.

## Invariants

- Digesting must not install, enable, or execute the source.
- Absorption is a local re-authoring decision, not a byte-for-byte copy of upstream instructions.
- Every active capability needs a source, owner, risk tier, verification evidence, and rollback or retirement path.
- `no-absorb` decisions remain discoverable so the same source is not repeatedly re-investigated.
- Automation can validate records; it must not silently promote a source to active.

## Capability discovery and layered loading

An approved capability can still create context debt if every rule and reference is loaded for every task. Treat discovery and loading as part of the activation design.

1. **Always-on contract** — keep global or repository instructions thin: authority boundaries, completion rules, and the triggers that require a deeper read.
2. **Capability catalog** — expose only a skill's name and short description until it is relevant. The description is a routing interface, not a rulebook or a security decision.
3. **Selected skill** — load the full `SKILL.md` only after selection. It should state the workflow contract, safety boundary, and a direct map to the material that may be needed next.
4. **References** — read an individual reference only when its explicit trigger applies. Put cross-skill policy in a stable shared `references/` area; keep workflow-specific detail beside the skill.
5. **Scripts and templates** — make these available to the selected skill, but do not inject their contents as standing instructions.

Do not recursively include long reference trees from a top-level instruction file. Some runtimes concatenate imported instruction files eagerly, which defeats progressive loading. A relevance match may select a skill; it never authorizes installation, tool pre-approval, or activation.

Current implementations differ, but the distinction between catalog metadata, selected instructions, and on-demand material is documented by [Codex](https://developers.openai.com/codex/codex-manual.md#customization-and-tooling), [Claude Code](https://code.claude.com/docs/en/slash-commands), and [GitHub Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills). [Gemini CLI](https://geminicli.com/docs/cli/gemini-md/) is a useful counterexample: its hierarchical context files are concatenated for each prompt, so they must remain especially small.

## Quick start

1. Create an intake record from [`templates/intake-record.md`](templates/intake-record.md).
2. Complete the digest without enabling the source.
3. Choose exactly one disposition:
   - [`absorb`](templates/absorb-decision.md)
   - [`no-absorb`](templates/no-absorb-decision.md)
   - `quarantine` when a material safety concern must block use.
4. For `absorb`, define pass/fail checks and rollback before changing a runtime.
5. Store the record beside the capability registry or decision log your team treats as authoritative.

## Scope

Use this kit for externally supplied agent customization that can affect behavior or authority:

- skills, prompts, instructions, custom agents, and templates
- hooks, plugins, extensions, CLI wrappers, and runtime packages
- MCP servers and other connected tools

It is deliberately not a package manager, a runtime sandbox, a security scanner, or an automatic approval engine. Pair it with platform controls and CI where available.

## Repository map

- [`GUIDE.md`](GUIDE.md) — a concise reading map for people and agents.
- [`SPEC.md`](SPEC.md) — state model, decision gate, and minimum evidence.
- [`schemas/intake-record.schema.json`](schemas/intake-record.schema.json) — portable machine-readable record shape.
- [`templates/`](templates/) — Markdown records for human review.
- [`examples/`](examples/) — a safe absorption decision and a documented decline.
- [`i18n/`](i18n/README.md) — translation layout and maintenance rules.

## Status

Early reference implementation. The schema and templates are intentionally small; feedback should focus on whether they make intake decisions clearer, safer, and easier to revisit.

## License

[MIT](LICENSE)
