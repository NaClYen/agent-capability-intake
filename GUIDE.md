# Guide

This repository offers a direction for reasoning about external agent capabilities. It is not a prescribed workflow, a runtime integration guide, or a substitute for judgment. People and AI agents should read only the next document their question requires.

## Choose the next document

- Read [`README.md`](README.md) for the purpose, vocabulary, and core boundary between `digest` and `absorb`.
- Read [`SPEC.md`](SPEC.md) when evaluating a source or making a disposition.
- Read [`schemas/intake-record.schema.json`](schemas/intake-record.schema.json) when producing or validating a machine-readable record.
- Read [`templates/`](templates/) when preparing a record for human review.
- Read [`examples/`](examples/) when a concrete decision would clarify the model.

## Keep the model intact

`digest` establishes enough understanding to decide. It does not install, enable, execute, or pre-approve a source. `absorb`, `no-absorb`, and `quarantine` are distinct decisions; choose one only when the available evidence supports it.

No document in this repository authorizes activation. If the relevant document leaves a material question open, record the gap instead of filling it with an assumption.

## Source of truth

[`SPEC.md`](SPEC.md) defines the normative decision contract. The schema, templates, and examples make that contract usable in different forms; they do not replace it.

[English](GUIDE.md) · [繁體中文](i18n/zh-Hant/GUIDE.md) · [日本語](i18n/ja/GUIDE.md)
