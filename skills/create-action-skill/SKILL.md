---
name: create-action-skill
description: 職員 / 研究者の暗黙知を対話的にヒアリングし、higher-ed-ai-skills 規格に準拠した SKILL.md（Reference type または Task type）を生成する。「自分のノウハウをスキル化したい」「業務手順を構造化したい」と言われた時に手動で起動する。
disable-model-invocation: true
allowed-tools: Read Write Bash(mkdir:*) Bash(ls:*)
---

# create-action-skill

higher-ed-ai-skills 規格に準拠した新規 SKILL.md を、対話ヒアリング経由で生成するメタ Task skill。

## What This Does

ユーザー（大学職員 / 研究者 / URA / 教員）が自分の暗黙知・業務知見を、higher-ed-ai-skills のいずれかの SKILL.md として構造化したい場面で使う。対話的に必要情報を聞き取り、Anthropic 公式 Skills 仕様に準拠した SKILL.md ファイル一式（本体 + examples/ 1 件）を生成する。

t46/ra-skills の `create-ra-skill` 設計を参照しつつ、higher-ed-ai-skills 固有の以下を統合:
- Reference type / Task type の使い分け判断を最初に問う
- DESIGN.md §2 の 5 原則（Progressive Disclosure / description トリガー設計 / 本体は判断ロジック / 模範回答 / 陳腐化前提）に沿った構造化
- ライセンス（CC BY-SA 4.0）と引用方針（政府一次ソース / 構造借用のみ）の確認

## Required Inputs

`$ARGUMENTS` は不要。対話で以下を順次収集:

1. type 選択（Reference / Task）
2. 業務概要（1-2 文）
3. 想定起動シーン（ユーザーの自然な発話）
4. 入力情報（Task の場合）/ 適用文脈（Reference の場合）
5. 出力 / 期待挙動
6. 手順 / 判断基準
7. よくある落とし穴
8. 参照する一次ソース（政府 / 大学事例 / 既存 P4Us / Ontario Pressbooks）
9. ライセンス互換性確認

## What It Produces

- `skills/{skill-name}/SKILL.md` または `domain-skills/{area}/{skill-name}/SKILL.md` 一式
- `skills/{skill-name}/examples/example-01-*.md`（最低 1 件）
- 配置先パス、frontmatter、本体構造、依存スキルの一覧サマリ

## 手順

### Phase 0: 起動チェック

`/create-action-skill` 実行時、まず以下を確認:

- 現在の作業ディレクトリが `higher-ed-ai-skills` リポジトリ直下か（`README.md` と `DESIGN.md` の存在で判定）
- 違う場合: 「higher-ed-ai-skills リポジトリのルートで実行してください」と返して終了

### Phase 1: type 選択ヒアリング

最初に以下を提示:

```
作成するスキルの type を選んでください:

1. Reference type — 判断フレームワーク / ガイドライン文書。AI が読んで人間
   に判断材料を返す。例: confidential-info-guidelines, syllabus-ai-policy。
   既存 12 個の SKILL.md はすべてこの type。

2. Task type — AI が手順を実行して成果物を返す Action skill。
   例: /check-info-level（テキスト渡すと Level 判定）。
   v0.5 で導入された新類型。
```

ユーザーが選択した type に応じて、Phase 2 以降のテンプレートを切り替える。

### Phase 2: ヒアリング（共通）

#### Q1. 業務 / ノウハウの概要

「どんな業務 / 判断についてのスキルですか？」（1-2 文）

#### Q2. 想定起動シーン（description トリガー設計用）

「ユーザーがどんな言葉で問いかけた時にこのスキルが起動すべきですか？」
具体的な発話例を 3 つ挙げてもらう（DESIGN.md §2 原則 2 に沿う）。

### Phase 3a: Reference type 専用ヒアリング

(Phase 1 で 1 を選んだ場合のみ)

#### Q3. 適用文脈
どの業務領域 / 担当部門で参照されるか（例: 教務、研究支援、広報）。

#### Q4. 判断軸
判断のための区分 / 階層 / フローチャート（例: 3 段階分類、4 区分判定）。

#### Q5. 限界 / 例外
規程や法令に従って判断が変わる箇所、所属大学による差異。

### Phase 3b: Task type 専用ヒアリング

(Phase 1 で 2 を選んだ場合のみ)

#### Q3'. 入力情報
スキル起動時に渡される引数 / ファイル / テキストの種類。

#### Q4'. 出力 / 成果物
判定結果、レポート、ファイル、リスト等、何を返すか。

#### Q5'. 実行手順
ステップバイステップの動作。AI が踏む順序。

#### Q6'. 使用ツール
Read / Write / Bash / WebSearch 等、必要なツールを列挙。

#### Q7'. 自動起動の可否
副作用（ファイル作成、メール送信、外部 API 呼び出し）の有無。
ある場合は `disable-model-invocation: true` を frontmatter に追加。

### Phase 4: 共通追加ヒアリング

#### Q8. よくあるミス / 落とし穴
利用者がやりがちな誤りとその対策。

#### Q9. 参照する一次ソース
- 政府一次ソース（文科省 / 教育部 / TEQSA / NIH 等）
- 大学事例（特定大学のガイドライン公開ページ）
- 森木 P4Us（MIT License）
- Ontario Pressbooks（CC BY-SA 4.0）

**ライセンス警告**: EDUCAUSE / Stanford / 復旦大 / 出版社公式ポリシーから直接引用しない（CC BY-SA 4.0 互換性なし）。構造のみ参照可。

#### Q10. 配置先

- 横断スキル → `skills/{skill-name}/`
- 業務領域別 → `domain-skills/{area}/{skill-name}/`（area: academic-affairs / international-office / ir-analysis / public-relations / research-support / student-support）

### Phase 5: SKILL.md 生成

ヒアリング結果を以下のテンプレートに流し込む:

#### Reference type テンプレート

```markdown
---
name: {kebab-case}
description: {Q2 から生成、トリガー設計}
version: 1.0.0
last_updated: "{今日の日付 ISO 8601}"
author: {ユーザー指定}
license: CC BY-SA 4.0
---

# {skill-name}

{1 行説明}

## 1. Overview
{Q1 + Q3}

## 2. Prerequisites
{確認すべき所属大学規程・関連法令}

## 3. {判断軸の名前}
{Q4 を表 / フローチャートで構造化}

## 4. 判断フロー
{Mermaid flowchart}

## 5. 使用場面
{ミニ判断例 2-3 件}

## 6. Limitations
{Q5 を整理}

## 依存スキル / 関連スキル
{他の skill を参照する場合は `[label](../skill-name/SKILL.md)` の Markdown link 形式で記述。例: 機密情報判定が必要なら [`skills/confidential-info-guidelines/`](../confidential-info-guidelines/SKILL.md) を参照、等。無ければセクション削除}

## References
{Q9 を分類して列挙、ライセンス警告適用済み}
```

#### Task type テンプレート

```markdown
---
name: {kebab-case}
description: {Q2 から生成。自然発話を 2-3 個埋め込み「…と問われた時に起動する」で締める。例: skills/check-info-level/SKILL.md の description を参照}
when_to_use: {Q2 の発話例 3 つ}
argument-hint: {Q3' から推定}
{オプション行: Q7' で副作用ありの場合のみ次行を追加}
disable-model-invocation: true
allowed-tools: {Q6' から生成。Bash 引数はコロン構文 (例: Bash(git status:*))。複数 entry はスペース区切り}
---

# {skill-name}

{1 行説明}

## What This Does
{Q1 + Q3'}

## Required Inputs
{Q3' を構造化}

## What It Produces
{Q4' を箇条書き}

## 手順
{Q5' をステップバイステップ、各ステップ番号付き}

## 品質基準
{Q8 から「これを満たさないとダメ」を逆算して列挙}

## Available Tools
{Q6'。frontmatter と同じ Bash(...:*) 表記で揃える}

## 依存スキル
{もし他 skill を参照するなら明示。`[label](../skill-name/SKILL.md)` の Markdown link 形式で}
```

### Phase 6: examples 生成

`examples/example-01-{シーン名}.md` を 1 件生成。テンプレート:

```markdown
# 例 1: {シーン名}

## 入力 / 状況
{ユーザーが想定する典型シナリオ}

## 期待される処理 (Task type) / 判定 (Reference type)
{該当 skill を適用した時の挙動}

## 期待される出力
{具体的な応答例}

## なぜこの応答が適切か
{2-3 文の解説}
```

### Phase 7: ファイル保存と検証

1. `mkdir -p {配置先}`
2. `Write` で SKILL.md 保存
3. `Write` で examples/example-01-*.md 保存
4. frontmatter parse 検証コマンドを提示 (yaml モジュールが入っていれば yaml.safe_load、なければ正規表現で `name:` と `description:` の存在を確認)
5. 配置先パスとファイル一覧をユーザーに提示

### Phase 8: 次のステップ案内

```
スキルを生成しました:
- {配置先}/SKILL.md
- {配置先}/examples/example-01-{シーン名}.md

次のステップ:
1. SKILL.md を読み返し、文意・トーンを微修正
2. README.md のスキル一覧表に追加
3. CHANGELOG.md に [Added] エントリ追加
4. 検証: Claude Code を再起動し、想定発話で起動するか確認
   → /{skill-name} で直接起動も試す
5. 半期改訂時 (3月末 / 9月末) に内容を見直し、last_updated を更新

GitHub への PR を出すなら:
1. fork → branch (add-skill/{skill-name})
2. CONTRIBUTING.md 参照して PR 作成
```

## 品質基準

- ヒアリングは一方的でなく、ユーザー回答に応じて深掘りすること
- ユーザーが言っていない情報を AI が補完しない（憶測で書かない）
- 一次ソース引用時に CC BY-SA 4.0 互換性を必ず確認すること
- 生成された SKILL.md が DESIGN.md §2 の 5 原則に沿っていること
- examples/ を必ず最低 1 件生成すること（DESIGN.md §2 原則 4 ─ 模範回答必須）
- 生成後に「ユーザー自身でレビューしてください」と必ず添えること

## Available Tools

- **Read**: 既存スキル / DESIGN.md / README.md の参照
- **Write**: 新規ファイル作成
- **Bash(mkdir:*)**: ディレクトリ作成
- **Bash(ls:*)**: 既存ファイル確認

## 依存スキル / 参照

- [`DESIGN.md`](../../DESIGN.md) §2（5 原則）
- [`CONTRIBUTING.md`](../../CONTRIBUTING.md)（PR ルール）
- 既存 12 SKILL.md（[`skills/`](../../skills/) と [`domain-skills/`](../../domain-skills/) 配下、テンプレート参考）
- [`runtime-adapters/claude-code.md`](../../runtime-adapters/claude-code.md)（公式 frontmatter 仕様）
