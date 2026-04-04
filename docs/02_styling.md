# 02_styling.md (Visual Design & Layout)

清善 泰賀 公式ホームページにおける視覚設計とCSSの実装指針を解説します。
「静謐（せいひつ）さと論理」をテーマに、余計な装飾を削ぎ落とした設計を採用しています。

## 1. Fluid Typography & Layout
固定値（px）による指定を極力排除し、デバイスの画面幅に応じて滑らかに変化する「流体設計」を導入しています。

* **`clamp()` 関数の活用**: `.container` の幅を `max-width: clamp(320px, 50vw, 540px)` と定義。スマートフォンからデスクトップまで、常に最適な読書幅（一行の文字数）を維持。
* **Relative Units**: フォントサイズに `rem` を使用し、ブラウザの基本設定を尊重しつつ、セクション間のバランスを数理的に制御。

## 2. Typography & Rendering
日本語の美しさを最大限に引き出すため、タイポグラフィの設定に細心の注意を払っています。

* **Serif Stack**: 「游明朝」を筆頭とした明朝体フォントファミリーを指定。知的な信頼感と、縦のラインが強調される視覚効果を狙っています。
* **Anti-aliasing**: `-webkit-font-smoothing: antialiased` により、細い明朝体でもかすれず、MacやiPhone等の高解像度ディスプレイでクッキリと表示。
* **Line Height**: `line-height: 1.8` を設定し、学術書のようなゆとりある行間を確保。

## 3. LCP & CLS Optimization
ページの読み込み速度（LCP）と、表示のガタつき（CLS）をゼロにするための工夫をCSS側でも行っています。

* **`aspect-ratio`**: プロフィール画像の表示領域に `aspect-ratio: 3 / 4` を指定。画像が読み込まれる前から領域を確保し、レイアウトシフトを完全に防止。
* **Skeleton Background**: 画像読み込み中の空白を避けるため、`.profile-image-area` に淡いグレー（`#f0f0f0`）のプレースホルダー色を設定。

## 4. Interaction Design
過度なアニメーションを控え、ユーザーのアクションに対して最小限かつ直感的なフィードバックを返します。

* **Button Transitions**: `.btn` クラスにおいて、背景色と文字色の反転を `0.3s` で実行。
* **Link Underline**: `.link-list a` に `text-underline-offset` を設定し、文字と下線の重なりを微調整。視認性を損なわずにリンクであることを明示。

## 5. Accessibility & Compliance (Updated: 2026/04/03)
多様な閲覧環境と、決済プラットフォームの要件に合致する修正を加えました。

* **Contrast Ratio**: フッターの文字色を `#555555` とし、背景色 `#fcfcfc` に対して **7.1:1** という高いコントラスト比（WCAG AAランク以上）を維持。
* **Focus on Information**: 重要な連絡先（メールアドレス）に `user-select: all` を適用。クリック一つで全選択を可能にし、ユーザーの「コピーする」という目的を最短で達成。
* **Legal Link Visibility**: 2026/04/03のアップデートにより追加された「特商法に基づく表記」には、リンクであることを示す下線を維持し、色の判別が困難なユーザーにも配慮。

## 6. Zero-Library Policy
外部のCSSフレームワーク（Tailwind, Bootstrap等）やアイコンフォント（Font Awesome等）を一切使用していません。
これにより、CSSファイルのサイズを極小化し、HTTPリクエストを削減。ブラウザが1パケットで受信完了できるほどの軽量性を実現しています。