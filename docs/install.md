# インストールガイド

`higher-ed-ai-skills` は、必要な skill だけを AI エージェントに入れて使うことを想定しています。全 skill を一括導入する前に、利用部門、扱う情報、契約済み AI サービス、更新責任者を確認してください。

## 導入前に決めること

- どの大学業務で使うか。
- どの AI ランタイムで使うか。
- 誰が skill を更新するか。
- 学生データ、内部資料、研究データを扱う契約条件か。
- 所属大学の AI 利用ガイドライン、情報セキュリティポリシー、個人情報保護規程と矛盾しないか。

迷う場合は、最初に次の 3 点セットだけを入れてください。

- `check-info-level`
- `confidential-info-guidelines`
- `ai-use-risk-classification`

## Claude Code

個別 skill を入れる例です。

```bash
git clone https://github.com/gmoriki/higher-ed-ai-skills.git
mkdir -p ~/.claude/skills/
rm -rf ~/.claude/skills/higher-ed-check-info-level
cp -R higher-ed-ai-skills/skills/check-info-level \
  ~/.claude/skills/higher-ed-check-info-level
```

領域別 skill を入れる場合は、skill のディレクトリを直接コピーします。

```bash
rm -rf ~/.claude/skills/higher-ed-research-integrity-ai-disclosure
cp -R higher-ed-ai-skills/domain-skills/research-support/research-integrity-ai-disclosure \
  ~/.claude/skills/higher-ed-research-integrity-ai-disclosure
```

プロジェクト単位で使う場合は、対象プロジェクトの `.claude/skills/` にコピーします。

```bash
mkdir -p /path/to/project/.claude/skills/
rm -rf /path/to/project/.claude/skills/higher-ed-student-inquiry-triage
cp -R higher-ed-ai-skills/domain-skills/student-support/student-inquiry-triage \
  /path/to/project/.claude/skills/higher-ed-student-inquiry-triage
```

詳しい Claude Code 固有の運用は [runtime-adapters/claude-code.md](../runtime-adapters/claude-code.md) を参照してください。

## その他の Agent Skills 対応ランタイム

公式に `SKILL.md` ディレクトリ形式を登録できるランタイムでは、対象 skill ディレクトリをそのまま登録してください。環境ごとの最新手順は各サービスの公式ドキュメントを確認してください。`references/` や `examples/` がある skill は、ディレクトリごと登録します。

登録後、AI に次のように聞いて動作を確認します。

```text
架空の委員会資料カテゴリを使って、AI 入力前のトリアージをしてください。
本文や実ファイルは使わないでください。
```

## ChatGPT / Microsoft Copilot

現時点では、このリポジトリには ChatGPT や Microsoft Copilot 向けの正式 adapter はありません。代替として、次の範囲で使えます。

1. 使いたい skill の `SKILL.md` を開く。
2. 必要なら `references/` の関連ファイルも開く。
3. AI の instructions や knowledge に入れる。
4. 機密情報や学生データをアップロードする前に、所属大学の契約条件を確認する。

この方法はネイティブな Agent Skills ではありません。tool 呼び出し、ファイル読み取り、subagent dispatch などは動かない場合があります。

## 部局別の最小構成

| 部局・用途 | 推奨 skill |
|---|---|
| 共通の入力前確認 | `check-info-level`, `confidential-info-guidelines`, `ai-use-risk-classification` |
| 教務・教学 | `syllabus-ai-policy`, `student-inquiry-triage` |
| 入試 | `entrance-exam-ai-policy`, `check-info-level` |
| 学生支援 | `student-inquiry-triage`, `multilingual-student-communication`, `ai-tone-check` |
| 研究支援 | `research-integrity-ai-disclosure`, `confidential-info-guidelines` |
| IR・内部質保証 | `ir-freeform-text-analysis`, `check-info-level` |
| 広報 | `pr-ai-checklist`, `ai-tone-check` |
| 組織導入・研修 | `check-info-level`, `confidential-info-guidelines`, `ai-use-risk-classification`, `institutional-ai-adoption-checklist`, `staff-ai-literacy-primer` |

## 更新

このリポジトリは半期改訂を前提にしています。コピー方式で導入した場合は、更新時に再コピーしてください。

```bash
cd higher-ed-ai-skills
git pull origin main
rm -rf ~/.claude/skills/higher-ed-check-info-level
cp -R skills/check-info-level \
  ~/.claude/skills/higher-ed-check-info-level
```

既存ディレクトリにそのまま `cp -R` すると、`higher-ed-check-info-level/check-info-level/` のようにネストして更新されない場合があります。更新時は削除してからコピーするか、`rsync --delete` で同期してください。

```bash
rsync -a --delete skills/check-info-level/ \
  ~/.claude/skills/higher-ed-check-info-level/
```

シンボリックリンクで導入した場合は、clone 元を `git pull` すれば反映されます。ただし、組織利用では更新内容を確認してから反映してください。

## 命名

他の skill 集と併用する場合は、インストール先ディレクトリ名に `higher-ed-` prefix を付けることを推奨します。

```text
~/.claude/skills/higher-ed-check-info-level/
~/.claude/skills/higher-ed-syllabus-ai-policy/
```

## 動作確認

導入後は、実データではなく架空の資料カテゴリで試してください。

```text
架空の教授会資料です。
議題に通常報告、予算途中経過、人事案件が混ざる可能性があります。
本文を読まずに、入力前トリアージと次に確認すべき情報カテゴリを返してください。
```

実データ、学生情報、人事、入試、未公表研究データを使った動作確認は避けてください。
