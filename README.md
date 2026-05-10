# higher-ed-ai-skills

日本の大学職員が AI エージェントに大学業務を頼むための Agent Skills 集です。

教務、学生支援、研究支援、IR、広報、国際、委員会運営、研修、文書確認などの実務を、大学固有の規程、権限、情報管理、承認経路を踏まえて支援します。

[English](README.en.md)

## これは何か

大学業務には、規程だけでは扱いきれない判断が多くあります。稟議、委員会、教員と職員の権限分離、学生データ、年度サイクル、部局ごとの慣行は、そのまま AI に頼みにくい知識です。

このリポジトリは、その暗黙知を `SKILL.md` 形式で公開します。主な読者は AI エージェントです。大学職員は、AI エージェントに自然文で相談し、必要な skill を呼び出してもらう想定です。

## まず安全確認

本文やファイルを渡す前に、資料種別、公開範囲、情報カテゴリ、処理目的、利用する AI 環境を先に確認します。判断に必要な場合でも、いきなり全文を読ませるのではなく、まずカテゴリ情報だけでトリアージします。

```text
教授会資料を要約したいです。
本文はまだ渡しません。
資料種別、含まれそうな情報カテゴリ、AI 実行環境をもとに、入力可否の事前トリアージをしてください。
```

| やりたいこと | 最初に使う skill | 次に使う skill |
|---|---|---|
| 資料を AI に渡してよいか事前確認したい | [check-info-level](skills/check-info-level/) | [confidential-info-guidelines](skills/confidential-info-guidelines/) |
| 情報区分と入力条件を整理したい | [confidential-info-guidelines](skills/confidential-info-guidelines/) | [ai-use-risk-classification](skills/ai-use-risk-classification/) |
| 業務として AI を使ってよい範囲を決めたい | [ai-use-risk-classification](skills/ai-use-risk-classification/) | [institutional-ai-adoption-checklist](skills/institutional-ai-adoption-checklist/) |

## 業務別に頼む

| 業務 | 相談例 | 使う skill | 返すもの |
|---|---|---|---|
| 会議運営 | 委員会議事録で AI を使える範囲を整理したい | [committee-meeting-minutes-ai](skills/committee-meeting-minutes-ai/) | 議題分類、利用可否、確認先、運用手順 |
| 教務・教学 | シラバスに生成 AI 利用方針を入れたい | [syllabus-ai-policy](domain-skills/academic-affairs/syllabus-ai-policy/) | 方針レベル、文案例、周知方法 |
| 入試 | 志望理由書での AI 使用方針を出願要項に書きたい | [entrance-exam-ai-policy](domain-skills/academic-affairs/entrance-exam-ai-policy/) | 記載方針、疑義対応、委員会確認事項 |
| 学生対応 | 学生問い合わせを AI 回答と有人対応に分けたい | [student-inquiry-triage](domain-skills/student-support/student-inquiry-triage/) | 問い合わせ分類、エスカレーション基準、残リスク |
| 国際 | 留学生向け案内を多言語化したい | [multilingual-student-communication](domain-skills/international-office/multilingual-student-communication/) | 文書種別判定、確認者、翻訳手順 |
| 研究支援 | 論文・科研費での AI 利用開示について相談された | [research-integrity-ai-disclosure](domain-skills/research-support/research-integrity-ai-disclosure/) | 開示要否、禁止事項、確認すべき規程 |
| IR・内部質保証 | 学生アンケート自由記述を分析したい | [ir-freeform-text-analysis](domain-skills/ir-analysis/ir-freeform-text-analysis/) | 匿名化手順、分析手順、検証観点 |
| 広報・文書 | 広報原稿や学生向け案内を公開前に確認したい | [pr-ai-checklist](domain-skills/public-relations/pr-ai-checklist/), [ai-tone-check](skills/ai-tone-check/) | 事実確認、読者負荷、トーン改善案 |

## 組織導入・研修

AI governance は独立した目的ではなく、大学業務を安全に進めるための組織整備として扱います。

| やりたいこと | 使う skill | 返すもの |
|---|---|---|
| 部署や全学の AI 利用ルールを整理したい | [ai-use-risk-classification](skills/ai-use-risk-classification/) | 禁止・限定・推奨・開放の区分案 |
| 委員会や執行部に AI 導入を上げたい | [institutional-ai-adoption-checklist](skills/institutional-ai-adoption-checklist/) | 成熟度診断、論点表、上程メモ |
| 職員向け研修を作りたい | [staff-ai-literacy-primer](skills/staff-ai-literacy-primer/) | 30-60 分研修骨子、演習、確認問題 |

## Skill 作成・保守

大学業務の暗黙知を新しい skill にする場合は、[create-action-skill](skills/create-action-skill/) を使います。設計方針は [AGENTS.md](AGENTS.md)、文書形式は [references/skill-format-guide.md](references/skill-format-guide.md) を参照してください。

## 全 skill catalog

| 区分 | Skill | Version |
|---|---|---|
| まず安全確認 | [confidential-info-guidelines](skills/confidential-info-guidelines/) | 1.5.0 |
| まず安全確認 | [check-info-level](skills/check-info-level/) | 1.3.0 |
| まず安全確認 / 組織導入 | [ai-use-risk-classification](skills/ai-use-risk-classification/) | 1.2.0 |
| 会議運営 | [committee-meeting-minutes-ai](skills/committee-meeting-minutes-ai/) | 1.2.0 |
| 文書確認 | [ai-tone-check](skills/ai-tone-check/) | 1.2.0 |
| 組織導入・研修 | [institutional-ai-adoption-checklist](skills/institutional-ai-adoption-checklist/) | 1.2.0 |
| 組織導入・研修 | [staff-ai-literacy-primer](skills/staff-ai-literacy-primer/) | 1.2.0 |
| Skill 作成・保守 | [create-action-skill](skills/create-action-skill/) | 1.1.0 |
| 教務・教学 | [syllabus-ai-policy](domain-skills/academic-affairs/syllabus-ai-policy/) | 1.3.0 |
| 入試 | [entrance-exam-ai-policy](domain-skills/academic-affairs/entrance-exam-ai-policy/) | 1.2.0 |
| 学生対応 | [student-inquiry-triage](domain-skills/student-support/student-inquiry-triage/) | 1.2.0 |
| 国際 | [multilingual-student-communication](domain-skills/international-office/multilingual-student-communication/) | 1.2.0 |
| 研究支援 | [research-integrity-ai-disclosure](domain-skills/research-support/research-integrity-ai-disclosure/) | 1.3.0 |
| IR・内部質保証 | [ir-freeform-text-analysis](domain-skills/ir-analysis/ir-freeform-text-analysis/) | 1.2.0 |
| 広報・文書 | [pr-ai-checklist](domain-skills/public-relations/pr-ai-checklist/) | 1.2.0 |

準備中・非推奨 skill は [docs/roadmap.md](docs/roadmap.md) と [deprecated/](deprecated/) に移しています。

## 導入

詳しい導入手順は [docs/install.md](docs/install.md)、AI エージェントへの頼み方は [docs/using-with-agent.md](docs/using-with-agent.md) を参照してください。

Claude Code で個別 skill を入れる例:

```bash
git clone https://github.com/gmoriki/higher-ed-ai-skills.git
mkdir -p ~/.claude/skills/
cp -R higher-ed-ai-skills/skills/check-info-level \
  ~/.claude/skills/higher-ed-check-info-level
```

導入後は、実データではなく架空の資料カテゴリで動作確認してください。

## 安全と限界

- 所属大学の規程、情報セキュリティポリシー、個人情報保護規程、AI 利用ガイドラインが常に優先されます。
- 本リポジトリは法的助言ではありません。
- 学生個人情報、成績、相談記録、人事、入試、未公表研究データは、本文やファイルを渡す前に入力可否を確認してください。
- 外部 AI サービスにファイルをアップロードする前に、契約形態、学習利用、保存期間、削除手順を確認してください。

## 関連ドキュメント

- [docs/install.md](docs/install.md) — インストール手順
- [docs/using-with-agent.md](docs/using-with-agent.md) — AI エージェントへの頼み方
- [docs/manual-reading.md](docs/manual-reading.md) — GitHub 上で直接読む場合
- [docs/update-policy.md](docs/update-policy.md) — 鮮度管理とバージョニング
- [docs/roadmap.md](docs/roadmap.md) — 次に整備する領域
- [runtime-adapters/claude-code.md](runtime-adapters/claude-code.md) — Claude Code 向け詳細
- [AGENTS.md](AGENTS.md) — 設計思想と AI コントリビューター向けガイド
- [references/skill-format-guide.md](references/skill-format-guide.md) — skill 作成・改修の標準
- [CONTRIBUTING.md](CONTRIBUTING.md) — 貢献ガイド
- [CHANGELOG.md](CHANGELOG.md) — 変更履歴

## ライセンス

本リポジトリのコンテンツは [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) で公開しています。改変して再配布する場合も同じライセンスで共有してください。

## 著者

森木銀河 (Ginga Moriki)

大学職員研修、ガイドライン策定支援、AI 導入アドバイザリーを提供しています。

- [gmoriki.com](https://gmoriki.com)
- [note](https://note.com/pogohopper8)
- [GitHub](https://github.com/gmoriki)
