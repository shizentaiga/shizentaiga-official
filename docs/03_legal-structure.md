# 03_Legal Structure & Compliance Log
**Last Updated: 2026-04-05**

## 1. 概要 (Overview)
shizentaiga.com における法務情報（特定商取引法、利用規約、プライバシーポリシー等）の管理構造と、決済審査（Stripe等）を通過するための設計意図を記録する。

## 2. ディレクトリ構成 (Directory Structure)
グローバル標準に基づき、拡張子を排したクリーンなURL（/legal/）を採用している。

- **Physical Path**: `/legal/index.html`
- **Public URL**: `https://shizentaiga.com/legal/`

### 設計意図:
1枚の静的HTMLに全情報を集約することで、情報の整合性を担保し、保守コストを最小化する。将来的なファイル分割が必要になった際も、ディレクトリ単位で管理しているため、外部リンク（決済ボタンのリンク等）を壊さずに移行が可能である。

## 3. アンカー設計 (Anchor Definitions)
各セクションに固有のID（Anchor）を割り当て、ダイレクトアクセスを可能にしている。

| ID | 名称 (Heading) | スコープ |
| :--- | :--- | :--- |
| #terms | Terms of Service | 利用規約。自己責任原則と合意管轄の明示。 |
| #privacy | Privacy Policy | 個人情報保護。現状は日本(APPI)を対象。 |
| #cookies | Cookie Policy | クッキー利用の透明性確保。 |
| #commercial | Commercial Disclosure | 特定商取引法に基づく表記。決済審査の核心。 |
| #refund | Refund Policy | 返金規定。#termsと矛盾しない「3日前」ルール。 |
| #contact | Contact Us | 問い合わせ窓口。応答目安時間の明記。 |

## 4. 決済審査（Stripe等）対策の要点
本ページは、国際的な決済プラットフォームの機械的な審査および目視審査を即時通過させるための「攻めの設計」を行っている。

- **特商法の12項目網羅**: 販売価格の参照先、支払い時期、提供時期等の必須項目をTable形式で視認性高く配置。
- **電話番号・所在地の省略規定**: 「請求があった場合に遅滞なく開示する」旨を明記し、#contactへの導線を配置することで法的要件をクリア。
- **応答目安の明記**: 審査官が重視する「連絡可能性」を担保するため、`Response Time: 2 business days` を明記。
- **返金規定の独立**: 審査で最も精査される Refund Policy を独立したアンカー（#refund）として定義。

## 5. アクセシビリティと技術仕様
- **PageSpeed Insights 対応**: メタディスクリプションの完備および、テキストカラーのコントラスト比（4.5:1以上）を確保。
- **印刷最適化 (Print-friendly)**: ユーザーが規約を物理的に保管できるよう、`@media print` にて不要なナビゲーションを除外する制御を実装。
- **流体デザイン**: モバイル端末（スマートフォン）での閲覧時も、表形式（Table）が崩れないようCSSによるレスポンシブ制御を行っている。

## 6. 将来の拡張 (Future Roadmap)
- **GDPR/CCPA対応**: 事業規模の拡大に合わせ、#privacy 内の `Applicable Regions` を更新し、適切な法域スコープへ拡張する。
- **URLリダイレクト**: 将来的に各規約を別ページに分ける場合は、`/legal/privacy` などのURLを各アンカーへ301リダイレクトする運用を検討する。

---
Document Author: Taiga Shizen