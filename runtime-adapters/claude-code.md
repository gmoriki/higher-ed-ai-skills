---
title: Claude Code での higher-ed-ai-skills 活用ガイド
version: 1.0.0
last_updated: "2026-04-19"
author: gmoriki
license: CC BY-SA 4.0
---

# Claude Code での higher-ed-ai-skills 活用ガイド

本ガイドは、Anthropic の CLI ツール **Claude Code** を利用する大学職員・教職員が、本リポジトリ（higher-ed-ai-skills）の 12 スキルを自分の作業環境に組み込むための手順書である。

> **本書の位置づけ**: 本リポジトリの設計思想は `DESIGN.md` §4「ランタイム非依存の思想」に基づく。skill.md を Single Source of Truth（唯一の正）として扱い、各ランタイム向けの実行方法は `runtime-adapters/` 配下に分離する。本ガイドはその最初の実装として Claude Code 向けの導入手順を整理したものである。
>
> **前提**: 本書の記載は 2026 年 4 月時点の Claude Code の仕様に基づく。Claude Code の仕様は頻繁に変わる可能性があるため、公式ドキュメントも併せて参照してほしい。

---

## 1. Claude Code の skill 仕組み概要

Claude Code は、ローカルディレクトリに配置された markdown ファイルを「スキル」として自動認識する仕組みを持つ。2026 年 4 月時点での挙動は以下のとおりと想定される。

- **グローバル配置先**: `~/.claude/skills/` 配下の `.md` ファイルおよびサブディレクトリ内の `SKILL.md` が自動検出される。
- **プロジェクト配置先**: 現在の作業ディレクトリ（およびその親ディレクトリを遡って最初に見つかる）の `.claude/skills/` 配下も同様に認識される。
- **トリガー条件**: スキルの冒頭 YAML frontmatter にある `description` フィールドが、ユーザーの発話と照合され、関連度が高いと判断されるとスキル本体が読み込まれる（Progressive Disclosure の第 1 段階）。
- **補助ファイルの扱い**: `SKILL.md` 本体で明示的に参照された `examples/` や `references/` 配下のファイルは、必要時にのみ AI が読み込む。常時コンテキストに展開されるわけではない。

この仕組みは、本リポジトリが採用する「description をトリガー設計として書く」「本体は判断ロジックに絞る」「詳細は references へ」という設計原則（`DESIGN.md` §2）と自然に整合する。Claude Code は本リポジトリの skill.md を、そのままの構造で活用できる数少ないランタイムである。

ただし、Claude Code の仕様は短期間で変更されうる。以下の手順は「2026 年 4 月時点の推奨」として読んでほしい。

---

## 2. 個人環境（~/.claude/skills/）への配置

### 2-1. 全スキル一括導入

本リポジトリの 12 スキルをまとめて個人の Claude Code 環境に取り込む方法を示す。

#### 方法 A: git clone して配置

```bash
# 作業用ディレクトリでクローン
cd ~/Documents
git clone https://github.com/gmoriki/higher-ed-ai-skills.git

# ~/.claude/skills/ 配下にサブディレクトリとして配置
mkdir -p ~/.claude/skills/
cp -R ~/Documents/higher-ed-ai-skills/skills/* ~/.claude/skills/
cp -R ~/Documents/higher-ed-ai-skills/domain-skills/* ~/.claude/skills/
```

この方式はファイルをコピーするため、upstream の更新を反映するには再度 `cp -R` を実行する必要がある。

#### 方法 B: symbolic link を張る

```bash
# クローンしたリポジトリを ~/.claude/skills/ からリンクする
mkdir -p ~/.claude/skills/
ln -s ~/Documents/higher-ed-ai-skills/skills/confidential-info-guidelines \
      ~/.claude/skills/higher-ed-confidential-info-guidelines
# 必要なスキルぶん繰り返す
```

symbolic link を使うと、`git pull` で upstream を更新すれば自動的に反映される。ローカルで改変しない運用に向く。

#### 方法 C: リポジトリ丸ごとをサブディレクトリに置く

```bash
mkdir -p ~/.claude/skills/
git clone https://github.com/gmoriki/higher-ed-ai-skills.git \
          ~/.claude/skills/higher-ed-ai-skills
```

この方式は簡便だが、Claude Code が `~/.claude/skills/higher-ed-ai-skills/` 配下の `SKILL.md` をどこまで再帰的に検出するかは実装に依存する。動作しない場合は方法 A/B に切り替える。

#### 命名衝突の回避

他の公開スキル集と併用する場合、`confidential-info-guidelines` のような一般的な名前は衝突しやすい。以下のように prefix を付けて配置することを推奨する。

```bash
cp -R ~/Documents/higher-ed-ai-skills/skills/confidential-info-guidelines \
      ~/.claude/skills/higher-ed-confidential-info-guidelines
```

### 2-2. 個別スキル選択導入

全 12 スキルではなく必要なものだけを入れたい場合の手順。

```bash
# 例: confidential-info-guidelines のみ導入
mkdir -p ~/.claude/skills/
cp -R ~/Documents/higher-ed-ai-skills/skills/confidential-info-guidelines \
      ~/.claude/skills/
```

担当業務が明確な職員は、この個別導入が現実的である。たとえば以下のような組み合わせが想定される。

- 情報セキュリティ担当: `confidential-info-guidelines` / `ai-use-risk-classification` / `institutional-ai-adoption-checklist`
- 教務担当: `confidential-info-guidelines` / `domain-skills/academic-affairs/` 配下
- IR 担当: `confidential-info-guidelines` / `domain-skills/ir-analysis/` 配下
- 研究支援担当: `confidential-info-guidelines` / `domain-skills/research-support/` 配下

### 2-3. 更新 pull の運用

本リポジトリは **半期改訂**（3 月末・9 月末）を原則としている（`DESIGN.md` §5）。更新への追従方法は以下のとおり。

```bash
cd ~/Documents/higher-ed-ai-skills
git pull origin main

# symbolic link 方式なら以降の操作は不要
# cp 方式の場合は再度コピー
cp -R ~/Documents/higher-ed-ai-skills/skills/* ~/.claude/skills/
```

ローカルで独自改変を積みたい場合は GitHub 上で fork し、自分の fork を clone して運用することを推奨する。fork 運用なら、upstream の更新を `git remote add upstream ...` で取り込みつつ、ローカル修正は自分の branch で保持できる。

---

## 3. プロジェクト単位（.claude/skills/）での運用

個人環境全体に導入するのではなく、特定のプロジェクト（リポジトリ）だけでスキルを有効化したい場合の運用を示す。

### 3-1. 大学ごとの private リポジトリでの配置

大学ごとに用語・規程・運用が異なるため、upstream をそのまま使うよりも「所属大学用の私的リポジトリに必要スキルをコピーし、大学固有のカスタマイズを加える」運用が想定される。

```bash
# 所属大学用リポジトリの例
cd ~/Documents/my-univ-ai-playbook
mkdir -p .claude/skills/
cp -R ~/Documents/higher-ed-ai-skills/skills/confidential-info-guidelines \
      .claude/skills/
cp -R ~/Documents/higher-ed-ai-skills/skills/ai-use-risk-classification \
      .claude/skills/
# 大学固有の改変は .claude/skills/ 配下で直接行う
```

この運用の利点は、大学固有の用語置換（例: 「学部」→「学群」、「教務部」→「教育支援課」）や、学内 AI サービス（Azure OpenAI 契約など）への言及追加などを upstream と分離して管理できる点である。

### 3-2. 部局別の切り分け

部局ごとに有効化したいスキルが異なる場合、部局の業務リポジトリごとに `.claude/skills/` を設けるとよい。想定される切り分け例を示す。

| 部局 | 推奨スキル |
|------|------------|
| 教務部 | `domain-skills/academic-affairs/syllabus-ai-policy` / `confidential-info-guidelines` |
| 研究推進部 | `domain-skills/research-support/research-integrity-ai-disclosure` / `confidential-info-guidelines` |
| 広報部 | `domain-skills/public-relations/` 配下 / `confidential-info-guidelines` |
| IR 部門 | `domain-skills/ir-analysis/ir-freeform-text-analysis` / `confidential-info-guidelines` |
| 学生支援部 | `domain-skills/student-support/student-inquiry-triage` / `confidential-info-guidelines` |

部局ごとに `.claude/skills/` を分けることで、「自部局に関係ないスキルが誤起動する」リスクを抑えられる。また、`confidential-info-guidelines` はどの部局でも共通で配置することを推奨する。

---

## 4. スキル間の依存関係と呼び出し

本リポジトリのスキルは、互いを参照しあう設計になっている箇所がある。Claude Code は依存関係を自動解決しないため、利用者側で揃えて配置する必要がある。

### 4-1. `confidential-info-guidelines` を前提とするスキル

以下のスキルは、内部で `confidential-info-guidelines` の 3 段分類（区分 I / II / III）を参照している。

- `committee-meeting-minutes-ai`（議事録 AI 化）
- `domain-skills/ir-analysis/ir-freeform-text-analysis`（自由記述の IR 分析）
- `domain-skills/student-support/student-inquiry-triage`（学生問い合わせのトリアージ）
- その他、学生データや会議資料を扱う domain-skills の多く

これらを導入する場合、`confidential-info-guidelines` も必ず同じ場所（`~/.claude/skills/` または同一プロジェクトの `.claude/skills/`）に配置する。依存側のスキルだけ入れても、AI が 3 段分類の定義を参照できず、期待どおり動かない。

### 4-2. `ai-use-risk-classification` との組み合わせ

`ai-use-risk-classification` は「業務場面での AI 利用の 4 区分判定」を提供する。`confidential-info-guidelines` の「情報機密性の 3 段分類」と併用すると、次の順序での呼び出しが推奨される。

1. まず業務場面を `ai-use-risk-classification` で 4 区分判定する（禁止 / 要承認 / 要注意 / 許容 など）。
2. 許容寄りの区分であれば、扱う情報を `confidential-info-guidelines` で 3 段分類する。
3. 情報分類に応じた AI サービスの選定を行う。

この順序は「業務場面 → 情報機密性」であり、逆順（先に情報だけで判断し、業務文脈を見落とす）は推奨しない。

### 4-3. 競合シナリオ（旧 deprecated スキルとの同居）

`deprecated/` 配下には、役割を後発スキルに引き継いだ旧スキルが残されている（例: `advanced-prompting-for-admin`, `ai-report-evaluation`, `tool-selection-guide`）。これらを誤ってグローバル環境に置いてしまうと、新スキルと競合する可能性がある。

対応方針:

- 原則として `deprecated/` 配下は Claude Code のスキル検出対象から外す。
- 既に導入済みの場合は、`~/.claude/skills/` から該当ディレクトリを外すか、ファイル名の末尾に `.disabled` を付けるなどして無効化する。
- どうしても旧スキルを参照したい場合は、本体冒頭の「非推奨／代替スキルへの誘導」記述が残っていることを確認する（`DESIGN.md` §5.4）。

---

## 5. トラブルシューティング

### 5-1. 日本語 description が英語と混合して解釈される

本リポジトリのスキルは日本語で書かれているが、Claude Code のロケールやモデルの挙動によっては、応答が英語混じりになることがある。

対処策:

- セッション冒頭で「以降の応答は日本語で行ってください」と明示的に指示する。
- プロジェクトの `CLAUDE.md`（または `~/.claude/CLAUDE.md`）に「本プロジェクトでは日本語で応答する」旨を記載する。
- description 側には手を加えず、ユーザー指示側で言語を固定するほうが副作用が少ない。

### 5-2. mermaid 図が Claude Code 上で描画されない

本リポジトリのスキルでは mermaid 構文で判断フローを示している箇所がある。Claude Code のターミナル出力は mermaid を図として描画しないが、AI は構文として理解できるため判断ロジックの読み取りには支障はない。

視覚的に確認したい場合は、GitHub 上で該当の `SKILL.md` を開くと mermaid が図として描画される。Claude Code 上で図を見る前提で設計されていない点に留意してほしい。

### 5-3. frontmatter parse エラー

スキルを自作・改変したときに、frontmatter の YAML 構文エラーで読み込まれないことがある。典型的な原因は以下。

- インデントがスペースとタブで混在している。
- 値にコロン（`:`）を含む文字列をクォートしていない。
- 複数行の description で `>` や `|` の使い方を誤っている。
- `last_updated: 2026-04-19` のように日付をクォートせずに書くと、YAML パーサによっては日付オブジェクトとして解釈され、他の処理で文字列前提のコードが動かないことがある。本リポジトリでは `last_updated: "2026-04-19"` のように**必ずクォートする**方針を採っている。

エラー発生時は `python -c "import yaml; yaml.safe_load(open('SKILL.md').read().split('---')[1])"` などで frontmatter だけを切り出して検証すると原因特定が速い。

### 5-4. グローバルとプロジェクトでの名前衝突

`~/.claude/skills/confidential-info-guidelines/` と、プロジェクト `.claude/skills/confidential-info-guidelines/` の両方に同名スキルが存在する場合、どちらが優先されるかは Claude Code の実装に依存する。2026 年 4 月時点では「プロジェクト側が優先される」挙動が一般的と想定されるが、確証はない。

推奨:

- グローバル側は upstream をそのまま置き、大学固有改変はプロジェクト側でのみ行う。
- プロジェクト側で改変した場合は、`SKILL.md` の frontmatter に `author: gmoriki + 〇〇大学` のように追記して由来を明示する。
- どちらが実際に読まれているか疑わしいときは、Claude Code セッションで「いまロードされているスキルの description を教えて」と尋ねて確認する。

---

## 6. 更新運用

### 6-1. 半期改訂時の追従

本リポジトリは 3 月末・9 月末の半期改訂を原則としている。改訂タイミングに合わせて以下を行うことを推奨する。

```bash
cd ~/Documents/higher-ed-ai-skills
git pull origin main

# CHANGELOG で変更点を確認
less CHANGELOG.md
```

`CHANGELOG.md` は Keep a Changelog 形式で記述されており、「Added / Changed / Deprecated / Removed」の区分で変更を追える。とくに `Changed` と `Deprecated` はローカルカスタマイズへの影響が出やすいため重点的に確認する。

### 6-2. カスタマイズと upstream の整合

所属大学の用語や規程に合わせて改変する場合、以下の判断が必要になる。

- **汎用的な改善**（typo、文意の改善、新しいサービスへの言及追加など）は upstream への Pull Request を送ることを推奨する。`CONTRIBUTING.md` を参照。
- **大学固有の改変**（自学名の差し込み、学内 AI サービスの具体名など）は upstream には送らず、fork または大学内リポジトリで保持する。
- いずれの場合も、`DESIGN.md` §2 の 5 原則（Progressive Disclosure / description はトリガー設計 / 本体は判断ロジック / 模範回答 / 陳腐化前提の更新設計）を外さない範囲でのカスタマイズが望ましい。

---

## 7. 参考

- Claude Code 公式ドキュメント: <https://docs.anthropic.com/ja/docs/claude-code> （URL は 2026 年 4 月時点のもの。仕様の最新情報はこちらを参照）
- 本リポジトリの `DESIGN.md` §4「ランタイム非依存の思想」
- 本リポジトリの `docs/how-to-use.md`（パターン A/B/C の使い方概観）
- 本リポジトリの `CONTRIBUTING.md`（改変・PR の方針）

他のランタイム（ChatGPT / Microsoft Copilot / GitHub Copilot / ローカル LLM）向けのアダプタは、本リポジトリ v0.5 以降で順次追加予定である。

---

*本ガイド自体も半期改訂の対象である。Claude Code の仕様変更に追従できていない記述があれば、Issue または PR で指摘してほしい。*
