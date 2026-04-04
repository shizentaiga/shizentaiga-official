# Taiga Shizen Official Website
清善 泰賀の公式ポートフォリオ・ポータルサイトのリポジトリです。

## 🏛️ Design Philosophy
「不完全な論理のその先を、観測する」という活動指針を具現化するため、装飾を排したミニマルな設計を採用しています。

* **Logic-First Structure**: セマンティックなHTML構造により、検索エンジンとアクセシビリティの両面に配慮。
* **Mathematical Layout**: `clamp()` 関数による動的な流体タイポグラフィと、数理的な余白設計の導入。
* **Zero-Weight Performance**: 外部ライブラリに依存せず、ネイティブな技術のみで PageSpeed Insights 100点を実現。
* **Typography**: 日本語の美しさを引き出す「游明朝」をベースとした、縦のラインを意識した視覚構成。

## 🛠️ Technical Stack
* **HTML5 / CSS3**: モダンブラウザの機能をフル活用したノーフレームワーク実装。
* **Cloudflare Pages**: Wranglerによる高速なエッジデプロイとセキュリティの確保。
* **LCP/CLS Optimization**: `aspect-ratio` や `fetchpriority` による、知覚速度の極大化。
* **Structured Data**: JSON-LDによる詳細なSchema.org実装を完備。

## ⚖️ Compliance & Accessibility (Updated: 2026/04/05)
グローバルな決済サービス（Stripe等）の審査および特定商取引法への完全準拠のため、法務基盤を独自ドメイン（/legal）へ統合しました。

* **Legal Hubの構築**: `/legal/index.html` に特商法・利用規約・プライバシーポリシーを集約。アンカー（#）による高精度なダイレクトリンクを実装。
* **コントラスト比の最適化**: PageSpeed Insightsの指摘に基づき、テキストおよびLast Updated表示のコントラスト比を再設計。全ユーザーへの可読性を確保。
* **グローバル対応の布石**: 日本のAPPI（個人情報保護法）を主軸としつつ、将来的なGDPR/CCPAへの拡張性を考慮したディレクトリ構造を採用。
* **アクセシビリティ**: 色覚特性に配慮したインタラクションと、`@media print` による印刷用最適化（Print-friendly CSS）を完備。

## 📄 Documents
サイトの設計および運用に関する詳細ドキュメントは `docs/` ディレクトリに格納されています。

* **01_structure.md**: サイト全体の構造とディレクトリ設計
* **02_styling.md**: 視覚設計と流体タイポグラフィの定義
* **03_legal-structure.md**: 法務ページのアンカー設計と審査対策ログ（2026/04 追加）
* **11-1_git-ssh-setup-log.md**: SSH接続および環境構築のトラブルシューティング

---
© 2026 Taiga Shizen.