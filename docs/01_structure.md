# 01_structure.md (HTML Structure)

清善 泰賀 公式ホームページにおけるHTML構造の設計意図を解説します。
ソースコードの軽量化と、検索エンジン・アクセシビリティへの最適化を両立させています。

## 1. Meta Data & SEO
`<head>` セクションでは、SNSでの拡散と検索結果での視認性を最大化する設定を行っています。

* **Canonical URL**: 重複コンテンツを避け、`https://shizentaiga.com/` への評価を統合。
* **Favicon Ecosystem**: 標準の `.ico` に加え、モダンブラウザ用の `.svg`、iOS用の `apple-touch-icon` を完備。
* **OGP / Twitter Cards**: 共有時のインプレッションを高めるため、`og:image`（1200x630）を最適化。

## 2. JSON-LD (Structured Data)
Google等の検索エンジンに、サイトの「意味」を直接伝えるための構造化データを実装しています。

* **Person Entity**: 「清善 泰賀」が経営コンサルタント・著述家であることを定義し、各種SNS（note, LinkedIn, X等）との関連性を明示。
* **Knowledge Graph**: 検索結果のサイドパネル（ナレッジグラフ）に表示されやすい情報を整理。

## 3. Semantic Body Structure
ブラウザやスクリーンリーダーがコンテンツを正しく解釈できるよう、セマンティックなタグを採用しています。

* **`<header>`**: サイトタイトル（h1）とサブタイトルを格納。
* **`<main>`**: サイトの主要コンテンツを包含。
* **`<section>`**: `profile`, `service`, `links` の3つの論理ブロックに分割。各セクションに一貫した見出し（h2）を配置。
* **`<img>` 最適化**: 
    * `loading="eager"` & `fetchpriority="high"`: LCP（最大視覚コンテンツ）であるプロフィール画像の読み込みを最優先。
    * `decoding="async"`: 画像のデコードによるレンダリングブロックを回避。

## 4. Business Compliance (Added: 2026/04/03)
`<footer>` 領域には、信頼性を担保するための実務的要素を集約しています。

* **特定商取引法に基づく表記**: Stripe等の決済審査に準拠するため、リザーブストック内の開示ページへ直接リンク。
* **Selectable Email**: ユーザーがコピーしやすいよう `user-select: all` を適用したクラスを付与し、利便性を向上。

## 5. Optimization for Speed
外部フォントや重いスクリプトを排除し、静的HTMLの特性を活かした「Zero-Weight」な設計により、PageSpeed Insightsにおいて最高スコアを維持する構造となっています。