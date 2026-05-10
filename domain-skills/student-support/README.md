# 学生支援 / Student Support

学生問い合わせ、奨学金、証明書、合理的配慮、メンタル不調、ハラスメント相談など、学生に不利益が生じやすい業務を扱います。AI に自動回答させることよりも、公開情報に基づく定型回答と有人対応の境界を明確にすることを優先します。

## 実装済み skill

| Skill | 使う場面 | 先に確認すること |
|---|---|---|
| [student-inquiry-triage](student-inquiry-triage/) | 学生問い合わせを AI 一次応答と有人対応に振り分ける | 学生 PII、緊急性、個別判断の有無 |

## 関連 skill

- [multilingual-student-communication](../international-office/multilingual-student-communication/) — 留学生向け案内の多言語化。
- [ai-tone-check](../../skills/ai-tone-check/) — 学生向け文面の読みやすさ確認。
- [check-info-level](../../skills/check-info-level/) — 学生情報を含む可能性がある資料の入力前確認。

## 今後の候補

- 奨学金 FAQ の運用設計
- 合理的配慮申請の案内文レビュー
- 相談記録の匿名化・傾向整理

[README.md](../../README.md) に戻る。
