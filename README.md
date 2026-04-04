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
* **LCP/CLS Optimization**: `aspect-ratio` や `fetchpriority` による、知覚速度の極大化。
* **Structured Data**: JSON-LDによる詳細なSchema.org実装を完備し、ナレッジグラフとの親和性を向上。

## ⚖️ Compliance & Accessibility (Updated: 2026/04/03)
決済サービスの審査（Stripe等）および特定商取引法への準拠のため、以下のアップデートを実施しました。

* **特定商取引法に基づく表記の追加**: フッター領域に法的開示ページへのダイレクトリンクを実装。
* **コントラスト比の最適化**: `footer` 内のテキストカラーを `#555555` に設定し、背景（`#fcfcfc`）に対して十分なコントラスト比（約7:1）を確保。
* **リンクの判別性向上**: 色覚特性に配慮し、リンク箇所には `text-decoration: underline` を付与。マウスホバーによるインタラクション（`#1a1a1a`への遷移）を実装し、視認性と操作性を両立。

### ⚠️ Maintenance Note
* **外部リンクの依存性**: 現在、特商法ページは「リザーブストック（リザスト）」の生成ページを参照しています。
* **自社対応の必要性**: 将来的にリザストを解約、または決済基盤を独自システム（Aletheiaプロジェクト等）へ完全に移行する場合は、**本ドメイン配下（`shizentaiga.com/tokusho/` 等）に独自の特商法解説ページ（静的HTML）を作成・配置し、リンクを更新する必要があります。**

---
© 2026 Taiga Shizen.