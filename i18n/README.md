# Translations

The English files in the repository root are the normative source. Localized documents live under `i18n/<BCP-47-language-tag>/` so a locale can later include `README.md`, `SPEC.md`, and other public documentation without changing the repository layout.

Current locales:

- [`zh-Hant README`](zh-Hant/README.md) · [`Guide`](zh-Hant/GUIDE.md) — Traditional Chinese
- [`ja README`](ja/README.md) · [`Guide`](ja/GUIDE.md) — Japanese

## Maintaining a translation

- Translate meaning, not sentence shape. Translate explanatory prose and ordinary technical or operational terms into natural target-language wording; do not require line-for-line correspondence with English.
- Preserve document structure, links, code blocks, commands, paths, identifiers, and risk-tier values. Translate headings naturally. Keep project and protocol names, JSON keys, CLI commands, filenames, URLs, and stable lifecycle tokens exact when translation would make cross-language operation ambiguous.
- Update the locale document when the corresponding English document changes materially. A translation must preserve the same normative meaning even when its wording differs.
- Do not translate names, file paths, JSON keys, CLI commands, code samples, or Markdown link destinations.
- Add a language only when someone can review and maintain it. A machine-generated file without review is not a supported translation.
- Use a BCP 47 tag for each directory, for example `fr`, `pt-BR`, `zh-Hans`, or `ko`.

Translations describe this repository; they do not change its normative contract. When a localized document conflicts with the English source, the English source governs until the translation is corrected.
