# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

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
