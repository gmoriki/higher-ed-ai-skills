# higher-ed-ai-skills

大学業務のAI活用を skill.md 形式で構造化した公開スキル集。

[English](README.en.md)

---

## これは何か

日本の大学業務と生成AIのあいだには、しばしば翻訳が必要になります。

大学には文書化されていない暗黙知が多く存在します。

- 稟議の通し方
- 学年暦の例外処理
- 教員と職員の権限分離
- 委員会の議事運営

こうした知識は、そのままでは AI のプロンプトに乗りません。

本リポジトリは、大学現場で積み上げた判断フレームワークを skill.md 形式で公開するものです。誰でも再利用できる形に整えてあります。

v0.5 から、スキルは **Reference layer**（判断フレームワーク文書、AI が読んで人間に判断材料を返す）と **Task layer**（AI が手順を実行して成果物を返す Action skill、スラッシュコマンドで起動）の二層構造になっています。Anthropic 公式 Claude Code Skills の Reference content / Task content 二類型に整合します。

---

## 今使えるスキル

### 横断スキル（skills/）

| スキル | 説明 | Version |
|---|---|---|
| [confidential-info-guidelines](skills/confidential-info-guidelines/) | 生成AIに機密情報を入力してよいかを3レベル分類で判断する | 1.2.0 |
| [ai-use-risk-classification](skills/ai-use-risk-classification/) | AI 利用を「禁止／限定／推奨／開放」の 4 区分で判定する | 1.0.0 |
| [staff-ai-literacy-primer](skills/staff-ai-literacy-primer/) | 新任職員向け AI リテラシー入門、SD 研修コア | 1.0.0 |
| [institutional-ai-adoption-checklist](skills/institutional-ai-adoption-checklist/) | 組織としての AI 導入検討チェックリストと成熟度モデル | 1.0.0 |
| [committee-meeting-minutes-ai](skills/committee-meeting-minutes-ai/) | 委員会・教授会議事録の AI 活用判断とツール選定 | 1.0.0 |

### 業務領域別スキル（domain-skills/）

| 領域 | スキル | 説明 |
|---|---|---|
| [academic-affairs](domain-skills/academic-affairs/) | [syllabus-ai-policy](domain-skills/academic-affairs/syllabus-ai-policy/) | シラバス AI 方針の 4 段階テンプレート |
| academic-affairs | [entrance-exam-ai-policy](domain-skills/academic-affairs/entrance-exam-ai-policy/) | 入試書類の AI 使用可否と検知対応 |
| [international-office](domain-skills/international-office/) | [multilingual-student-communication](domain-skills/international-office/multilingual-student-communication/) | 留学生向け多言語化の判断と運用 |
| [ir-analysis](domain-skills/ir-analysis/) | [ir-freeform-text-analysis](domain-skills/ir-analysis/ir-freeform-text-analysis/) | 学生調査の自由記述 AI 分析ワークフロー |
| [public-relations](domain-skills/public-relations/) | [pr-ai-checklist](domain-skills/public-relations/pr-ai-checklist/) | 広報原稿 AI 利用 7 点チェック |
| [research-support](domain-skills/research-support/) | [research-integrity-ai-disclosure](domain-skills/research-support/research-integrity-ai-disclosure/) | 論文・学位論文・科研費の AI 開示判断 |
| [student-support](domain-skills/student-support/) | [student-inquiry-triage](domain-skills/student-support/student-inquiry-triage/) | 学生問い合わせの AI／有人対応振り分け |

### Task layer スキル（v0.5 新規）

AI が手順を実行して成果物を返す Action skill。スラッシュコマンド `/skill-name` で起動できる。

| スキル | コマンド | 説明 |
|---|---|---|
| [check-info-level](skills/check-info-level/) | `/check-info-level [text or file]` | 渡されたテキスト / ファイルを Level 1/2/3 判定し、AI 入力可否と推奨次アクションを返す |
| [create-action-skill](skills/create-action-skill/) | `/create-action-skill` | 自分の暗黙知を対話ヒアリングで SKILL.md（Reference / Task）に変換するメタスキル |

### 準備中

| スキル | 備考 | 目標 |
|---|---|---|
| ai-news-curation | 情報源キュレーション | v0.5+ |
| case-library-ai-usage | `case-studies/` ディレクトリの充実で代替 | v0.5+ |

※ v0.3 で準備中だった `advanced-prompting-for-admin` / `ai-report-evaluation` / `tool-selection-guide` の 3 枠は v0.4 で非推奨化しました。詳細は下の「非推奨スキル」と [`deprecated/`](deprecated/) を参照。

### 非推奨スキル（deprecated/）

機能が既存スキルに吸収されたため非推奨となった枠を [`deprecated/`](deprecated/) に保存しています。

| 非推奨スキル | 代替スキル |
|---|---|
| [advanced-prompting-for-admin](deprecated/advanced-prompting-for-admin/) | [staff-ai-literacy-primer](skills/staff-ai-literacy-primer/) |
| [ai-report-evaluation](deprecated/ai-report-evaluation/) | [research-integrity-ai-disclosure](domain-skills/research-support/research-integrity-ai-disclosure/) + [syllabus-ai-policy](domain-skills/academic-affairs/syllabus-ai-policy/) |
| [tool-selection-guide](deprecated/tool-selection-guide/) | [institutional-ai-adoption-checklist](skills/institutional-ai-adoption-checklist/) |

---

## 読者別の最短ルート

| あなたが | 最初に開くべき |
|---|---|
| 大学職員で、実務で使いたい | [confidential-info-guidelines](skills/confidential-info-guidelines/SKILL.md) |
| 導入検討委員会の資料を作りたい | [institutional-ai-adoption-checklist](skills/institutional-ai-adoption-checklist/SKILL.md) |
| 新任 SD 研修を組みたい | [staff-ai-literacy-primer](skills/staff-ai-literacy-primer/SKILL.md) |
| コンサルタントや研究者 | [DESIGN.md](DESIGN.md) |
| 英語で読みたい | [README.en.md](README.en.md) |
| GitHub に慣れていない | [docs/how-to-use.md](docs/how-to-use.md) |

---

## 使い方

主な使い方は4つあります。

1. **そのまま読む**（Reference layer 向け） — SKILL.md を開き、判断フローに沿って業務判断に使う
2. **AIアシスタントに読ませる**（Reference layer 向け） — Claude、ChatGPT、Microsoft Copilot などの指示文やナレッジに貼り付ける
3. **スラッシュコマンドで起動する**（Task layer 向け） — Claude Code に組み込み、`/check-info-level <path>` のように直接呼び出して成果物を得る
4. **研修教材にする** — CC BY-SA 4.0 の範囲で改変・再配布できる

詳しい手順は [docs/how-to-use.md](docs/how-to-use.md) を参照してください。GitHub アカウントがなくても利用できます。

---

## Runtime Adapters

AI ランタイムごとの組み込み方法を [`runtime-adapters/`](runtime-adapters/) にまとめています。Claude Code 向けの初弾を v0.4 で追加しました。

| ランタイム | ガイド | 状態 |
|---|---|---|
| Claude Code | [claude-code.md](runtime-adapters/claude-code.md) | v0.4 初弾 |
| ChatGPT (Custom GPT) | — | v0.5+ 予定 |
| Microsoft Copilot | — | v0.5+ 予定 |
| GitHub Copilot | — | v0.5+ 予定 |
| ローカル LLM | — | v0.5+ 予定 |

---

## ライセンスと免責

本リポジトリのコンテンツはすべて [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) の下で自由に使えます。改変して再配布する場合は、同じライセンスで共有してください。

本リポジトリは情報提供を目的としたものであり、法的助言ではありません。実際の業務判断は、所属大学の規程および担当部署の指示に従ってください。

---

## 関連ドキュメント

- [DESIGN.md](DESIGN.md) — 設計思想と6原則
- [CONTRIBUTING.md](CONTRIBUTING.md) — 貢献ガイド
- [CHANGELOG.md](CHANGELOG.md) — 変更履歴
- [docs/update-policy.md](docs/update-policy.md) — スキルの更新ポリシー

---

## 著者

森木銀河 (Ginga Moriki)

大学職員研修、ガイドライン策定支援、AI導入アドバイザリーを提供しています。

本リポジトリのコンテンツは無料で使えます。大学固有の稟議フローへの適用や研修プログラムは、別途有料で提供しています。

- [gmoriki.com](https://gmoriki.com)
- [note](https://note.com/pogohopper8)
- [GitHub](https://github.com/gmoriki)
