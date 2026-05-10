# Roadmap

このページは、準備中の skill、非推奨 skill、次の整備方針をまとめます。実際の追加時期は、利用者からの要望、出典確認、ライセンス確認、レビュー体制によって変わります。

## 整備方針

`higher-ed-ai-skills` は、AI 活用支援ではなく、大学職員が AI エージェントに大学業務を頼むための skill 集として整備します。

現行版では、README / docs の入口再設計、全 active `SKILL.md` の unified protocol 移行、`create-action-skill` の旧分類撤去、Claude Code adapter の軽量化を実施済みです。次は、実務領域の追加、検査自動化、例文の継続レビューを優先します。

## 次に優先する保守

- README の skill catalog と `SKILL.md` frontmatter のずれを検出する検査を追加する。
- 例文が本文方針と矛盾しないかを検査するチェックリストを整備する。
- `docs/install.md` と runtime adapter を、各ランタイムの仕様変更に合わせて半期ごとに確認する。
- deprecated skill が現行 skill と同時に導入されないよう、導入ガイドと検査を強化する。

## 次に増やしたい大学業務領域

| 領域 | 候補 skill | 位置付け |
|---|---|---|
| 稟議・起案・承認経路 | `ringi-approval-route`, `approval-document-drafting` | 総務・企画・部局事務の中核業務を扱う |
| 会議体運営 | `committee-agenda-routing`, `decision-log-management` | 議題分類、審議/報告区分、決定事項管理を扱う |
| 文書管理・記録 | `document-retention-and-disclosure`, `metadata-removal-check` | 保存年限、配布範囲、公開請求、メタデータ除去を扱う |
| 職員研修・SD | `staff-development-training-design` | ローカル `training-development` から公開版へ翻案 |
| IR・内部質保証 | `university-dashboard-design`, `quality-assurance-evidence-review` | ローカル `dashboard-design-guidebook` から高等教育向けへ翻案 |
| 文書レビュー | `university-document-team-review` | ローカル `team-review` から大学文書レビューへ抽出 |
| ナレッジサイト運営 | `university-knowledge-site-maintenance` | `p4us-renovate` の汎用部分を抽出 |

## 準備中

| 候補 | 位置付け | 状態 |
|---|---|---|
| `staff-development-training-design` | 大学職員研修の設計・レビュー skill | ローカル skill から公開版へ翻案検討 |
| `university-dashboard-design` | IR・教学・経営ダッシュボード設計 skill | デジタル庁資料の利用条件と高等教育向け翻案を確認中 |
| `university-document-team-review` | 大学文書の多角的レビュー skill | tool 依存を整理し公開版へ抽出検討 |
| `ringi-approval-route` | 稟議・承認経路の整理 skill | 新規設計候補 |
| `document-retention-and-disclosure` | 文書保存・公開請求・配布範囲の整理 skill | 新規設計候補 |

## 非推奨 skill

過去に準備中または公開済みだった枠のうち、既存 skill に吸収したものは [deprecated/](../deprecated/) に保存しています。

| 非推奨 skill | 代替 |
|---|---|
| [advanced-prompting-for-admin](../deprecated/advanced-prompting-for-admin/) | [staff-ai-literacy-primer](../skills/staff-ai-literacy-primer/) |
| [ai-report-evaluation](../deprecated/ai-report-evaluation/) | [research-integrity-ai-disclosure](../domain-skills/research-support/research-integrity-ai-disclosure/) + [syllabus-ai-policy](../domain-skills/academic-affairs/syllabus-ai-policy/) |
| [tool-selection-guide](../deprecated/tool-selection-guide/) | [institutional-ai-adoption-checklist](../skills/institutional-ai-adoption-checklist/) |

非推奨 skill は削除しません。過去の参照保護と設計履歴のために残します。
