# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.7.0] - 2026-04-21

### Changed (設計思想の B-first 刷新)

- **skill 設計思想の B-first 刷新**: Reference content / Task content 二類型区分を廃止し、全 skill を「AI エージェントが読んで実行する unified protocol」として再定義。execution completeness スペクトラム (人間読み / Web AI / Claude Code 等) で runtime 差を捉える
- **`DESIGN.md` → `AGENTS.md` にリネーム**: skill エコシステムのデファクト (obra/superpowers / claude-code / cursor / gemini CLI が AGENTS.md を自動参照する動線) に整合。旧 `DESIGN.md` はリダイレクトスタブとして v0.8 まで残す
- **AGENTS.md 冒頭に「If You Are an AI Agent」節を追加**: superpowers 流の AI contributor 向けガイド。本 repo の利用モデル (AI エージェント主読、大学職員は AI 経由で間接利用) を宣言
- **AGENTS.md 原則 6 を B-first に書き換え**: Reference/Task 区分の廃止、execution completeness スペクトラムの導入、Claude Code 固有機能は `compatibility:` フィールドで明示する方針を明記

### Changed (Anthropic 公式 Agent Skills Spec 準拠)

- **全 15 skill の frontmatter を公式 spec に準拠**: `version` / `last_updated` / `author` を `metadata:` 下に畳む、description 1,024 字上限を遵守、`compatibility:` フィールドを Task tool / Write tool 依存 skill (ai-tone-check / create-action-skill) に採用、`disable-model-invocation` を `metadata:` 下に移動 (create-action-skill)
- `skills/ai-tone-check/` v1.0.1 → v1.1.0: description から環境制約節を削除、`compatibility:` に移動
- `skills/create-action-skill/` 初版 → v1.0.0: 正規 frontmatter に整備
- その他 13 skill: minor bump (機械的変換)
- **`references/skill-format-guide.md` を v0.7 対応に改訂**: Reference / Task 差分節を削除、unified protocol に統一、description 上限誤記 (「1,536 字」→「1,024 字」) を訂正、frontmatter の `metadata:` 下畳みを §2.1 で新規定義、読者 = AI エージェント前提を §0 冒頭で明示、execution completeness スペクトラム節 (§5) を新設

### Changed (利用者向けドキュメント)

- **`README.md` / `README.en.md`**: 「これは何か」節を「組織の AI エージェントにインストールする skill パッケージ」という位置付けに書き換え、DESIGN.md 参照を AGENTS.md に変更、全 skill の version 表示を v0.7 bump 後の値に更新
- **`runtime-adapters/claude-code.md`**: DESIGN.md 参照を AGENTS.md に変更 (4 箇所)
- **`skills/create-action-skill/SKILL.md`**: DESIGN.md 参照を AGENTS.md に変更 (7 箇所)

### Non-breaking

- skill 本文 (節構成 / トーン) の B-first 書き換えは半期改訂タイミングで順次実施、v0.7.0 では思想宣言と frontmatter 機械的修正のみ
- Task skill 3 件 (check-info-level / create-action-skill / ai-tone-check) の merger は v0.7.1+ に分離、v0.7.0 では場所と名前を維持
- 外部引用への影響: `DESIGN.md` リンクはリダイレクトスタブで維持 (v0.8 まで)、skill 名・パスに変更なし
- 利用者は新旧混在を意識する必要なし — frontmatter 刷新は AI エージェントが spec 準拠で読めるようになるだけの裏方変更

## [0.6.1] - 2026-04-20

### Changed

- **`skills/ai-tone-check/SKILL.md` (v1.0.0 → v1.0.1)**: empirical 検証で発見した nested subagent 環境での Task tool 不可制約を反映
  - description に「top-level Claude Code セッションから起動する」前提を明示
  - 手順に「0. 実行環境チェック」節を新規追加 — `Task` tool 利用不可時は親エージェントによるロールプレイ代行を採らず、明示失敗して top-level 再起動を促す
  - 落とし穴節に「Task tool が使えないから親がロールプレイで採点」を合理化カタログ 1 項目として追加
- `README.md` Task layer 表の ai-tone-check 行に top-level 起動前提を追記

## [0.6.0] - 2026-04-20

### Added

- **SKILL.md 文書フォーマット標準の策定**: `references/skill-format-guide.md` を新設。`github.com/mizchi/chezmoi-dotfiles/dot_claude/skills` を参照し、AI 主読 × 人間可読を両立する固定節構成（mission / いつ使うか / 中核節 / 落とし穴 / 関連）を定義
- **DESIGN.md §2 に原則 7「skill 文書フォーマット」を追加** — skill-format-guide への誘導と段階移行方針を明記
- **`skills/ai-tone-check/` 新規追加（Task layer）** — 大学業務文書（広報原稿 / 研修教材 / 学生向け案内）の「業務文書適切性 / AI 臭度 / 読者負荷」を subagent dispatch で 3 軸判定。`/ai-tone-check [draft] [staff|student|public]` で起動
- `skills/ai-tone-check/examples/` に広報原稿・研修教材の評価サンプル 2 件を追加

### Changed

- **`skills/check-info-level/SKILL.md` を新フォーマットに改修（v1.0 → v1.1.0）** — 「いつ使うか」「落とし穴」「関連」節を新設、description を trigger 記述に拡張、判定ロジックは維持
- **`skills/confidential-info-guidelines/SKILL.md` を新フォーマットに改修（v1.2.0 → v1.3.0）** — Overview を 3 段落から 1 段落 mission に圧縮、節番号を廃止、「落とし穴」節（8 項目の合理化カタログ）を新設、「関連」節を末尾に追加、3 段分類と判断フローの内容は維持
- README.md「これは何か」節に v0.6 フォーマット刷新方針を追記、Task layer 表に `ai-tone-check` を追加

## [0.5.0] - 2026-04-19

### Added

- **Task layer 導入**: Anthropic 公式 Claude Code Skills の Task content 仕様に準拠した Action skill 群を `skills/` 直下に追加
  - `check-info-level/` ─ confidential-info-guidelines を内部参照する Action 版
  - `create-action-skill/` ─ ユーザーの暗黙知を対話で SKILL.md 化するメタスキル
- DESIGN.md に「原則 6: Reference content と Task content の区別」を追加
- runtime-adapters/claude-code.md に §1.5「Reference layer と Task layer の使い分け」を追加
- README.md に Task layer スキル一覧表と「スラッシュコマンドで起動する」使い方パターンを追加

### Changed

- README.md「これは何か」「使い方」を Reference + Task 二層化に対応した記述に更新

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
