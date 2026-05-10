---
name: create-action-skill
description: >
  大学職員や研究支援職員が「自分の業務ノウハウを Agent Skill にしたい」
  「部署の暗黙知を SKILL.md に構造化したい」「新しい higher-ed-ai-skills 用 skill を
  作りたい」と明示した時に使う。業務目的、利用者、入力前確認、判断軸、
  出力フォーマット、落とし穴、関連 skill、配置先、ライセンスをヒアリングし、
  unified protocol 形式の SKILL.md と example を生成する。
compatibility: >
  Requires Claude Code or equivalent runtime with file writing tools.
  Creates new files only after explicit user approval.
allowed-tools: Read Write Bash(mkdir:*) Bash(ls:*)
license: CC BY-SA 4.0
metadata:
  version: "1.1.0"
  last_updated: "2026-05-10"
  author: gmoriki
  disable-model-invocation: true
---

# create-action-skill

大学業務の暗黙知を、AI エージェントが実行できる `SKILL.md` に変換する。旧 Reference / Task 二分類は使わず、すべて unified protocol として、入力前確認、判断軸、出力フォーマット、落とし穴を持つ skill を作る。

## いつ使うか

- 大学職員が自分の業務ノウハウを skill 化したい時。
- 部署の運用、確認経路、判断基準を AI エージェントに渡せる形にしたい時。
- `higher-ed-ai-skills` に新しい大学業務 skill を追加したい時。
- 既存 skill の抜けを埋める新領域を設計したい時。

使わない場面:

- 単に README や手順書を人間向けに書きたいだけの時。
- 外部公開できない学内規程や個人情報をそのまま skill に入れたい時。
- ファイル作成の承認がない時。

## 入力前の確認

ヒアリングで、実データや内部文書をそのまま求めない。まず次のカテゴリで聞く。

- 業務名と業務目的。
- 想定利用者: 職員、教員、研究支援、管理職、学生対応など。
- ユーザーが実際に言いそうな相談文。
- 扱う情報カテゴリ: 学生、人事、入試、研究、会議、公開情報など。
- AI が返すべき成果物。
- 所属大学で確認すべき規程、部署、決裁権者。
- よくある誤りや合理化。
- 外部根拠とライセンス。

内部資料が必要な場合は、公開できる抽象化、架空例、項目名だけに変換してもらう。

## ヒアリング項目

1. **業務概要**: どの大学業務を支援する skill か。
2. **発話 trigger**: ユーザーがどんな言葉で相談した時に起動すべきか。
3. **使う場面 / 使わない場面**: 対象と除外。
4. **入力前確認**: 本文やファイルを読む前に確認すべき情報カテゴリ。
5. **中核判断軸**: 分類、手順、チェックリスト、フロー。
6. **出力フォーマット**: AI が返す Markdown 構造。
7. **確認先**: 規程、担当部署、決裁権者、記録化。
8. **落とし穴**: 現場で起こる合理化と実態。
9. **関連 skill**: 連携すべき既存 skill。
10. **配置先**: `skills/` か `domain-skills/<area>/`。
11. **ライセンス**: 引用可否、構造参照、出典。

## 配置先

| 配置 | 用途 |
|---|---|
| `skills/` | 複数業務で使う横断 skill、入力前確認、組織導入、文書確認、skill 作成 |
| `domain-skills/academic-affairs/` | 教務・教学・入試 |
| `domain-skills/student-support/` | 学生支援 |
| `domain-skills/international-office/` | 国際・留学生 |
| `domain-skills/research-support/` | 研究支援 |
| `domain-skills/ir-analysis/` | IR・内部質保証 |
| `domain-skills/public-relations/` | 広報・文書 |

新領域が必要な場合は、README と roadmap も更新する。

## 生成する構造

```text
<skill-name>/
  SKILL.md
  examples/example-01-<scenario>.md
  references/   # 必要な場合のみ
```

## SKILL.md テンプレート

````markdown
---
name: <skill-name>
description: >
  <発話 trigger、業務場面、返すもの、除外条件>
license: CC BY-SA 4.0
metadata:
  version: "1.0.0"
  last_updated: "<YYYY-MM-DD>"
  author: gmoriki
---

# <skill-name>

<1-3 文の mission。AI エージェントが何を確認し、何を返すかを書く。>

## いつ使うか

- <使う場面>

使わない場面:
- <除外条件>

## 入力前の確認

- <本文やファイルを読む前に確認する情報カテゴリ>
- <未確認なら質問すること>

## <中核節>

<判断軸、手順、チェックリスト、フロー>

## 出力フォーマット

```markdown
## 判定
<実行可 / 条件付き / 要確認 / 不可>

## 根拠
- 業務目的:
- 扱う情報カテゴリ:
- 判断に使う規程・担当部署・決裁権者:

## 推奨対応
1. <AI エージェントが行う作業>
2. <職員・担当部署が確認する作業>

## AI に渡してよい資料範囲
- <公開情報 / 学内限定 / 匿名化済み / 渡さない情報>

## 確認先
- <規程 / 担当部署 / 委員会 / 決裁権者>

## 残リスク
- <未確認事項、外部根拠、制度差、運用上の例外>
```

## 落とし穴

| 合理化 | 実態 |
|---|---|

## 関連

- `<related-skill>` — <関係>
````

## 出力フォーマット

```markdown
## 作成計画
- skill 名:
- 配置先:
- 想定利用者:
- 発話 trigger:

## 確認したい不足情報
- <本文ではなく情報カテゴリで質問>

## 生成物
- `SKILL.md`
- `examples/example-01-...md`

## 変更したファイル
- <path>

## 残リスク
- <外部根拠、ライセンス、未確認規程>
```

## 落とし穴

| 合理化 | 実態 |
|---|---|
| Reference / Task のどちらかを選ばせる | 旧分類。全 skill は unified protocol として書く |
| 学内規程をそのまま貼ればよい | 公開できない情報や著作権上の問題がある。抽象化して書く |
| 使い方を丁寧に説明すれば skill になる | AI が何を確認し、何を返すかが必要 |
| 出力例を省く | Agent skill は返す形がないと実行がぶれる |
| 落とし穴を省く | 大学業務では合理化の抑止が品質に直結する |
| ファイル作成を自動で進める | 副作用があるため、配置先と作成ファイルを明示してから進める |

## 関連

- [`references/skill-format-guide.md`](../../references/skill-format-guide.md) — SKILL.md の標準形式。
- [`AGENTS.md`](../../AGENTS.md) — リポジトリ設計思想。
- [`confidential-info-guidelines`](../confidential-info-guidelines/SKILL.md) — 入力前確認の基礎。
