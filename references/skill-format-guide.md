# skill 文書フォーマット標準ガイド (v0.7〜)

**位置付け:** `AGENTS.md` 原則 6 の本体。本リポジトリで新規作成 / 改修する SKILL.md の形式を定義する単一出典。
**参照元:**
- [Anthropic Agent Skills Spec](https://agentskills.io/specification) (公式 spec、frontmatter と推奨ディレクトリ)
- `github.com/mizchi/chezmoi-dotfiles/dot_claude/skills` (18 skill のパターン調査、`research/2026-04-20-mizchi-inspired-skills.md` 参照)

**更新履歴:**
- v0.6 (2026-04-20): 初版策定、mizchi 集を参照した AI 主読 × 人間可読の両立形式
- v0.7 (2026-04-21): Reference/Task 二類型区分を廃止、Anthropic 公式 spec 準拠 (metadata: 下畳み、compatibility: 採用、description 1,024 字上限)

---

## 0. 本ガイドが解く問題と読者像

**読者 = AI エージェント**。本ガイドが対象とする SKILL.md は、組織の AI エージェント (Claude for Work / Claude Code / 将来の ChatGPT エージェント等) が読んで実行する protocol として書かれる。大学職員 / 研究者 / 管理部はその AI エージェント越しに利用する間接利用者で、GitHub で SKILL.md を直接読むことは想定しない (読めるが副次)。

この利用モデルの下で、skill を書く時に同時に成立させたい 3 点:

1. `description` が **発話 trigger 記述** として AI の自動起動精度を決める
2. **固定節構成と 1 段落 mission** で、AI が逐語解釈しやすく、人間が読んだ場合も 30 秒で全体像を掴める
3. **落とし穴テーブル** が AI の自己抑制プロトコルとして機能し、人間にとっても「やりがちな勘違いカタログ」として読める

本ガイドは mizchi skills 集の構造的強度を大学業務文書向けに翻訳したもの。大学公式トーンを維持し、AI 臭 (冗長敬語 / 空虚強調 / 両論併記) だけ削る。

**Reference content / Task content の区別は本 repo では採用しない** (v0.7 で廃止)。Anthropic 公式 docs の区別は pedagogical clarity のもので、本リポジトリの利用モデル (AI エージェント主読) では偽の二分法になる。全 skill は execution completeness スペクトラムの上にある (詳細は §5)。

---

## 1. 適用範囲

### 1.1 適用対象

- `skills/` 直下の全 skill (横断)
- `domain-skills/<area>/` 配下の領域別 skill
- `deprecated/` 配下の skill (deprecation 告知節は残す、本体は旧形式のまま)

### 1.2 非適用

- `awesome/` 配下のリンク集
- `case-studies/` 配下の事例レポート
- `research/` / `plan/` 配下の作業文書
- `runtime-adapters/` 配下のランタイム別ガイド

### 1.3 移行方針

既存 skill は **半期改訂 (3 月末 / 9 月末) のタイミングで順次移行**。新規作成と改修は本ガイド準拠。未移行の skill が混在している状態は過渡的正常状態。

v0.7 での frontmatter 形式刷新 (公式 spec 準拠) は全 skill 一斉で実施する (機械的変換)。本文の書き換え (節構成 / トーン) は半期改訂で順次。

---

## 2. frontmatter

### 2.1 全 skill 共通のベース形

```yaml
---
name: <kebab-case>
description: >
  <§2.3 に従った trigger 記述、1,024 字以内>
license: <license 名>
metadata:
  version: "<semver>"
  last_updated: "<YYYY-MM-DD>"
  author: <author>
---
```

**v0.7 以降、`version` / `last_updated` / `author` は `metadata:` 下に置く** (Anthropic 公式 Agent Skills Spec 準拠)。v0.6 以前の frontmatter 直下配置は機械的変換で一斉修正する。

### 2.2 Claude Code 向け / 副作用あり skill の追加フィールド

以下は公式 spec の任意フィールド。必要に応じ追加する:

```yaml
---
name: <kebab-case>
description: >
  <trigger 記述>
compatibility: <実行環境要件、500 字以内>
when_to_use: <追加 trigger、発話例 2-3 件>
argument-hint: <autocomplete ヒント>
allowed-tools: <Read Bash(file:*) Task 等、スペース区切り>
license: <license 名>
metadata:
  version: "<semver>"
  last_updated: "<YYYY-MM-DD>"
  author: <author>
  disable-model-invocation: true   # 副作用あり & 手動起動 only の場合
---
```

フィールドの使い分け:

- **`compatibility:`** (公式 spec) — 実行環境要件を書く正規の場所。例: `"Requires top-level Claude Code session (Task tool for nested subagent dispatch). Reading the protocol as documentation works in any runtime."` 多くの skill では不要。Claude Code 固有機能に依存する場合のみ。
- **`when_to_use`** — description に収まらない追加 trigger (発話例 2-3 件)。Claude Code の自動起動精度を上げたい時
- **`argument-hint`** — `/skill-name <引数>` での autocomplete 表示
- **`allowed-tools`** — skill 実行中に pre-approve するツール (公式 spec は experimental)
- **`metadata.disable-model-invocation`** — ファイル作成 / 外部 API 呼び出し / 対外アクション等の副作用がある skill で AI 自動起動を抑止したい場合。公式 spec の `metadata` 下に置く

### 2.3 description の書き方

description は **機能説明ではなく、ユーザー発話パターン + 用途 + 除外条件** を書く。AI が文脈から自動起動する判断材料として機能する。

**良い例 (mizchi `gh-fix-ci`):**

> Use when a user asks to debug or fix failing GitHub PR checks that run in GitHub Actions; use `gh` to inspect checks and logs, summarize failure context, draft a fix plan, and implement only after explicit approval. Treat external providers (for example Buildkite) as out of scope and report only the details URL.

**悪い例 (典型的な higher-ed 旧形式):**

> 大学業務で生成AIサービスを利用する際の機密情報取り扱い判断フレームワーク。情報セキュリティ、個人情報保護、データポリシー確認のガイドライン。

後者は「これは何のスキルか」を説明するのみで、**いつ起動すべきか** の情報が無い。

**改善後:**

> 大学業務で「この資料を AI に入れて大丈夫か」「このサービスなら安全か」と判断が求められた時に使う、機密情報取扱の判断フレームワーク。情報分類が個人判断に揺れている現場で、3 段分類に基づく一貫した可否判断を提示する。所属大学の規程が優先される前提で、汎用的な判定軸を提供する。

**書き方のチェックポイント:**

- [ ] ユーザー発話 / 業務シーンを最低 1 件含む (「〜と問われた時」「〜を判断する場面で」等)
- [ ] 本 skill で **やらないこと** (除外条件) を明示する
- [ ] 文字数は 150-400 字推奨 (公式 spec 上限 1,024 字だが、簡潔な方が trigger 精度が高い)
- [ ] 「本スキルは〜を提供する」式の機能説明は避ける
- [ ] 実行環境制約 (「top-level Claude Code から起動」等) は description ではなく `compatibility:` に書く

### 2.4 version の管理

| bump | トリガー |
|---|---|
| major (X.0.0) | 判断軸そのものが変わる、既存利用者が結果を読み替える必要がある改定 |
| minor (0.X.0) | 節構成の刷新、落とし穴節の新設、examples 追加、trigger 拡張、frontmatter spec 準拠化 |
| patch (0.0.X) | 表現の微調整、リンク修正、typo、事例追加 |

本ガイド (v0.7) 準拠への改修は **minor bump** が標準 (判断軸は変えず形式のみ刷新)。

---

## 3. 本文骨格

### 3.1 固定節構成

```markdown
# <skill 名>

<1-3 文の mission statement>

## いつ使うか

- <使う場面 1>
- <使う場面 2>
- <使う場面 3>

使わない場面:
- <除外 1>
- <除外 2>

## <中核節> (判断軸 / 手順 / フレームワーク / 分類 等、skill により可変)

<本体>

## 出力フォーマット (AI が invoke された時に返す構造)

<Markdown テンプレート or 期待される出力構造>

## 落とし穴

<合理化カタログ表>

## 関連

- `<related-skill>` — <1 行説明>
```

**冒頭 mission / いつ使うか (+ 使わない場面) / 中核節 / 出力フォーマット / 落とし穴 / 関連** の 6 節は全 skill で共通骨格。中核節の名前と構成は skill の性質で変わる。

### 3.2 節番号は使わない

`## 1. Overview` `## 2. Prerequisites` のような番号付きは廃止。代わりに意味のある節タイトル。理由:

- 節の追加削除で番号がズレると既存引用 (`§3.5` 等) が破綻する
- 番号があると「全節読まないと分からない」印象を与える。実際は個別節で自己完結している方が AI / 人間双方に読みやすい
- 細番号参照 (§3.5) は、アンカー付きヘッダ (`#file-metadata-risk` 等) で代替できる

例外: `CHANGELOG.md` / `AGENTS.md` のような構造的文書は番号維持可。

### 3.3 冒頭 mission statement

skill タイトル直後、1 段落 (1-3 文) で次を書く:

- この skill が存在する理由 (なぜ必要か)
- 核となる主張 / 判断軸 / 動作

**良い例 (retrospective-codify):**

> タスクの終盤で「最初にこれを知っていれば遠回りしなかった」知見を抽出し、静的ルール・skill・常時有効ルールのいずれかに固定する。プロンプトに頼らず再現可能な形に落とすことを優先する。

**悪い例 (冗長、典型 AI 臭):**

> 大学業務において生成AIの活用が広がる中、「この情報をAIに入力して問題ないか」という判断は日常的に発生する。しかし、その判断基準が個人の感覚に委ねられている現状では、情報漏洩リスクと業務効率化の間で一貫性のある意思決定ができない。本スキルは、大学業務で扱う情報を3段階に分類し、生成AIサービスへの入力可否を構造的に判断するフレームワークを提供する。(3 段落中の 1 段落目)

後者は **背景 → 問題 → 解決** の論証構造を取っているが、skill 冒頭としては冗長。論証は References / 限界 節に委ね、冒頭は断定で書く。

---

## 4. 各節の書き方

### 4.1 `## いつ使うか`

- 箇条書き 3-5 項目で「使う場面」を列挙
- 直後に「使わない場面:」を同じ箇条書き形で 2-4 項目

**意図:** description の trigger を本文で具体例として示す。AI は本節を参照して「今がこの skill の適用場面か」を判定できる。人間は「これを読むべきタイミング」を把握できる。

**例 (tech-article-reproducibility):**

```markdown
## いつ使うか

- 技術記事ドラフトの公開前最終チェック
- ハンズオン記事 / チュートリアル記事
- ツール導入記事 / セットアップ記事
- 「動いた」と書いた記事の検証

使わない場面:
- 概念解説記事 (再現するものがない)
- ポエム / オピニオン記事
- 記事内で完結する小ネタ
```

### 4.2 中核節

skill の性質に応じて中核節の名前と構成を決める。型は以下の 3 パターンが頻出:

**(a) 判断フレームワーク型** — 「このケースはどう判定するか」に答える skill

```markdown
## 判断軸 (または 3 段分類 / 4 区分 / 分類体系)

<表 / mermaid flowchart>

## 判断フロー

<mermaid>

## 前提確認 (optional、所属規程との照合)
```

**(b) 執行手順型** — AI が tool を呼んで成果物を生成する skill

```markdown
## 手順

### 1. <ステップ名>
<動作>

### 2. <ステップ名>
<動作>

## 品質基準

- <これを満たさないと失格>

## Available Tools

- **<tool>**: <用途>
```

**(c) 評価 / レビュー型** — subagent dispatch で評価を返す skill

```markdown
## 評価軸 (N 軸)

<各軸の定義 + 採点基準>

## subagent dispatch テンプレート

<コードブロックで、そのまま Task tool の prompt 引数に渡せる形>

## レポート構造
```

skill によっては 2 型を組合せる (例: `check-info-level` は判断フレームワーク型 + 執行手順型)。どの型でも **「AI が invoke されたら何をするか」が手順として書けている** ことが B-first 設計の要件。

表 / Mermaid flowchart / Graphviz dot で可視化できるものはそうする。散文だけで判断ロジックを書かない。

### 4.3 `## 出力フォーマット`

AI が invoke された時に返す構造を、Markdown テンプレートで明示する:

```markdown
## 出力フォーマット

```markdown
## 判定結果: Level [1/2/3]

**判定理由:**
[2-3 文、本文の具体記述を引用ベースで]

**AI 入力可否:**
[判定結果文]

**推奨次アクション:**
- [ ] [具体行動 1]
```
```

判断フレームワーク型 skill でも「何を返すか」を明示する。これが B-first の核 — AI が skill を invoke した時に一貫した構造で応答するために、出力仕様を skill 側で決めておく。

### 4.4 `## 落とし穴`

本ガイドで最も重要な節。合理化カタログを 2 列表で書く:

```markdown
## 落とし穴

| 出てくる合理化 | 実態 |
|---|---|
| 「Enterprise 契約なら何でも入力していい」 | Level 3 の個人情報は Enterprise でも避ける。契約はデータ学習を止めるが、漏洩リスクはゼロにならない |
| 「黒塗り PDF は安全」 | PDF の黒塗りは画像化してないとテキスト層に原文が残る。アップロード時は AI が透過して読む |
| 「匿名化すれば全て OK」 | 学籍番号 / 発言特徴 / 研究テーマの組合せで個人が再特定されうる。k-匿名化程度では不十分 |
```

**書き方ルール:**

- 左列は「〜と思った瞬間」「〜ならいいだろう」等、合理化の内声そのもの
- 右列は「なぜそれが誤りか + 何をすべきか」
- 項目数は 4-8 件、10 を超えたら分類する
- skill 固有の現場知識を書く (generic な AI 警告表現でなく)

**意図:** AI のループ中に本テーブルの左列に該当する思考が出たら止まる。v0.6 の empirical 検証で、subagent が自己申告レベルで本節を自己抑制プロトコルとして機能させた事例が確認されている (詳細は `CHANGELOG.md` v0.6.0 検証節)。

### 4.5 `## 関連`

末尾に配置、依存 / 補完 skill を 1 行説明付きで列挙:

```markdown
## 関連

- `confidential-info-guidelines` — 本 skill が判定に使う 3 段分類の定義元
- `ai-use-risk-classification` — 4 分類版の上位互換、ガバナンス文書起草時に使う
- `check-info-level` — 本 skill を Action 化したもの、ファイル / テキストを渡すと判定結果を返す
```

**書き方ルール:**

- 本文中に散発的にリンクするのではなく、**末尾に集約**
- 「依存」「補完」「上位互換」「Action 版」等、関係性の種類を 1 行で示す
- 他リポジトリの skill (`superpowers:writing-skills` 等) も含めてよい
- 最低 1 件、上限 8 件を目安

---

## 5. execution completeness スペクトラム

**Reference / Task 二類型は v0.7 で廃止**。全 skill は同じフォーマットで書き、実行主体 (runtime) の能力差で execution completeness が決まる。

| runtime | 実行可能度 | できること |
|---|---|---|
| 人間 (ブラウザ直読) | 低 | protocol を読んで自分で手動実行。判断フレームワーク部分は参考になるが、subagent dispatch や tool 呼び出しは人が代行 |
| Web 版 AI (ChatGPT / Claude / Gemini) | 中 | protocol を読んで判断部分を実行、自然言語で構造化出力を返す。tool 呼び出し / subagent dispatch は不可 |
| Claude Code / Claude for Work / エージェント runtime | 高 | protocol 全部実行、tool 呼び出し / subagent dispatch 可、スラッシュコマンド起動可 |

skill file は同一、実行主体が違うだけ。Claude Code 向け `/check-info-level` のようなスラッシュコマンド起動は「高 execution completeness runtime 上での具体化」であって別種の skill ではない。

### 5.1 runtime 固有機能を要する skill の扱い

Claude Code の Task tool / Write tool 等、特定 runtime でしか動かない機能を使う skill は:

1. frontmatter の `compatibility:` に実行環境要件を書く (例: `"Requires top-level Claude Code session (Task tool for nested subagent dispatch)"`)
2. 手順節に「実行環境チェック」ステップを冒頭に入れる (利用不可時の明示失敗)
3. 落とし穴節に「代替動作 (親エージェントの代行等) を採らない」を明記する

これにより、低 execution completeness runtime で呼ばれた場合も skill は壊れず、適切な fallback (「top-level で再起動してください」メッセージ) を返す。

### 5.2 典型行数

- 判断フレームワーク型 skill: 150-400 行 (判断軸の複雑さによる)
- 執行手順型 skill: 150-300 行
- 評価 / レビュー型 skill: 200-400 行 (subagent dispatch template 内蔵)

500 行を超える skill は内容を分割するか、`references/<topic>.md` に詳細を逃がす (Anthropic 公式 spec 推奨)。

---

## 6. トーン

### 6.1 削る表現 (AI 臭)

| パターン | 例 | 直し方 |
|---|---|---|
| 冗長な丁寧表現 | 「〜することができます」「〜することが重要です」 | 「〜できる」「〜が大事」 |
| 空虚な強調語 | 「素晴らしい」「画期的な」「革新的な」「重要な」 | 削除、または具体性で置換 |
| 両論併記の無意味な中立 | 「〜という見方もあれば〜という見方もある」 | どちらの立場を取るか明示 |
| 章冒頭の前章要約 | 「前章では X について述べた。本章では...」 | 削除 |
| 一般論の締め | 「重要なのはバランスです」「適切に使い分けましょう」 | 具体的判断軸で置換 |
| 対称的な見出し階層 | すべての節に「概要 / 意義 / 方法 / まとめ」 | 各節の長さを内容に合わせて非対称に |
| 主観の過剰回避 | 「一般的に〜とされている」「〜と言われている」 | 「〜する」断定、必要なら出典添付 |
| 過剰な箇条書き | 文章で書けることを全部 bullet | 主張は文で、列挙が必要な箇所だけ bullet |
| 結論部の繰り返し | 「以上、本節では〜を解説した」 | 削除、または次の節への橋渡し |
| 抽象的な仮想例 | 「例えば、ある大学では〜という事例があります」 | 実在の大学名 / 実 URL / 公表事例で置換、無ければ例自体を削除 |

### 6.2 入れる表現

- **断定**: 「〜する」「〜を避ける」「〜に置換する」 (大学業務文脈で問題ない範囲で、「〜と考えられる」「〜すべきである」は残してよい)
- **具体性**: 抽象論の合間に必ずコマンド / 数値 / 引用 / 具体事例
- **率直な限界開示**: 「本 skill は〜までをカバーし、〜は範囲外」「所属大学規程が優先」
- **主語省略**: 日本語として自然な範囲で主語を省く。「本スキルは〜を提供する」→「〜を提供する」

### 6.3 入れない表現

- **口語**: 「めっちゃ」「シュッと」「消耗した」「〜っぽい」。mizchi 文体の核だが、大学公式利用を想定する本リポジトリでは採用しない
- **絵文字 / 顔文字**: 文中にも、コードブロック外にも入れない
- **個人名義の主観**: 「自分は〜と思う」「筆者の経験では」。本リポジトリは著者個人ではなく集合知として提示する。事例が個人経験由来の場合は「本リポジトリの試行では〜」と集団主語に

### 6.4 水準の目安

mizchi 水準を 100% とすると、本リポジトリは **70-80% に寄せる**。AI 臭削減は徹底するが、口語 / 個人主観は入れない、という差分。

---

## 7. 具体例

### 7.1 良い例 (新形式、判断フレームワーク型)

```markdown
---
name: confidential-info-guidelines
description: >
  大学業務で「この資料を AI に入れて大丈夫か」「どのサービスなら安全か」と
  判断が求められた時に使う、機密情報取扱の判断フレームワーク。情報分類が
  個人判断に揺れている現場で、3 段分類に基づく一貫した可否判断を提示する。
  所属大学規程が優先される前提で、汎用的な判定軸を提供する。
license: CC BY-SA 4.0
metadata:
  version: "1.4.0"
  last_updated: "2026-04-21"
  author: gmoriki
---

# confidential-info-guidelines

大学業務で扱う情報を 3 段分類し、生成 AI サービスへの入力可否を構造的に判断するフレームワーク。所属大学規程が優先される前提で、判定が個人感覚に依存しない共通の物差しを提供する。

## いつ使うか

- 職員 / 研究者が「これ AI に入れていい？」と判断を迷った時
- 大学として AI 利用ガイドラインを策定 / 改定する時
- 情報漏洩インシデント後、判定基準を見直す時

使わない場面:
- 所属大学の独自ガイドラインで判定フローが確立している場合 (大学規程優先)
- 個別サービスの契約内容確認

## 3 段分類
<表 / mermaid>

## 判断フロー
<mermaid>

## 出力フォーマット
<判定 + 理由 + 推奨アクションの Markdown 構造>

## 落とし穴
| 出てくる合理化 | 実態 |
|---|---|
| 「Enterprise 契約なら何でも入力していい」 | ... |

## 限界

所属大学規程が本 skill と異なる場合、大学規程が優先。

## 関連

- `check-info-level` — 本 skill を Action 化したもの
- `ai-use-risk-classification` — 4 分類版、ガバナンス起草用
```

### 7.2 良い例 (新形式、執行手順型 + Claude Code 依存)

```markdown
---
name: ai-tone-check
description: >
  大学業務文書 (広報原稿 / 研修教材 / 申請書 / 学生向け案内等) のドラフトを
  読み取り、subagent dispatch で 3 軸評価を返す。...
compatibility: >
  Requires top-level Claude Code session (Task tool for nested subagent dispatch).
  Reading the protocol as documentation works in any runtime.
when_to_use: >
  広報原稿 / 研修配布資料 / 職員向けメール / 学生向け FAQ 等のドラフトを
  書いた後、公開前の最終チェックで使う。
argument-hint: "[draft path or text] [role: staff|student|public]"
allowed-tools: Read Task
license: CC BY-SA 4.0
metadata:
  version: "1.1.0"
  last_updated: "2026-04-21"
  author: gmoriki
---

# ai-tone-check
(本文)
```

### 7.3 NG 例 (過剰パロディ化)

mizchi 水準に寄せすぎた失敗例:

```markdown
# confidential-info-guidelines

大学職員がめっちゃ雑に AI に学生情報入れちゃうのを止める skill。
自分の経験的には、シュッと 3 段分類で判定するのが一番回る。

## いつ使うか
...
```

**何が NG か:**

- 「めっちゃ」「シュッと」の口語 — 大学公式利用で不適
- 「自分の経験的には」— 集合知として提示する方針に反する
- mission statement が率直すぎて公式文書として使いにくい

**直す方向:**

- 口語を標準的書き言葉に
- 主語を「本 skill」または省略形に
- 率直さは「落とし穴」節に逃がす

---

## 8. 既存 skill の移行チェックリスト

既存 skill を新形式に改修する時の手順:

### 8.1 frontmatter 刷新 (v0.7 で一斉実施)

- [ ] `version` / `last_updated` / `author` を `metadata:` 下に移動
- [ ] description を 1,024 字以内に trim (必要時のみ)
- [ ] `compatibility:` を必要に応じ追加 (Claude Code 固有機能依存 skill のみ)
- [ ] `disable-model-invocation` を `metadata:` 下に移動 (該当 skill のみ)
- [ ] minor version bump (例: 1.3.0 → 1.4.0)、`last_updated` 更新

### 8.2 本文刷新 (半期改訂で順次)

- [ ] description を機能説明 → trigger 記述に書き換える (§2.3 参照)
- [ ] 冒頭の `## 1. Overview` (3 段落等) を 1-3 文の mission statement に圧縮
- [ ] `## いつ使うか` + 使わない場面 節を新設 (mission の直後)
- [ ] 既存の `## 2. Prerequisites` を `## 前提確認` に改名、簡素化
- [ ] 中核節の番号を外す (`## 3. 情報分類の3段階` → `## 3 段分類` 等)
- [ ] `## 出力フォーマット` 節を新設 (判断フレームワーク型 skill にも追加)
- [ ] `## 落とし穴` 節を新設 (限界 節の後、関連 節の前)
- [ ] `## 関連` 節を末尾に新設、本文中の依存 skill 参照をここへ集約
- [ ] 本文から AI 臭表現を削除 (§6.1 のチェックリストで確認)
- [ ] `CHANGELOG.md` に改修エントリ追加

推定所要時間:
- frontmatter 刷新 (機械的): 1 skill あたり 5-10 分
- 本文刷新: 1 skill あたり 1-2 時間

---

## 9. 本ガイドの落とし穴

| 出てくる合理化 | 実態 |
|---|---|
| 「既存 skill 全部を一括で本文改修しよう」 | 一括は検証不足を生む。半期改訂タイミングで順次移行が本方針。frontmatter のみ一斉 (機械的) は可 |
| 「description は既存のままでいいだろう、本文だけ直そう」 | description の trigger 化が最も効果大。本文改修より先に description を直す |
| 「落とし穴節は思い付かないから省こう」 | 思い付かない段階で skill として未成熟の signal。3 項目程度は捻り出す。ゼロは省略不可 |
| 「mizchi 水準に寄せれば寄せるほど良い」 | 口語 / 個人主観を入れると大学公式利用できなくなる。70-80% に抑える |
| 「節番号を全部外せばいい」 | `CHANGELOG.md` / `AGENTS.md` の節番号は維持。SKILL.md だけが対象 |
| 「関連節に同じリポジトリの skill だけ書く」 | 他リポジトリ (`superpowers:*` 等) も書いてよい。読み手が次に読むべきものを列挙 |
| 「examples/ があるから inline 例は不要」 | examples/ は few-shot 用、本文の具体性は別途必要。§7 のような inline ミニ例を入れる |
| 「version は frontmatter 直下のままでも動くし」 | 公式 spec 非準拠。将来 Anthropic ツール / agentskills.io 認定 CI が `metadata:` 下参照を前提にする可能性あり。v0.7 で一斉準拠化する |
| 「Reference / Task の区別を維持したい (Anthropic 公式と合わせたい)」 | 公式区別は pedagogical clarity のためのもの。本 repo の利用モデル (AI エージェント主読) では偽の二分法。v0.7 で廃止済み、迷ったら unified protocol として書く |

---

## 10. 本ガイド自身の更新

本ガイド (v0.7) は運用で不足が見つかったら改訂する。想定される改訂項目:

- Anthropic 公式 Agent Skills Spec の更新 (2026-04 時点、今後 `user-invocable` / `paths` / `context: fork` 等の機能拡張が入る可能性)
- 実際の移行パイロット後のフィードバック (v0.7 の全 skill 一斉 frontmatter 刷新の実体験)
- 他ランタイム (ChatGPT / Microsoft Copilot) 向け変換時の差分
- agentskills.io 認定ワークフロー対応 (v0.8+ 候補)

改訂時は本ガイドの version (文中に明記せず、git commit と CHANGELOG で管理) を更新し、移行チェックリスト (§8) に差分を追記する。

---

## 11. 関連

- `AGENTS.md` §2 原則 6 — 本ガイドの参照元 (B-first / unified protocol の思想宣言)
- [Anthropic Agent Skills Spec](https://agentskills.io/specification) — 公式 frontmatter / ディレクトリ構造の正規定義
- `research/2026-04-20-mizchi-inspired-skills.md` — 本ガイド策定の調査記録
- `runtime-adapters/claude-code.md` — Claude Code 上での skill 配置 / 起動仕様
- `github.com/mizchi/chezmoi-dotfiles/dot_claude/skills` — 参照元 skill 集 (外部、CC / MIT 互換確認のうえ構造借用)
- `superpowers:writing-skills` — 新規 skill 作成時の TDD アプローチ (他リポジトリ)
- `skills/check-info-level/` — 新形式の執行手順型 skill 実装例
- `skills/confidential-info-guidelines/` — 新形式の判断フレームワーク型 skill 実装例 (v1.4.0)
- `skills/ai-tone-check/` — 新形式の評価 / レビュー型 skill 実装例 (compatibility: 採用例)
