# higher-ed-ai-skills

大学業務のAI活用を skill.md 形式で構造化した公開スキル集
Open-source AI skills for higher education administration, structured as skill.md files

*English version: [README.en.md](README.en.md)*

---

## What is this? / これは何か

日本の大学業務と生成AIの間には、しばしば「翻訳」が必要になる。大学の暗黙知（稟議の通し方、学年暦の例外処理、教職員の権限分離）は文書化されておらず、そのままでは AI のプロンプトに乗らない。本リポジトリは、森木銀河（Ginga Moriki）が大学×AI の現場で蓄積してきた判断フレームワークを skill.md 形式で公開し、誰でも再利用できる形に整えたものです。

**著者 / Author:** 森木銀河（Ginga Moriki）。大学職員研修、ガイドライン策定支援、AI 導入のアドバイザリーを提供。詳細は [gmoriki.com](https://gmoriki.com) / [note](https://note.com/pogohopper8)。

**公開版の位置づけ:** このリポジトリの**すべてのコンテンツは [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) の下で自由に使えます**。原則論・判断フレームワーク・設計思想はそのまま実務で使える水準で書いています。大学固有の稟議フローへの適用や研修プログラム提供は、別途有料アドバイザリーとして [gmoriki.com](https://gmoriki.com) で提供しています。

### 読者別の最短ルート / Where to start

| 読者 / Reader | まずここから / Start here |
|---|---|
| 大学職員（実務で使いたい） | → [今使えるスキル](#available-skills--今使えるスキル) の `confidential-info-guidelines` |
| コンサルタント・研究者 | → [DESIGN.md](DESIGN.md)（設計思想と5原則） |
| Global higher ed admins | → [README.en.md](README.en.md) |
| GitHub アカウントがない | → [docs/how-to-use.md](docs/how-to-use.md) の冒頭 |

---

## Available Skills / 今使えるスキル

### Ready to use / 実装済み

| スキル | 一行説明 | 想定読者 | バージョン | リンク |
|---|---|---|---|---|
| **confidential-info-guidelines** | 生成AIに機密情報を入力してよいかを3レベル分類で判断 | 大学職員全般 | v1.1.0 | [SKILL.md](skills/confidential-info-guidelines/SKILL.md) / [examples/](skills/confidential-info-guidelines/examples/) |

### Coming soon / 準備中

| スキル | 一行説明 | 目標バージョン |
|---|---|---|
| ai-report-evaluation | AI 生成レポートの評価基準と検証手順 | v0.3 |
| tool-selection-guide | 大学業務向け AI ツールの選定チェックリスト | v0.3 |
| advanced-prompting-for-admin | 大学事務向けの応用プロンプト集 | v0.4 |
| ai-news-curation | 大学×AI 領域の情報収集・キュレーション手法 | v0.4 |
| case-library-ai-usage | 他大学の AI 活用事例ライブラリ | v0.5 |

### Domain skills / 業務領域別スキル（準備中）

[`domain-skills/`](domain-skills/) 配下に、業務領域ごとのディレクトリを用意しています（v0.3 以降に順次公開）:
[academic-affairs](domain-skills/academic-affairs/) / [international-office](domain-skills/international-office/) / [ir-analysis](domain-skills/ir-analysis/) / [public-relations](domain-skills/public-relations/) / [research-support](domain-skills/research-support/) / [student-support](domain-skills/student-support/)

---

## How to use / 使い方

1. **そのまま読む** — [SKILL.md](skills/confidential-info-guidelines/SKILL.md) を開き、判断フローに沿って業務判断に使う
2. **AI アシスタントに読ませる** — Claude / ChatGPT / Microsoft Copilot の指示文やナレッジとして貼り付ける
3. **研修教材にする** — CC BY-SA 4.0 の範囲で自由に改変・再配布できる（改変時は同ライセンスで共有）

詳細は **[docs/how-to-use.md](docs/how-to-use.md)**（GitHub アカウントがなくても使えます）。Claude Code / Custom GPT / Copilot Agent への変換ガイドは [`runtime-adapters/`](runtime-adapters/)（v0.3 以降）に追加予定。

---

## About / 著者・ライセンス・貢献

**コンタクト:** [gmoriki.com](https://gmoriki.com) | [note](https://note.com/pogohopper8) | [@gmoriki](https://github.com/gmoriki)

**免責 / Disclaimer:** 本リポジトリのコンテンツは情報提供を目的としたものであり、法的助言ではありません。個人情報保護法や各大学の規程が優先します。実際の業務判断は所属大学の規程および担当部署の指示に従ってください。

**ライセンス:** [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) — 詳細は [LICENSE](LICENSE)

**関連ドキュメント:** [DESIGN.md](DESIGN.md)（設計思想） / [CONTRIBUTING.md](CONTRIBUTING.md)（貢献ガイド） / [CHANGELOG.md](CHANGELOG.md)（変更履歴） / [docs/update-policy.md](docs/update-policy.md)（更新ポリシー）
