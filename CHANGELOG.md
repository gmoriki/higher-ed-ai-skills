# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.4.0] - 2026-04-19

### Added

- **新規スキル**: `skills/ai-use-risk-classification/` — AI 使用を「禁止／限定／推奨／開放」の 4 区分で判定（上海交大 4 分類を骨格に再構築、`confidential-info-guidelines` の 3 段分類と直交する業務場面軸）
- **Full 形拡張 3 件** (Lite → Full):
  - `skills/confidential-info-guidelines/` 1.1.0 → 1.2.0 (SKILL.md 122→157 行、examples 3→4、§3.5 ファイル添付・§4.5 カスタム GPT/ナレッジ判断を追加)
  - `domain-skills/academic-affairs/syllabus-ai-policy/` 1.0.0 → 1.1.0 (SKILL.md 137→180 行、examples 1→3、§4.6 学生周知文・§4.7 学科合意形成プロセスを追加)
  - `domain-skills/research-support/research-integrity-ai-disclosure/` 1.0.0 → 1.1.0 (SKILL.md 149→209 行、examples 1→3、§4.5 検証プロトコルを追加、references に BMC/Cell Press/Oxford Academic/Cambridge Core/J-STAGE を追加)
- **Runtime adapter**: `runtime-adapters/claude-code.md` (273 行) — Claude Code ユーザー向け組み込み手順書 (DESIGN.md §4.2 の初弾)
- **`deprecated/` ディレクトリ** 新設、3 枠の README + 概要 README 計 4 ファイル

### Changed

- `README.md` / `README.en.md`: 横断スキル表に `ai-use-risk-classification` を追加、準備中表から 3 枠削除、「非推奨スキル」セクションと「Runtime Adapters」セクションを新設、`confidential-info-guidelines` の Version を 1.2.0 に更新
- 既存 3 スキルのバージョン番号更新（frontmatter version、last_updated 継続）

### Deprecated

- `skills/advanced-prompting-for-admin/` → `deprecated/advanced-prompting-for-admin/` — 代替: `staff-ai-literacy-primer`
- `skills/ai-report-evaluation/` → `deprecated/ai-report-evaluation/` — 代替: `research-integrity-ai-disclosure` + `syllabus-ai-policy`
- `skills/tool-selection-guide/` → `deprecated/tool-selection-guide/` — 代替: `institutional-ai-adoption-checklist`

### Removed

- 旧 `skills/advanced-prompting-for-admin/` / `skills/ai-report-evaluation/` / `skills/tool-selection-guide/` の空ディレクトリスタブを削除（中身は deprecated/ へ移動）

## [0.3.0] - 2026-04-19

### Added

- **10 new skills (Lite form)**, expanding catalog from 1 to 11:
  - `skills/staff-ai-literacy-primer/` — 新任職員向け AI リテラシー入門
  - `skills/institutional-ai-adoption-checklist/` — 組織導入検討チェックリスト
  - `skills/committee-meeting-minutes-ai/` — 委員会議事録 AI 化
  - `domain-skills/academic-affairs/syllabus-ai-policy/` — シラバス AI 方針
  - `domain-skills/academic-affairs/entrance-exam-ai-policy/` — 入試 AI 対応
  - `domain-skills/international-office/multilingual-student-communication/` — 留学生多言語化
  - `domain-skills/ir-analysis/ir-freeform-text-analysis/` — IR 自由記述分析
  - `domain-skills/public-relations/pr-ai-checklist/` — 広報 7 点チェック
  - `domain-skills/research-support/research-integrity-ai-disclosure/` — 研究 AI 開示
  - `domain-skills/student-support/student-inquiry-triage/` — 学生問い合わせトリアージ
- **全 6 領域 `domain-skills/` ディレクトリ**に最低 1 件ずつスキルを配置
- 4 references ファイル (`sample-syllabus-wording`, `journal-policy-overview`, `tool-overview-table`, `workflow-steps`)
- 10 example ファイル (`examples/example-01-*.md`、1 件/スキル)

### Changed

- `README.md` / `README.en.md`: 実装済みスキル表を 11 件に拡張、横断／領域別サブセクション構造を導入、読者別の最短ルートに新スキルへの入口を追加
- 準備中スキルの注記更新（v0.3 新スキルとの吸収関係を明示）

### Note

- v0.3 の 10 新スキルはすべて Lite 形（SKILL.md 80-150 行 + example 1 件）。Full 形への拡張（examples 増強・references 充実）は各スキルの成熟度に応じて v0.4 以降で対応する。
- ソース調査は日英中 3 言語圏 + X の計 113 候補から統合（research/ は .gitignore で除外済み、公開リポジトリには含まれない）。CC BY-SA 4.0 互換を確保するため、各 SKILL.md は「複数ソースに着想を得たオリジナル日本語」として書き下ろし、非互換ソースは構造のみ参照。

## [0.2.1] - 2026-04-19

### Changed

- **README.md / README.en.md 可読性の抜本的改善**:
  - 日英インライン併記（`What is this? / これは何か` 型）を全面廃止。各言語ファイルで完結させ、冒頭の1行リンクで切替する方式に変更。GitHub 主要ドキュメント集リポジトリ13件の慣例に合わせた。
  - 著者情報を冒頭から末尾へ移動。awesome系、anthropics、microsoft など主要リポジトリの定石に合わせる。
  - 一文の長さを60字以内に短縮。読点は1文あたり2個以内に抑制。
  - 全角括弧 `（）` と鉤括弧 `「」` を本文からゼロに削減（従来は約20箇所）。英名併記・連続する名詞列挙・抽象概念の強調を箇条書きや太字に置き換えた。
  - 暗黙知の例を段落内列挙から箇条書きに変更。

## [0.2.0] - 2026-04-19

### Changed

- **README.md / README.en.md 全面再設計**: 7セクションから4セクションへ再編成。冒頭に「Available Skills」表（実装済み / 準備中）を配置し、「どのスキルが今使えるか」を即座に判別可能に。読者別ルーティング表を追加（大学職員 / コンサルタント・研究者 / Global admins / GitHub非経験者）。ディレクトリツリー図を廃止。AIランタイムによる構造解析を容易にするため表形式を全面採用。
- **Open vs Premium フレーミング**: 「有料サービスが利用可能」（宣言型）から「すべてのコンテンツは CC BY-SA 4.0 で自由に使える」（許可型）へ変更。有料アドバイザリーは付随的に案内する構造に。
- `skills/confidential-info-guidelines/SKILL.md` → v1.1.0。セクション6「よくある判断例」を `examples/` ディレクトリへのリンク参照に書き換え。`last_updated: 2026-04-19`。
- `DESIGN.md` §3.4: 個人情報保護法の記述を2023年4月の法制一本化（令和3年改正個人情報保護法）に合わせて修正。
- `docs/how-to-use.md`: 冒頭に「GitHubアカウント不要で使う方法」セクションを追加。
- `skills/confidential-info-guidelines/references/ai-service-comparison.md`: 比較表の「-」セルを意味を明示した表現（「明示なし」「要確認」「特記事項なし」）に修正。「制限なし」と誤読されるリスクを解消。

### Added

- `skills/confidential-info-guidelines/examples/` ディレクトリ:
  - `example-01-meeting-minutes.md` — 学内委員会議事録の要約（Level 2）
  - `example-02-student-grades.md` — 学生の成績データ分析（Level 3、匿名化による回避策）
  - `example-03-website-translation.md` — 大学公式Webの英訳（Level 1、出力検証観点）
- `domain-skills/*/README.md` × 6: academic-affairs / international-office / ir-analysis / public-relations / research-support / student-support の各ディレクトリに最小READMEを配置（想定スキル・公開予定を明示）。

### Fixed

- DESIGN.md 原則4（「すべてのスキルには examples/ を格納する」）と実装の矛盾を解消。
- AIサービス比較表の「-」セルによる情報の曖昧さ。
- 個人情報保護法の記述が2023年法制一本化前の制度を前提としていた誤り。

## [0.1.0] - 2026-04-15

### Added

- Repository initial release
- `skills/confidential-info-guidelines/` — 機密情報取り扱い判断フレームワーク (v1.0.0)
- `DESIGN.md` — skill.md 設計の5原則と大学業務固有の注意点
- `docs/how-to-use.md` — スキルの使い方ガイド
- `docs/update-policy.md` — スキル鮮度管理方針
- `awesome/tools.md` — AIツールキュレーション（準備中）
- `case-studies/TEMPLATE.md` — 事例掲載テンプレート
- `CONTRIBUTING.md` — 外部貢献ガイドライン（初期方針）
