# 例3: 国際誌投稿時の AI 開示テンプレート選択

## 状況

医学系研究室の URA（リサーチ・アドミニストレーター）。臨床研究の論文を海外査読誌への投稿準備中で、筆頭著者の准教授から「Nature Medicine、Lancet、BMC Medicine、Cell Reports Medicine に順次投稿する予定だが、AI 開示のフォーマットが違うようで混乱している」との相談。

研究チームの AI 利用状況:
- 統計解析コードの補助生成: ChatGPT で R コードの雛形生成（出力は自分で検証・修正）
- 英文校正: Paperpal で文法・表現チェック
- 図表作成: 図表そのものは研究者作成、キャプション英訳に DeepL
- 先行研究整理: ChatGPT で関連論文の要約を参考（原典確認済）

投稿先 4 誌それぞれで開示要件が微妙に異なり、「汎用の開示文を使い回していいか、毎回書き直すべきか」で判断に迷っている。

## 判断

**投稿先ごとに開示フォーマットを個別作成**。汎用テンプレートの使い回しは不可。各誌のポリシーを最新版で確認し、指定書式に従うこと。

具体方針:
1. 投稿前に各誌の AI ポリシーページを必ず最新確認（半期ごとに更新される）
2. 開示位置（Methods / Acknowledgments / 専用セクション）が誌ごとに異なるため要確認
3. 共著者全員で利用状況を共有し、漏れなく開示
4. 査読過程で追加 AI 利用があれば、再投稿時に追記

## 判断の理由

主要出版社の AI ポリシーは一見似ているが、細部で差異がある。本スキルの `references/journal-policy-overview.md` にある通り、Nature 系は「LLM を著者にできない」「Methods での開示」が原則、Elsevier は「原稿末尾に専用セクション（Declaration of Generative AI）」を設ける、BMC は投稿システム上でチェックボックス方式、Cell Press は Methods 内で詳細記載、という具合にフォーマット・位置が異なる。

「汎用テンプレートの使い回し」は、出版社ポリシー違反を招きやすく、査読差戻しの原因にもなる。本スキル §4.5 の検証プロトコルに沿って使用記録を保持し、投稿時に各誌要件に合わせてフォーマット調整する方が効率的。

共著者合意も重要で、Nature 系・BMC は「すべての著者が AI 使用を把握している」ことを暗黙に要求。共著者の一人が個別に AI を使い、筆頭著者が知らないまま投稿すると、後から問題化しうる。

## 具体的な対応手順

1. **投稿先ポリシー確認**:
   - Nature Medicine: https://www.nature.com/nature-portfolio/editorial-policies/ai
   - Lancet (Elsevier): https://www.elsevier.com/about/policies-and-standards/publishing-ethics
   - BMC Medicine: https://www.biomedcentral.com/getpublished/editorial-policies
   - Cell Reports Medicine: https://www.cell.com/cell-reports-medicine/authors
2. **開示箇所の特定**: 各誌で Methods / Acknowledgments / 専用セクション / 投稿画面チェックボックスのどれか
3. **記載文の作成**（Elsevier 系の例）:
   ```
   Declaration of generative AI and AI-assisted technologies in the writing process
   During the preparation of this work, the authors used ChatGPT (GPT-X.X)
   for drafting R code templates for statistical analysis, Paperpal for
   English language editing, and DeepL for translating figure captions.
   After using these tools, the authors reviewed and edited the content
   as needed and take full responsibility for the content of the publication.
   ```
4. **共著者合意形成**: 共著者全員に利用状況・開示文面を共有し、メール等で承諾取得
5. **投稿実行**: 投稿画面のチェックボックス／記載欄に従って開示内容を入力
6. **使用記録の保管**: プロンプト・出力・検証結果を 5 年以上保管（本スキル §4.5 準拠）

## 注意点

- **査読過程での追加 AI 使用**: 査読対応で新たに AI を使った場合、再投稿時に追記。「査読過程でも使用した」旨を Response letter で開示
- **再投稿時の履歴**: 投稿 → 差戻し → 再投稿の流れで AI 利用に変化があれば、差分を明示
- **Nature の「non-human author 明示不可」原則**: AI を著者欄・謝辞の著者列挙に入れることは全面禁止。使用の開示のみ
- **医学系特有の注意**: 患者データ（匿名化済でも）・未公表の臨床試験結果を Web 版 AI に入力しない。Enterprise 版・院内オンプレ環境を検討
- **日本語ジャーナルとの違い**: 日本語系の医学会誌でも AI 開示要件が追加されつつあるため、国内投稿時も要確認
- 関連スキル: `confidential-info-guidelines`（患者データ等の機密扱い）、`ai-use-risk-classification`（研究データのリスク区分）

## 所属大学のガイドライン優先

所属大学の研究倫理規程・医学部独自ルール・資金提供元（AMED・JSPS 等）の要件が常に優先される。投稿ジャーナルのポリシーと大学規程で要件が異なる場合、より厳しい方に合わせるのが安全。判断に迷う場合は大学の研究倫理委員会・医学系研究倫理審査委員会に相談する。
