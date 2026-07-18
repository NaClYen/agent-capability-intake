# Agent Capability Intake

[English](../../README.md) · [繁體中文](README.md) · [日本語](../ja/README.md)

這是一套以證據為先的治理工具組，用來判斷外來 AI agent capability 是否應進入本機環境。

它把 skill、prompt、hook、MCP server、plugin、agent、CLI wrapper 與 runtime package 視為尚未審查的來源。核心流程很簡單：

```text
外部來源 → 消化 → 吸收 | 不吸收
```

## 為什麼需要這套流程

安裝 agent capability 會改變 agent 能取得的資訊、能呼叫的工具，或能執行的動作。來源很熱門、有完整文件，或曾在 demo 中成功運作，都不足以成為啟用它的理由。

這套工具組把三件常被混在一起的事分開：

1. **消化**：確認來源與版本、理解內容、評估適配性和風險，並留下日後可回查的結論。這一步不授予任何執行權限。
2. **吸收**：只把已核准的行為落到指定的本機 surface，完成驗證，並保留 rollback path。
3. **不吸收**：清楚記錄不啟用的原因、替代方案，以及值得重新檢視的條件。這是完整的決策結果，不是未完成的工作。

## 不可破壞的原則

- 消化來源不能安裝、啟用或執行來源內容。
- 吸收是依本機環境重寫與落地的決策，不是直接複製上游 instruction。
- 每個 active capability 都要有來源、owner、risk tier、驗證證據，以及 rollback 或 retirement path。
- `no-absorb` 決策必須可被找到，避免同一來源反覆被重新研究。
- 自動化可以檢查紀錄，但不能自行把來源升格為 active。

## 快速開始

1. 從 [`templates/intake-record.md`](../../templates/intake-record.md) 建立 intake record。
2. 在不啟用來源的前提下完成消化。
3. 只選擇一個 disposition：
   - [`absorb`](../../templates/absorb-decision.md)
   - [`no-absorb`](../../templates/no-absorb-decision.md)
   - 若有需要阻止使用的實質安全疑慮，選擇 `quarantine`。
4. 若選擇 `absorb`，在改動 runtime 前先寫下 pass/fail checks 與 rollback。
5. 把 record 放到團隊認定為 authoritative 的 capability registry 或 decision log。

## 適用範圍

這套工具組適合處理可能改變 agent 行為或權限的外部客製化來源：

- skills、prompts、instructions、custom agents 與 templates
- hooks、plugins、extensions、CLI wrappers 與 runtime packages
- MCP servers 與其他 connected tools

它不是 package manager、runtime sandbox、安全掃描器，也不是自動批准引擎。需要時，請搭配平台本身的安全控制與 CI。

## Repo 結構

- [`SPEC.md`](../../SPEC.md) — 狀態模型、決策 gate 與最低證據要求。
- [`schemas/intake-record.schema.json`](../../schemas/intake-record.schema.json) — 可攜的 machine-readable record 格式。
- [`templates/`](../../templates/) — 供人工審查使用的 Markdown records。
- [`examples/`](../../examples/) — 一個安全吸收決策與一個具理由的不吸收決策。
- [`i18n/`](../README.md) — 翻譯目錄與維護規則。

## 狀態

這是早期的 reference implementation。schema 與模板刻意保持精簡；最需要的回饋是：它們是否讓 intake decision 更清楚、更安全，也更容易在未來重新檢視。

## 授權

[MIT](../../LICENSE)
