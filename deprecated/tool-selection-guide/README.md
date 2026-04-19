# tool-selection-guide（非推奨）

> **このスキルは 2026-04-19 v0.4.0 で非推奨となりました。**
> 代替: [skills/institutional-ai-adoption-checklist](../../skills/institutional-ai-adoption-checklist/) + [awesome/tools.md](../../awesome/tools.md)

## 非推奨の理由

「大学業務向け AI ツール選定ガイド」を単独スキルで提供する初期構想は、検討の過程で **2 層構造** の問題を単一スキルに押し込むことの無理が明らかになりました。

大学現場でのツール選定には、性質の異なる 2 つの層が存在します。

1. **用途別の個別ツール比較** — 議事録・文字起こし・翻訳・画像生成など、業務ユースケースごとに「どのツールが向いているか」を並べて見比べるレイヤー。変化が速く、記事や awesome リストに近い鮮度管理が必要。
2. **組織ガバナンスとしての選定** — 契約形態、データ保管場所、単年度予算制との整合、調達規程、学内セキュリティ審査、SSO 連携など、大学組織として導入可否を判断するレイヤー。チェックリストや成熟度モデルで体系化できる。

v0.3.0 の [institutional-ai-adoption-checklist](../../skills/institutional-ai-adoption-checklist/) が後者を正面から引き受けた結果、旧スキルに残る役割は前者（用途別の個別比較）だけになりました。これは個々のサービス仕様に強く依存し、半期改訂を超える更新頻度を要求します。スキル形式ではなく [awesome/tools.md](../../awesome/tools.md) のような awesome リストで継続的にメンテナンスする方が、構造として自然という結論に至りました。

## 代替スキル

- **[skills/institutional-ai-adoption-checklist](../../skills/institutional-ai-adoption-checklist/)** — 組織として AI ツールを導入検討する際のチェックリストと成熟度モデル。契約・予算・ガバナンスの観点を体系化しています。
- **[awesome/tools.md](../../awesome/tools.md)** — 用途別の個別ツール比較は、こちらで継続的にキュレーションします。

## 履歴

- **2026-04-15 (v0.1.0)** — README の「準備中」一覧に計上。
- **2026-04-19 (v0.3.0)** — `institutional-ai-adoption-checklist` が組織ガバナンス層を吸収。独立スキル化は v0.4 で再評価すると予告。
- **2026-04-19 (v0.4.0)** — 用途別個別比較は awesome リストで扱う方針とし、本ディレクトリへ非推奨化。

## 参照

- [CHANGELOG.md](../../CHANGELOG.md)
- [DESIGN.md §5.4 deprecated/ への移動](../../DESIGN.md#54-deprecated-への移動)
