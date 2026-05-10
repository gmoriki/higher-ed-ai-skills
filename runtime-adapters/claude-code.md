---
title: Claude Code での higher-ed-ai-skills 活用ガイド
version: 1.1.0
last_updated: "2026-05-10"
author: gmoriki
license: CC BY-SA 4.0
---

# Claude Code での higher-ed-ai-skills 活用ガイド

本ガイドは、Claude Code で `higher-ed-ai-skills` を使うための導入メモです。詳細な設計思想は [AGENTS.md](../AGENTS.md)、skill の書き方は [references/skill-format-guide.md](../references/skill-format-guide.md) を正とします。

## 位置付け

`higher-ed-ai-skills` は、大学職員が AI エージェントに大学業務を頼むための skill 集です。Claude Code では、各 skill ディレクトリを `~/.claude/skills/` またはプロジェクトの `.claude/skills/` に配置して使います。

旧 `Reference / Task` 二分類は使いません。全 skill は unified protocol です。違いは、判定だけで終わるか、文案作成やレビューを返すか、副作用があるかです。

## 最小導入

入力前トリアージの 3 点セットを入れます。

```bash
git clone https://github.com/gmoriki/higher-ed-ai-skills.git
mkdir -p ~/.claude/skills/
rm -rf ~/.claude/skills/higher-ed-check-info-level
cp -R higher-ed-ai-skills/skills/check-info-level \
  ~/.claude/skills/higher-ed-check-info-level
rm -rf ~/.claude/skills/higher-ed-confidential-info-guidelines
cp -R higher-ed-ai-skills/skills/confidential-info-guidelines \
  ~/.claude/skills/higher-ed-confidential-info-guidelines
rm -rf ~/.claude/skills/higher-ed-ai-use-risk-classification
cp -R higher-ed-ai-skills/skills/ai-use-risk-classification \
  ~/.claude/skills/higher-ed-ai-use-risk-classification
```

動作確認は、実データではなく架空カテゴリで行います。

```text
架空の教授会資料です。
通常報告、予算途中経過、人事案件が混ざる可能性があります。
本文を読まずに、入力前トリアージをしてください。
```

## 部局別導入

| 部局・用途 | 追加する skill |
|---|---|
| 教務・教学 | `domain-skills/academic-affairs/syllabus-ai-policy` |
| 入試 | `domain-skills/academic-affairs/entrance-exam-ai-policy` |
| 学生支援 | `domain-skills/student-support/student-inquiry-triage` |
| 国際 | `domain-skills/international-office/multilingual-student-communication` |
| 研究支援 | `domain-skills/research-support/research-integrity-ai-disclosure` |
| IR・内部質保証 | `domain-skills/ir-analysis/ir-freeform-text-analysis` |
| 広報 | `domain-skills/public-relations/pr-ai-checklist`, `skills/ai-tone-check` |
| 会議運営 | `skills/committee-meeting-minutes-ai` |
| 組織導入・研修 | `skills/ai-use-risk-classification`, `skills/institutional-ai-adoption-checklist`, `skills/staff-ai-literacy-primer` |

例:

```bash
rm -rf ~/.claude/skills/higher-ed-student-inquiry-triage
cp -R higher-ed-ai-skills/domain-skills/student-support/student-inquiry-triage \
  ~/.claude/skills/higher-ed-student-inquiry-triage
```

## プロジェクト単位の導入

大学や部局ごとの private repository に `.claude/skills/` を置くと、学内規程や部局用語を加えた運用ができます。

```bash
mkdir -p .claude/skills/
rm -rf .claude/skills/higher-ed-check-info-level
cp -R /path/to/higher-ed-ai-skills/skills/check-info-level \
  .claude/skills/higher-ed-check-info-level
rm -rf .claude/skills/higher-ed-ir-freeform-text-analysis
cp -R /path/to/higher-ed-ai-skills/domain-skills/ir-analysis/ir-freeform-text-analysis \
  .claude/skills/higher-ed-ir-freeform-text-analysis
```

ローカル改変を行う場合は、upstream 更新と混ざらないよう fork または別リポジトリで管理してください。

## skill 間の依存

多くの業務別 skill は、入力前確認として次を参照します。

- `check-info-level`
- `confidential-info-guidelines`
- `ai-use-risk-classification`

業務別 skill だけを入れると、AI が情報区分や利用区分の定義を参照できず、出力が一般論に寄ることがあります。最低でも 3 点セットを同じ skill ディレクトリに入れてください。

## tool 依存

一部 skill は Claude Code の tool に依存します。

| skill | tool | 注意 |
|---|---|---|
| `check-info-level` | `Read`, `Bash(file:*)`, `Bash(pdfinfo:*)` | 明示的にファイル内容判定を依頼された場合のみ読む。本文を読まない事前トリアージではファイルを開かない |
| `ai-tone-check` | `Read`, `Task` | subagent dispatch が使える top-level セッション向け |
| `create-action-skill` | `Read`, `Write`, `Bash(mkdir:*)` | 新規ファイル作成の副作用があるため、明示承認が必要 |

tool が使えない runtime では、skill は「読める手順」として使えますが、ファイル読み取りや subagent dispatch は実行できません。

## deprecated を入れない

`deprecated/` 配下は Claude Code の skill 検出対象に入れないでください。旧 skill と現行 skill が同時に発火し、判断がぶれる可能性があります。

## 更新

コピー方式で導入している場合:

```bash
cd higher-ed-ai-skills
git pull origin main
rm -rf ~/.claude/skills/higher-ed-check-info-level
cp -R skills/check-info-level ~/.claude/skills/higher-ed-check-info-level
```

既存ディレクトリに直接 `cp -R` するとネストして更新されないことがあります。更新時は削除してからコピーするか、`rsync --delete` で同期してください。

```bash
rsync -a --delete skills/check-info-level/ \
  ~/.claude/skills/higher-ed-check-info-level/
```

シンボリックリンク方式なら、clone 元の `git pull` で反映されます。組織利用では、更新内容を確認してから反映してください。

## トラブルシューティング

### 汎用回答になる

次のように skill 名を明示します。

```text
higher-ed-ai-skills の `check-info-level` と `student-inquiry-triage` を使ってください。
入力前確認、判定、根拠、推奨対応、確認先、残リスクを分けて返してください。
```

### 実データを読もうとする

次のように止めます。

```text
本文やファイルはまだ読まないでください。
資料種別、公開範囲、情報カテゴリ、処理目的、AI 実行環境だけで事前トリアージしてください。
```

### skill が古い

[docs/update-policy.md](../docs/update-policy.md) の半期改訂方針に従い、`metadata.last_updated` と [CHANGELOG.md](../CHANGELOG.md) を確認してください。
