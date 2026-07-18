# Agent Capability Intake

[English](../../README.md) · [繁體中文](../zh-Hant/README.md) · [日本語](README.md)

これは、外部の AI エージェント機能をローカル環境に取り込むべきか判断するための、evidence-first のガバナンス・キットです。

skill、prompt、hook、MCP server、plugin、agent、CLI wrapper、runtime package は、確認が済むまで未審査のソースとして扱います。基本の流れは次のとおりです。

```text
外部ソース → digest（精査） → absorb（導入） | no-absorb（不採用）
```

## この流れが必要な理由

agent capability を導入すると、agent が参照できる情報、呼び出せるツール、実行できる操作が変わります。人気があること、十分なドキュメントがあること、demo で動いたことだけでは、有効化の根拠になりません。

このキットでは、混同されがちな三つの行為を分けます。

1. **digest（精査）**：出所とバージョンを確認し、内容、適合性、リスクを評価して、あとで参照できる結論を残します。この段階で実行権限は与えません。
2. **absorb（導入）**：承認した動作だけを指定のローカル surface に反映し、検証を行い、rollback path を残します。
3. **no-absorb（不採用）**：導入しない理由、代替案、再検討する条件を明記します。これは未完了ではなく、完結した判断です。

## 守るべき原則

- digest では、ソースを install、enable、execute してはいけません。
- absorb はローカル環境向けに必要な動作を再構成して導入する判断であり、upstream instruction のそのままの複製ではありません。
- active capability には、source、owner、risk tier、検証の証拠、rollback または retirement path が必要です。
- `no-absorb` の判断は見つけられる状態に保ち、同じソースを何度も調査しないようにします。
- 自動化は記録を検証できますが、ソースを勝手に active へ昇格させてはいけません。

## はじめ方

1. [`templates/intake-record.md`](../../templates/intake-record.md) から intake record を作成します。
2. ソースを有効化せずに digest を完了します。
3. disposition を一つだけ選びます。
   - [`absorb`](../../templates/absorb-decision.md)
   - [`no-absorb`](../../templates/no-absorb-decision.md)
   - 利用を止める必要がある安全上の懸念がある場合は `quarantine`
4. `absorb` を選ぶ場合は、runtime を変更する前に pass/fail checks と rollback を定義します。
5. record は、チームが authoritative として扱う capability registry または decision log に保存します。

## 対象

agent の動作や権限に影響する外部カスタマイズを対象にします。

- skills、prompts、instructions、custom agents、templates
- hooks、plugins、extensions、CLI wrappers、runtime packages
- MCP servers とその他の connected tools

このキットは package manager、runtime sandbox、security scanner、自動承認エンジンではありません。必要に応じて、プラットフォームの制御や CI と組み合わせてください。

## リポジトリ構成

- [`SPEC.md`](../../SPEC.md) — 状態モデル、decision gate、最低限の証拠。
- [`schemas/intake-record.schema.json`](../../schemas/intake-record.schema.json) — 持ち運び可能な machine-readable record の形式。
- [`templates/`](../../templates/) — 人がレビューするための Markdown records。
- [`examples/`](../../examples/) — 安全に導入する判断と、理由を残した不採用の例。
- [`i18n/`](../README.md) — 翻訳の配置と保守ルール。

## ステータス

これは初期段階の reference implementation です。schema と template は意図的に小さくしています。intake decision を明確にし、安全にし、あとから見直しやすくできるかについてのフィードバックを歓迎します。

## ライセンス

[MIT](../../LICENSE)
