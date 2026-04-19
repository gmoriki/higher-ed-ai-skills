# ai-report-evaluation（非推奨）

> **このスキルは 2026-04-19 v0.4.0 で非推奨となりました。**
> 代替（2 件に分担）: [domain-skills/research-support/research-integrity-ai-disclosure](../../domain-skills/research-support/research-integrity-ai-disclosure/) / [domain-skills/academic-affairs/syllabus-ai-policy](../../domain-skills/academic-affairs/syllabus-ai-policy/)

## 非推奨の理由

「AI 生成レポートの評価」を単独スキルにする初期構想は、v0.3.0 までの検証の結果、守備範囲が広すぎて実務上の判断軸を一本化できないことが分かりました。

大学現場で「AI が使われたレポートをどう評価するか」という問いは、研究系（論文・学位論文・科研費報告書）と教学系（授業課題・レポート・卒業研究）で、求められる評価軸がまったく異なります。前者は **研究公正と開示義務** が中心で、著者性・再現性・剽窃検知との関係を扱う必要があります。後者は **学習目標との整合と授業運営** が中心で、到達目標に対して AI 使用を許容するかという教育方針と、シラバスでの事前開示の問題になります。

この 2 つを単一スキルに押し込めると、判断フローが肥大化し、しかも「どちらの文脈か」を冒頭で分岐させるだけの中身の薄い構造になってしまいます。そこで v0.3.0 のリリースに合わせ、2 つの領域別スキルに機能を分担する方針へ切り替えました。

## 代替スキル

- **[domain-skills/research-support/research-integrity-ai-disclosure](../../domain-skills/research-support/research-integrity-ai-disclosure/)** — 論文・学位論文・科研費における AI 使用の開示判断と、研究公正の観点からの評価軸を提供します。
- **[domain-skills/academic-affairs/syllabus-ai-policy](../../domain-skills/academic-affairs/syllabus-ai-policy/)** — シラバスで AI 使用方針を 4 段階で宣言するテンプレート。授業課題レポートの評価は、この方針と連動して行います。

## 履歴

- **2026-04-15 (v0.1.0)** — README の「準備中」一覧に計上。
- **2026-04-19 (v0.3.0)** — `research-integrity-ai-disclosure` と `syllabus-ai-policy` が機能の一部を吸収。独立スキル化は v0.4 で再評価すると予告。
- **2026-04-19 (v0.4.0)** — 領域別 2 スキルへの分担が妥当と結論し、本ディレクトリへ非推奨化。

## 参照

- [CHANGELOG.md](../../CHANGELOG.md)
- [DESIGN.md §5.4 deprecated/ への移動](../../DESIGN.md#54-deprecated-への移動)
