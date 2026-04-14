# higher-ed-ai-skills

大学業務のAI活用をskill.md形式で構造化した公開スキル集
Open-source AI skills for higher education administration, structured as skill.md files

**English version: [README.en.md](README.en.md)**

---

## Who is this for? / 対象読者

- **大学職員・経営層・IT部門** -- AI導入の判断材料や運用指針を探している方
- **コンサルタント・研究者** -- 大学業務へのAI活用を分析・提案する方
- **Higher Ed Administrators (global)** -- practitioners seeking structured AI adoption frameworks

---

## Open vs. Premium / 公開版と有料版の関係

このリポジトリは、森木銀河が大学×AI領域で蓄積しているスキル群の**公開版**です。原則論・判断フレームワーク・設計思想はそのまま使えます。大学固有の意思決定構造や具体的な稟議への落とし込みが必要な場合、森木の個別相談・アドバイザリーが有料で利用可能です。

---

## Design Philosophy / 設計思想

スキルの設計原則は [DESIGN.md](DESIGN.md) を参照してください。

---

## Getting Started / 最初に読むべきスキル

1. **[confidential-info-guidelines](skills/confidential-info-guidelines/)** -- 機密情報取り扱い判断フレームワーク / Confidential information handling framework
2. **[ai-report-evaluation](skills/ai-report-evaluation/)** -- AIレポート評価ガイドライン / AI report evaluation guidelines (Coming Soon)
3. **[tool-selection-guide](skills/tool-selection-guide/)** -- AIツール選定ガイド / AI tool selection guide (Coming Soon)

---

## Repository Structure / ディレクトリ構造

```
higher-ed-ai-skills/
├── skills/                      # 汎用スキル（業務横断）
│   ├── confidential-info-guidelines/
│   ├── ai-report-evaluation/
│   ├── ai-news-curation/
│   ├── advanced-prompting-for-admin/
│   ├── case-library-ai-usage/
│   └── tool-selection-guide/
├── domain-skills/               # 部署別スキル
│   ├── academic-affairs/
│   ├── international-office/
│   ├── ir-analysis/
│   ├── public-relations/
│   ├── research-support/
│   └── student-support/
├── runtime-adapters/            # AI環境別の実行アダプタ
├── docs/                        # 利用ガイド・運用方針
├── awesome/                     # AIツールキュレーション
├── case-studies/                # 導入事例テンプレート
├── DESIGN.md                    # skill.md 設計原則
├── CONTRIBUTING.md              # 貢献ガイドライン
├── CHANGELOG.md                 # 変更履歴
└── LICENSE                      # CC BY-SA 4.0
```

---

## Contact / 連絡先

**森木銀河 / Ginga Moriki**

- Web: <https://gmoriki.com>
- note: <https://note.com/pogohopper8>
- GitHub: <https://github.com/gmoriki>

---

## License

This work is licensed under [Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)](https://creativecommons.org/licenses/by-sa/4.0/).

See [LICENSE](LICENSE) for details.
