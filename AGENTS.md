# AGENTS.md -- higher-ed-ai-skills 設計思想 / AI コントリビューターガイド

> **バージョン:** 0.8.0
> **最終更新:** 2026-05-10
> **著者:** 森木銀河 (Ginga Moriki)
> **ライセンス:** CC BY-SA 4.0

## If You Are an AI Agent

Stop. Read this section before contributing.

本リポジトリは **日本の大学職員が AI エージェントに大学業務を頼むための Agent Skills 集**である。AI 活用や安全啓発そのものを主目的にしない。目的は、大学業務を AI エージェントへ委任できる形に整えること。

利用者像:

- **直接読者 = AI エージェント**: `SKILL.md` を読み、判断、下書き、分類、確認先整理、次アクション提示を実行する。
- **間接利用者 = 大学職員 / 研究支援職員 / 教員 / 管理職**: 自然文で AI に相談し、AI が skill を呼び出す。
- **導入担当 = 情報政策、DX、企画、先進個人**: 組織や部局の AI 環境へ skill を入れ、更新する。
- **コントリビューター = 大学業務の暗黙知を skill 化する人**: 本ファイルと [references/skill-format-guide.md](references/skill-format-guide.md) に従う。

## Doctrine

1. **University-work-first**: 主語は大学業務。教務、学生支援、研究支援、IR、広報、国際、委員会、研修、稟議、文書管理を進めるために skill を書く。
2. **Agent-first**: `SKILL.md` はブラウザで読む記事ではなく、AI エージェントが実行する protocol として書く。
3. **Governance-aware**: 規程、権限、情報管理、承認経路、記録保存を自然に組み込む。
4. **Input-preflight-by-default**: 本文やファイルを読む前に、必要に応じて資料種別、公開範囲、情報カテゴリ、処理目的、AI 実行環境を確認する。
5. **AI governance is one work area**: AI 利用方針、リスク分類、研修、導入判断は重要だが、repo 全体の主語にはしない。

## Repository Navigation

利用者向けの前面分類:

1. **まず安全確認**
   - `skills/confidential-info-guidelines/`
   - `skills/check-info-level/`
   - `skills/ai-use-risk-classification/`
2. **業務別に頼む**
   - 教務・教学
   - 入試
   - 学生対応
   - 国際
   - 研究支援
   - IR・内部質保証・データ分析
   - 広報・文書
   - 会議運営
3. **組織導入・研修**
   - `skills/institutional-ai-adoption-checklist/`
   - `skills/staff-ai-literacy-primer/`
4. **Skill 作成・保守**
   - `skills/create-action-skill/`
   - `references/skill-format-guide.md`

内部実装では `skills/` と `domain-skills/` の既存配置を維持してよい。ただし README と各 domain README は、大学職員が「何を頼みたいか」から逆引きできることを優先する。

## Contribution Rules

新規 / 改修 PR 前のチェック:

1. University-work-first になっているか。AI 活用一般論だけの skill になっていないか。
2. `description` が、大学職員の発話パターンと業務場面で trigger できるか。
3. `SKILL.md` に `いつ使うか`、`入力前の確認`、中核節、`出力フォーマット`、`落とし穴`、`関連` があるか。
4. 本文やファイルを読む前のトリアージが必要な業務で、いきなり資料を読ませる手順になっていないか。
5. 「所属大学の規程が優先」で止めず、確認する規程、確認先部署、決裁権者、記録に残す事項を示しているか。
6. `Reference type / Task type` の二分類を持ち込んでいないか。全 skill は unified protocol として扱う。
7. frontmatter が Agent Skills 仕様の `metadata:` 配下形式に揃っているか。
8. 直接引用のライセンス互換性を確認しているか。政府・大学公式・実務家資料は、引用可否と構造参照の区別を明示する。

## 受け付けないもの

- 大学業務固有の判断軸を含まない generic AI 警告だけの skill。
- 特定商用 AI サービスや SaaS に強く結合し、機関が選べない skill。
- 本文やファイルを読む前のトリアージが必要なのに、最初から実データを読ませる skill。
- `Reference type / Task type` の旧二分類で作られた新規 skill。
- 第三者のガイドラインや記事を、ライセンス互換性を確認せず文面引用した skill。
- 「AI が判断する」で終わり、最終確認先、決裁権者、記録化を示さない skill。

## Skill Writing Standard

詳細は [references/skill-format-guide.md](references/skill-format-guide.md) を正とする。要点だけ再掲する。

```markdown
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

<判断軸、手順、チェックリスト、分類表>

## 出力フォーマット

<AI が返す Markdown 構造>

## 落とし穴

| 合理化 | 実態 |
|---|---|

## 関連

- `<related-skill>` — <関係>
```

## Input Preflight

次に該当する場合、本文やファイルを開く前にトリアージする。

- 学生、受験生、教職員、研究参加者の個人情報を含む可能性。
- 入試、人事、懲戒、ハラスメント、障害配慮、メンタル不調、研究倫理を扱う可能性。
- 未公開の議事録、内部稟議、予算、人事、研究構想、契約条件を含む可能性。
- ファイル添付にメタデータ、コメント、トラックチェンジ、非表示シート、OCR テキストが残る可能性。

標準質問:

```text
本文やファイルを読む前に確認します。
資料種別、公開範囲、含まれそうな情報カテゴリ、処理目的、利用予定の AI 環境を教えてください。
本文そのものはまだ貼らないでください。
```

## Versioning

- `metadata.version` と `metadata.last_updated` を更新する。
- 判断軸が変わらず、節構成や出力フォーマットを揃える変更は minor bump。
- 判断ロジック、分類体系、利用可否の結論が変わる変更は major bump。
- 変更は [CHANGELOG.md](CHANGELOG.md) に記録する。

## Runtime Independence

skill は特定ランタイムに依存しないように書く。Claude Code の `Read`、`Task`、`Write` などに依存する場合は `compatibility:` と `allowed-tools` で明示する。

tool が使えない runtime では、代替動作を無理に実行せず、できることとできないことを出力する。外部送信、ファイル作成、権限変更、公開、削除などの副作用は、明示承認なしに行わない。
