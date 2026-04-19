# skill.md の使い方ガイド / How to Use skill.md

## GitHubアカウント不要で使う方法 / No GitHub account needed

このリポジトリのスキルは、GitHubアカウントがなくても利用できます。

**ブラウザで直接読む:**
1. 使いたいスキルのページ（例: [SKILL.md](https://github.com/gmoriki/higher-ed-ai-skills/blob/main/skills/confidential-info-guidelines/SKILL.md)）をブラウザで開く
2. ページ右上の「Raw」ボタンを押すと、プレーンテキストとしてコピー可能
3. コピーしたテキストを ChatGPT、Claude、Microsoft Copilot などに貼り付けて使う

**ダウンロードして使う:**
- リポジトリトップの緑色の「Code」ボタン → 「Download ZIP」で全ファイルをダウンロード
- ZIPを展開すれば、オフラインでも参照可能

**もしGitHubの操作に迷ったら:**
最も確実な方法は、SKILL.md の内容をそのまま AIアシスタント（Claude、ChatGPT等）のチャット欄に貼り付けて、「このフレームワークを使って、〇〇について判断して」と質問することです。

## skill.md とは

skill.md は、大学業務におけるAI活用の知見を**構造化された1ファイル**に凝縮したフォーマットです。各スキルは以下の3層構造で構成されています。

### 3層構造

1. **description（概要）** -- YAMLフロントマターによるメタデータ。スキルの目的、対象業務、バージョン、最終更新日を記述します。何のスキルか、誰が使うかが一目でわかります。
2. **本体（判断フレームワーク・手順・プロンプト）** -- スキルの中核。判断フロー、意思決定の基準、具体的な手順、AIへのプロンプト例などを含みます。人間が読んでもAIに読ませても機能するように記述されています。
3. **references（参考情報）** -- 根拠となる外部資料、データ比較表、関連法規へのリンクなど。スキルの判断ロジックを裏付ける補助情報です。`references/` ディレクトリに別ファイルとして格納されます。

---

## 使い方の3パターン

### パターンA: そのまま読む

最もシンプルな使い方です。SKILL.md を判断フレームワークとして人間が直接参照します。

**想定シーン:**
- AIサービスに学生データを入力してよいか迷ったとき
- AIで作成したレポートの品質をどう評価するか基準が欲しいとき
- AIツールの選定で検討項目を洗い出したいとき

**使い方:**
1. `skills/` または `domain-skills/` から該当するスキルのディレクトリを開く
2. `SKILL.md` を読み、判断フローやチェックリストに沿って業務を進める
3. 必要に応じて `references/` の補助資料も参照する

### パターンB: AIランタイムに組み込む

SKILL.md をAIアシスタントのシステムプロンプトやナレッジとして読み込ませ、AIの判断基盤として活用します。

**想定シーン:**
- Claude Code のカスタムスキルとして常時参照させたい
- Custom GPT の知識ベースに組み込みたい
- Copilot Agent のインストラクションに設定したい

**具体的な設定方法は後述の「Claude Code で使う場合」「Custom GPT で使う場合」を参照してください。**

### パターンC: 研修教材に組み込む

SKILL.md を研修コンテンツの素材として再利用します。CC BY-SA 4.0 ライセンスに基づき、クレジット表記と同一ライセンスでの共有を条件に、自由に改変・再配布できます。

**想定シーン:**
- 学内のAI活用研修でケーススタディの教材にしたい
- FD/SD研修のワークショップ素材として使いたい
- 他大学向けの勉強会で判断フレームワークを紹介したい

**使い方:**
1. SKILL.md の判断フローやチェックリストを研修スライドに転記
2. `examples/` のサンプルケースを演習問題として活用
3. 自学の文脈に合わせて事例を差し替え、独自の教材として配布

**ライセンス上の注意:**
- クレジット表記（出典: higher-ed-ai-skills / 森木銀河）を明記してください
- 改変した場合、CC BY-SA 4.0 で共有してください

---

## Claude Code で使う場合

Claude Code のスキル機能を使い、SKILL.md をカスタムスキルとして登録できます。

### 手順

1. スキルファイルをローカルにコピーする

```bash
# 例: 機密情報取り扱いスキルを登録する場合
mkdir -p ~/.claude/skills/
cp skills/confidential-info-guidelines/SKILL.md ~/.claude/skills/confidential-info-guidelines.md
```

2. Claude Code がスキルを自動検出する

`~/.claude/skills/` ディレクトリに配置された `.md` ファイルは、Claude Code のスキルとして自動的に認識されます。

3. 利用時にスキルを呼び出す

Claude Code のセッション内で、スキルに関連する質問をすると自動的にスキルが参照されます。

### プロジェクト単位で使う場合

特定のプロジェクトだけにスキルを適用したい場合は、プロジェクトルートの `.claude/skills/` に配置します。

```bash
mkdir -p /path/to/your-project/.claude/skills/
cp skills/confidential-info-guidelines/SKILL.md /path/to/your-project/.claude/skills/confidential-info-guidelines.md
```

---

## Custom GPT で使う場合

OpenAI の Custom GPT にスキルを組み込むことも可能です。

### 概要

1. Custom GPT の作成画面で「Instructions」にSKILL.md の内容を貼り付ける
2. または「Knowledge」にSKILL.md をアップロードする
3. 必要に応じて `references/` の資料もアップロードする

詳細な手順やアダプタの設定方法は `runtime-adapters/` ディレクトリを参照してください。

---

## フィードバックの方法

スキルに対するフィードバック（誤りの指摘、改善提案、新規スキルのリクエスト等）は、GitHub Issue で受け付けています。

- **バグ報告・誤りの指摘**: 該当するスキルのパスと具体的な問題点を記載してください
- **改善提案**: 現状の課題と提案内容を記載してください
- **新規スキルのリクエスト**: 対象業務、想定される利用シーン、既存のスキルとの関係を記載してください

Issue URL: <https://github.com/gmoriki/higher-ed-ai-skills/issues>

Pull Request による直接の貢献も歓迎します。詳細は [CONTRIBUTING.md](../CONTRIBUTING.md) を参照してください。
