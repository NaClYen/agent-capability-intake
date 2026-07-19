# 閱讀指南

這個儲存庫為思考外來代理能力提供方向。它不是既定流程、執行環境整合指南，也不能取代判斷。人與 AI 代理只應閱讀眼前問題所需的下一份文件。

## 選擇下一份文件

- 想理解目的、詞彙與 `digest` 和 `absorb` 的核心界線時，讀 [`README.md`](README.md)。
- 評估來源或做出處理決策時，讀 [`SPEC.md`](../../SPEC.md)。
- 產生或驗證供機器讀取的紀錄時，讀 [`schemas/intake-record.schema.json`](../../schemas/intake-record.schema.json)。
- 準備供人審查的紀錄時，讀 [`templates/`](../../templates/)。
- 需要具體決策協助理解模型時，讀 [`examples/`](../../examples/)。

## 保留模型的界線

`digest` 代表已理解到足以做決定；它不會安裝、啟用、執行或預先核准來源。`absorb`、`no-absorb` 與 `quarantine` 是不同的決定；只有在現有證據足以支持時才選擇其中一種。

這個儲存庫的任何文件都不授權啟用能力。若相關文件仍留有重要問題，應記錄缺口，而不是以假設補上答案。

## 依據來源

[`SPEC.md`](../../SPEC.md) 定義具規範性的決策契約。結構定義、範本與範例讓這份契約能以不同形式使用，但不會取代它。

[English](../../GUIDE.md) · [繁體中文](GUIDE.md) · [日本語](../ja/GUIDE.md)
