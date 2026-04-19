# deprecated/ — 非推奨スキルのアーカイブ

このディレクトリは、本リポジトリで一度公開された（もしくは予告された）スキルのうち、改訂や統廃合によって現役から外れたものを保管する場所です。削除ではなくアーカイブとしているのは、[DESIGN.md §5.4](../DESIGN.md#54-deprecated-への移動) に定めた非推奨化ポリシーに基づきます。

## 現在の非推奨スキル

| スキル | 非推奨化 | 主な代替 |
|---|---|---|
| [advanced-prompting-for-admin](advanced-prompting-for-admin/) | 2026-04-19 (v0.4.0) | [skills/staff-ai-literacy-primer](../skills/staff-ai-literacy-primer/) |
| [ai-report-evaluation](ai-report-evaluation/) | 2026-04-19 (v0.4.0) | [domain-skills/research-support/research-integrity-ai-disclosure](../domain-skills/research-support/research-integrity-ai-disclosure/) / [domain-skills/academic-affairs/syllabus-ai-policy](../domain-skills/academic-affairs/syllabus-ai-policy/) |
| [tool-selection-guide](tool-selection-guide/) | 2026-04-19 (v0.4.0) | [skills/institutional-ai-adoption-checklist](../skills/institutional-ai-adoption-checklist/) |

各スキルの README に、非推奨化の経緯と代替先への案内を記しています。

## なぜ削除せずに残すのか

本リポジトリは以下の3つの理由から、陳腐化したスキルを `deprecated/` に移動する運用を取っています。

1. **過去の参照者保護** — 研修資料、稟議書、学内ガイドライン、外部の記事などが旧スキルへリンクしている可能性があります。削除するとリンク切れが発生し、参照者の不利益になります。
2. **履歴としての価値** — 「かつてこういう判断枠組みを想定していた」という記録自体が、後続の設計議論や研究対象として参照価値を持ちます。
3. **復活の可能性** — AI サービス仕様、法制度、大学のガバナンス環境が変われば、一度非推奨化したスキルが再び有効になる余地があります。必要になったときに履歴から復元できるよう残しておきます。

## リポジトリへ戻る

- [リポジトリトップ](../README.md)
- [DESIGN.md](../DESIGN.md) — 設計思想と非推奨化ポリシー
- [CHANGELOG.md](../CHANGELOG.md) — 各バージョンでの移動記録
