# Agent Capability Intake

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

- [`SPEC.md`](SPEC.md) — state model, decision gate, and minimum evidence.
- [`schemas/intake-record.schema.json`](schemas/intake-record.schema.json) — portable machine-readable record shape.
- [`templates/`](templates/) — Markdown records for human review.
- [`examples/`](examples/) — a safe absorption decision and a documented decline.

## Status

Early reference implementation. The schema and templates are intentionally small; feedback should focus on whether they make intake decisions clearer, safer, and easier to revisit.

## License

[MIT](LICENSE)
