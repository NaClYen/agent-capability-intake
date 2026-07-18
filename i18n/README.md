# Translations

The English files in the repository root are the canonical source. Localized documents live under `i18n/<BCP-47-language-tag>/` so a locale can later include `README.md`, `SPEC.md`, and other public documentation without changing the repository layout.

Current locales:

- [`zh-Hant`](zh-Hant/README.md) — Traditional Chinese
- [`ja`](ja/README.md) — Japanese

## Maintaining a translation

- Keep headings, links, code blocks, commands, paths, identifiers, and risk-tier values aligned with the English source unless a locale needs a short explanation for clarity.
- Update the locale document when the corresponding English document changes materially. Small wording changes do not require a mechanical line-for-line update.
- Do not translate names, file paths, JSON keys, CLI commands, or code samples.
- Add a language only when someone can review and maintain it. A machine-generated file without review is not a supported translation.
- Use a BCP 47 tag for each directory, for example `fr`, `pt-BR`, `zh-Hans`, or `ko`.

Translations describe this repository; they do not change its normative contract. When a localized document conflicts with the English source, the English source governs until the translation is corrected.
