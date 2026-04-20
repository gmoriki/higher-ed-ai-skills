# skill 文書フォーマット標準ガイド (v0.6〜)

**位置付け:** `DESIGN.md` 原則 7 の本体。本リポジトリで新規作成 / 改修する SKILL.md の形式を定義する単一出典。
**参照元:** `github.com/mizchi/chezmoi-dotfiles/dot_claude/skills` (18 skill のパターン調査、`research/2026-04-20-mizchi-inspired-skills.md` 参照)
**策定日:** 2026-04-20

---

## 0. 本ガイドが解く問題

AI エージェント主読 (to-AI メイン) の skill を書くと、人間には冗長で読みにくくなりがち。逆に人間向けガイドラインとして書くと、AI にとっては trigger が曖昧で起動精度が落ち、本文も「実行可能手順」ではなく「説明文」になる。

両立の経路は存在する。mizchi skills 集 (18 件) は次の 3 点で両者を重ねている:

1. `description` が **発話 trigger 記述** — AI 自動起動の精度を決めつつ、人間にはシーン記述として読める
2. **1 段落 mission + 固定節構成** — AI は逐語解釈しやすく、人間は 30 秒で全体像を掴める
3. **落とし穴テーブル** — AI の自己抑制プロトコルとして機能しつつ、人間には「やりがちな勘違いカタログ」

本ガイドはこの 3 点を大学業務文書向けに翻訳して標準化する。大学公式トーンは維持し、AI 臭 (冗長敬語 / 空虚強調 / 両論併記) だけ削る。

---

## 1. 適用範囲

### 1.1 適用対象

- `skills/` 直下の Reference / Task skill (横断)
- `domain-skills/<area>/` 配下の領域別 skill
- `deprecated/` 配下の skill (deprecation 告知節は残す、本体は旧形式のまま)

### 1.2 非適用

- `awesome/` 配下のリンク集
- `case-studies/` 配下の事例レポート
- `research/` / `plan/` 配下の作業文書
- `runtime-adapters/` 配下のランタイム別ガイド

### 1.3 移行方針

既存 skill は **半期改訂 (3 月末 / 9 月末) または Full 形化タイミングで順次移行**。新規作成と改修は本ガイド準拠。未移行の skill が混在している状態は過渡的正常状態。

---

## 2. frontmatter

### 2.1 Reference skill の frontmatter

```yaml
---
name: <kebab-case>
description: >
  <2.3 に従った trigger 記述、150-400 字推奨>
version: <semver>
last_updated: "<YYYY-MM-DD>"
author: <author>
license: CC BY-SA 4.0
---
```

### 2.2 Task skill の frontmatter

```yaml
---
name: <kebab-case>
description: >
  <2.3 に従った trigger 記述>
when_to_use: <追加 trigger、発話例 2-3 件>
argument-hint: <autocomplete ヒント>
allowed-tools: <Read Bash(file:*) Task 等>
disable-model-invocation: true   # 副作用ある場合のみ
version: <semver>
last_updated: "<YYYY-MM-DD>"
author: <author>
license: CC BY-SA 4.0
---
```

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
- [ ] 文字数は 150-400 字 (公式上限 1,536 字だが、簡潔な方が trigger 精度が高い)
- [ ] 「本スキルは〜を提供する」式の機能説明は避ける

### 2.4 version の管理

| bump | トリガー |
|---|---|
| major (X.0.0) | 判断軸そのものが変わる、既存利用者が結果を読み替える必要がある改定 |
| minor (0.X.0) | 節構成の刷新、落とし穴節の新設、examples 追加、trigger 拡張 |
| patch (0.0.X) | 表現の微調整、リンク修正、typo、事例追加 |

本ガイド (v0.6) 準拠への改修は **minor bump** が標準 (判断軸は変えず形式のみ刷新)。

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

## <skill の中核> (Reference なら「判断軸」「フレームワーク」等、Task なら「What This Does」「手順」等)

<本体>

## 落とし穴

<合理化カタログ表>

## 関連

- `<related-skill>` — <1 行説明>
```

Reference / Task で中核節の名前は変わるが、**冒頭 mission / いつ使うか / 使わない場面 / 落とし穴 / 関連** の 5 節は共通骨格。

### 3.2 節番号は使わない

`## 1. Overview` `## 2. Prerequisites` のような番号付きは廃止。代わりに意味のある節タイトル。理由:

- 節の追加削除で番号がズレると既存引用 (`§3.5` 等) が破綻する
- 番号があると「全節読まないと分からない」印象を与える。実際は個別節で自己完結している方が AI / 人間双方に読みやすい
- 細番号参照 (§3.5) は、アンカー付きヘッダ (`#file-metadata-risk` 等) で代替できる

例外: `CHANGELOG.md` / `DESIGN.md` のような構造的文書は番号維持可。

### 3.3 冒頭 mission statement

skill タイトル直後、1 段落 (1-3 文) で次を書く:

- この skill が存在する理由 (なぜ必要か)
- 核となる主張 / 判断軸 / 動作

**良い例 (retrospective-codify):**

> タスクの終盤で「最初にこれを知っていれば遠回りしなかった」知見を抽出し、静的ルール・skill・常時有効ルールのいずれかに固定する。プロンプトに頼らず再現可能な形に落とすことを優先する。

**悪い例 (冗長、典型 AI 臭):**

> 大学業務において生成AIの活用が広がる中、「この情報をAIに入力して問題ないか」という判断は日常的に発生する。しかし、その判断基準が個人の感覚に委ねられている現状では、情報漏洩リスクと業務効率化の間で一貫性のある意思決定ができない。本スキルは、大学業務で扱う情報を3段階に分類し、生成AIサービスへの入力可否を構造的に判断するフレームワークを提供する。(3 段落中の 1 段落目)

後者は **背景 → 問題 → 解決** の論証構造を取っているが、skill 冒頭としては冗長。論証は References / Limitations 節に委ね、冒頭は断定で書く。

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

### 4.2 中核節 — Reference skill の場合

Reference skill の中核は「判断軸 / フレームワーク / 分類体系」。典型節名:

- `## 判断フロー` / `## 分類` / `## フレームワーク` / `## チェックリスト`
- `## 前提確認` (旧「Prerequisites」の改名、大学業務ガイドラインでは必須)
- `## 使用場面` (具体的な適用例 2-3 件、判断軸の運用例)
- `## 限界` (旧「Limitations」、所属大学規程との関係や適用外条件)

表 / Mermaid flowchart / Graphviz dot で可視化できるものはそうする。散文だけで判断ロジックを書かない。

### 4.3 中核節 — Task skill の場合

Anthropic 公式 Task content 慣習を維持:

```markdown
## What This Does

<1-2 段落、skill の動作>

## Required Inputs

<$ARGUMENTS で何を受け取るか>

## What It Produces

<出力構造、可能なら Markdown テンプレート添付>

## 手順

### 1. <ステップ名>
<動作>

### 2. <ステップ名>
<動作>

...

## 品質基準

- <これを満たさないと失格>
- <「気をつける」のような曖昧表現は避ける、具体動作で書く>

## Available Tools

- **<tool>**: <用途>
```

Task skill では `## いつ使うか` は What This Does と重複しがちだが、**起動 trigger の明示化のために重複させても OK**。description / when_to_use / いつ使うか の 3 箇所で trigger を書くことで AI の自動起動精度が上がる。

### 4.4 `## 落とし穴`

本ガイドで最も重要な新設節。合理化カタログを 2 列表で書く:

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

**意図:** AI のループ中に本テーブルの左列に該当する思考が出たら止まる。人間も本テーブルだけ読めば実運用での失敗を回避できる。

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

## 5. Reference / Task の差分

### 5.1 frontmatter

| field | Reference | Task |
|---|---|---|
| `name` | 必須 | 必須 |
| `description` | 必須、trigger 記述 | 必須、trigger 記述 |
| `when_to_use` | 通常不要 | 推奨 |
| `argument-hint` | 不要 | 推奨 |
| `allowed-tools` | 不要 | 推奨 |
| `disable-model-invocation` | 不要 | 副作用ある場合のみ |
| `version` / `last_updated` / `author` / `license` | 必須 | 必須 |

### 5.2 本文骨格

| 節 | Reference | Task |
|---|---|---|
| `# <skill 名>` | 必須 | 必須 |
| mission statement | 必須 (1-3 文) | 必須 (1-2 文) |
| `## いつ使うか` / 使わない場面 | 必須 | 必須 |
| 前提確認 / Prerequisites | 推奨 | 不要 |
| 判断軸 / フレームワーク | 必須 | ─ |
| `## What This Does` | ─ | 必須 |
| `## Required Inputs` | ─ | 必須 |
| `## What It Produces` | ─ | 必須 |
| `## 手順` | ─ | 必須 |
| `## 品質基準` | ─ | 必須 |
| `## Available Tools` | ─ | 必須 |
| 使用場面 / 判断例 | 推奨 | 推奨 (examples/ で代替可) |
| 限界 / Limitations | 推奨 | 推奨 |
| `## 落とし穴` | 必須 | 必須 |
| References | 推奨 | 不要 (関連節で代替) |
| `## 関連` | 必須 | 必須 |

### 5.3 典型行数

- Reference skill: 150-400 行 (判断軸の複雑さによる)
- Task skill: 150-300 行 (dispatch template 内蔵なら 300-400 行)

600 行を超える skill は内容を分割するか、`references/<topic>.md` に詳細を逃がす。

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

### 7.1 Reference skill の良い例 (新形式)

```markdown
---
name: confidential-info-guidelines
description: >
  大学業務で「この資料を AI に入れて大丈夫か」「どのサービスなら安全か」と
  判断が求められた時に使う、機密情報取扱の判断フレームワーク。情報分類が
  個人判断に揺れている現場で、3 段分類に基づく一貫した可否判断を提示する。
  所属大学規程が優先される前提で、汎用的な判定軸を提供する。
version: 1.3.0
last_updated: "2026-04-20"
author: gmoriki
license: CC BY-SA 4.0
---

# confidential-info-guidelines

大学業務で扱う情報を 3 段分類し、生成 AI サービスへの入力可否を構造的に判断するフレームワーク。所属大学規程が優先される前提で、判定が個人感覚に依存しない共通の物差しを提供する。

## いつ使うか

- 職員 / 研究者が「これ AI に入れていい？」と判断を迷った時
- 大学として AI 利用ガイドラインを策定 / 改定する時
- 情報漏洩インシデント後、判定基準を見直す時

使わない場面:
- 所属大学の独自ガイドラインで判定フローが確立している場合 (大学規程優先)
- 個別サービスの契約内容確認 (`awesome/tools.md` 等を参照)

## 前提確認

- 所属大学の AI 利用規程を確認済み
- 個人情報保護法の基本概念 (個人情報 / 要配慮個人情報 / 第三者提供制限) を把握
- 利用予定の AI サービスの利用規約 (学習利用可否 / 保存期間 / データセンター所在地) を確認

## 3 段分類

<表 / mermaid>

## 判断フロー

<mermaid>

## 落とし穴

| 出てくる合理化 | 実態 |
|---|---|
| 「Enterprise 契約なら何でも入力していい」 | ... |
| 「黒塗り PDF は安全」 | ... |
| 「匿名化すれば全て OK」 | ... |

## 限界

所属大学規程が本 skill と異なる場合、大学規程が優先。国公立 / 私立 / 学部規模 / 医学部の有無で判定が変わる論点がある。

## 関連

- `check-info-level` — 本 skill の Action 版、テキスト / ファイルを渡すと判定結果を返す
- `ai-use-risk-classification` — 4 分類版、大学 AI ポリシー起草時に使う
```

### 7.2 Task skill の良い例 (新形式)

既存の `check-info-level/SKILL.md` を本ガイドに沿って改修したもの。v0.6 改修後の形を参照。

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

- [ ] `description` を機能説明 → trigger 記述に書き換える (2.3 参照)
- [ ] 冒頭の `## 1. Overview` (3 段落等) を 1-3 文の mission statement に圧縮
- [ ] `## いつ使うか` + 使わない場面 節を新設 (mission の直後)
- [ ] 既存の `## 2. Prerequisites` を `## 前提確認` に改名、簡素化
- [ ] 中核節の番号を外す (`## 3. 情報分類の3段階` → `## 3 段分類` 等)
- [ ] `## 落とし穴` 節を新設 (Limitations の後、関連の前)
- [ ] `## 関連` 節を末尾に新設、本文中の依存 skill 参照をここへ集約
- [ ] 本文から AI 臭表現を削除 (6.1 のチェックリストで確認)
- [ ] frontmatter の `version` を minor bump、`last_updated` を更新
- [ ] `CHANGELOG.md` に改修エントリ追加

推定所要時間: 1 skill あたり 1-2 時間 (Reference の方が時間がかかる)。

---

## 9. 本ガイドの落とし穴

| 出てくる合理化 | 実態 |
|---|---|
| 「既存 skill 全部を一括で移行しよう」 | 一括は検証不足を生む。半期改訂 / Full 形化タイミングで順次移行が本方針 |
| 「description は既存のままでいいだろう、本文だけ直そう」 | description の trigger 化が最も効果大。本文改修より先に description を直す |
| 「落とし穴節は思い付かないから省こう」 | 思い付かない段階で skill として未成熟の signal。3 項目程度は捻り出す。ゼロは省略不可 |
| 「mizchi 水準に寄せれば寄せるほど良い」 | 口語 / 個人主観を入れると大学公式利用できなくなる。70-80% に抑える |
| 「節番号を全部外せばいい」 | `CHANGELOG.md` / `DESIGN.md` の節番号は維持。SKILL.md だけが対象 |
| 「関連節に同じリポジトリの skill だけ書く」 | 他リポジトリ (`superpowers:*` 等) も書いてよい。読み手が次に読むべきものを列挙 |
| 「examples/ があるから inline 例は不要」 | examples/ は few-shot 用、本文の具体性は別途必要。7 節のような inline ミニ例を入れる |

---

## 10. ガイド自身の更新

本ガイド (v0.6) は運用で不足が見つかったら改訂する。想定される改訂項目:

- mizchi 集の他 skill 調査結果 (ast-grep-practice / playwright-cli 等は今回未読)
- 実際の移行パイロット後のフィードバック (check-info-level / confidential-info-guidelines 改修の実体験)
- Anthropic 公式 Skills 仕様の更新 (2026-04 時点、今後 `user-invocable` / `paths` / `context: fork` 等の機能拡張が入る可能性)
- 他ランタイム (ChatGPT / Microsoft Copilot) 向け変換時の差分

改訂時は本ガイドの version (文中に明記せず、`last_updated` と CHANGELOG で管理) を更新し、移行チェックリスト (§8) に差分を追記する。

---

## 11. 関連

- `DESIGN.md` §2 原則 7 — 本ガイドの参照元
- `research/2026-04-20-mizchi-inspired-skills.md` — 本ガイド策定の調査記録
- `runtime-adapters/claude-code.md` — Claude Code 上での skill 配置 / 起動仕様
- `github.com/mizchi/chezmoi-dotfiles/dot_claude/skills` — 参照元 skill 集 (外部、CC / MIT 互換確認のうえ構造借用)
- `superpowers:writing-skills` — 新規 skill 作成時の TDD アプローチ (他リポジトリ)
- `skills/check-info-level/` — 新形式の Task skill 実装例 (v0.6 改修後)
- `skills/confidential-info-guidelines/` — 新形式の Reference skill 実装例 (v1.3.0)
