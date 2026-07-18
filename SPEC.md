# Capability Intake Specification (v0.1)

## 1. State model

```text
discovered -> digested -> { absorbed | no-absorb | quarantined }
                                |
                             retired
```

`digested` means the source was understood well enough to decide. It does not mean the source is installed or loadable.

## 2. Digest gate

Before a disposition, record:

- publisher and source URL
- immutable identity where available: commit SHA, package integrity, or artifact hash
- source type, license, and review date
- intended capability, local use case, and plausible alternatives
- authority change: read, write, execute, network, authentication, delegation, or external side effects
- risk tier: `low`, `medium`, `high`, or `critical`
- known security, drift, compatibility, and maintenance concerns

The digest may archive evidence and create a decision record. It must not install packages, write runtime configuration, enable connected tools, or run source-provided setup.

## 3. Disposition gate

### Absorb

Absorption is justified only when a concrete local need exists and the approved behavior has a named destination.

Before activation, define:

- local target surface and accountable owner
- approved behavior and intentionally excluded upstream behavior
- verification command or inspection and expected result
- rollback or disable procedure
- review trigger for source updates, trust changes, or runtime changes

Absorb the minimum useful behavior. A local rewrite is normally preferable to copying an upstream instruction bundle unchanged.

### No-absorb

Use `no-absorb` when value, safety, compatibility, maintenance, or duplication does not justify activation. Record the reason and a viable alternative. Set a re-review trigger only when a concrete change could alter the decision.

### Quarantine

Use `quarantine` when the source has a material trust or safety concern. If it was active, disable its load path first; preserve enough evidence to explain the decision.

## 4. Risk tiers

| Tier | Typical source | Minimum gate |
| --- | --- | --- |
| low | read-only prompt or reference pattern | provenance, fit review, decision record |
| medium | skill, custom agent, reusable template | source snapshot, local rewrite, target verification |
| high | hook, plugin, MCP, CLI, runtime package | immutable identity, authority/dependency review, smoke test, rollback |
| critical | auto-execution, credential access, production or destructive action | explicit human approval, isolated proof, recovery plan, post-change verification |

## 5. Non-goals

- This specification does not certify a source as secure.
- It does not replace sandboxing, platform policy, code review, secrets management, or vendor controls.
- It does not mandate one registry, file format, runtime, or automation tool.
- It does not authorize external writes merely because a capability was absorbed.
