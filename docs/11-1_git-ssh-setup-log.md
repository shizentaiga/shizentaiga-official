# 11-1_git-ssh-setup-log.md

# Git SSH接続設定およびプロジェクト同期・運用 実施記録

## 1. 概要
本資料は、GitHubへのアクセス方式を「SSH（公開鍵認証）」へ切り替え、開発環境のセキュリティと利便性を向上させた際の記録である。また、新規プロジェクトの同期手順および、macOS固有の不要ファイル（.DS_Store）の管理除外設定についても詳述する。

---

## 2. SSH接続の設定（共通基盤）

### 2.1 SSH鍵ペアの作成
ターミナルにてGitHub用の鍵ペアを作成した。

- **実行者**: tshizen2506@gmail.com
- **保存場所**: `~/.ssh/id_ed25519`

```bash
# 鍵の生成
ssh-keygen -t ed25519 -C "tshizen2506@gmail.com"
```

### 2.2 公開鍵のGitHub登録
`Settings > SSH and GPG keys` に作成した公開鍵を登録した。

- **Title**: My Mac 2026-04-04
- **Key type**: Authentication Key

```bash
# 公開鍵の中身をコピー
pbcopy < ~/.ssh/id_ed25519.pub
```

### 2.3 疎通確認
以下のコマンドで正常に認証されることを確認済み。

```bash
ssh -T git@github.com
# Hi shizentaiga! You've successfully authenticated...
```

---

## 3. プロジェクト同期とクリーンアップ

### 3.1 未初期化プロジェクトの同期 (shizentaiga-official)
ローカルディレクトリをGitHubのリポジトリと紐付け、履歴を統合した。

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin git@github.com:shizentaiga/shizentaiga-official.git

# リモートの履歴を強制統合
git config pull.rebase false
git pull origin main --allow-unrelated-histories
git push -u origin main
```

### 3.2 macOS固有ファイル (.DS_Store) の除外対応
リポジトリのクリーンさを保つため、`.DS_Store` を管理対象から完全に除外した。

#### 1. .gitignore への追記
リポジトリ直下の `.gitignore` に `.DS_Store` を追記。

#### 2. Gitキャッシュの削除
既にインデックスに登録されていた `.DS_Store` を管理から外す（物理ファイルは削除しない）。

```bash
git rm --cached -r .DS_Store
# または全ディレクトリ対象の場合
find . -name .DS_Store -print0 | xargs -0 git rm --cached --ignore-unmatch
```

#### 3. グローバル設定（推奨設定済み）
今後すべてのプロジェクトで自動的に無視されるよう設定。

```bash
git config --global core.excludesfile ~/.gitignore_global
echo .DS_Store >> ~/.gitignore_global
```

---

## 4. トラブルシューティング（解決済みの課題）

| 現象 | 原因 | 解決策 |
| :--- | :--- | :--- |
| fetch failed (Wrangler) | ツールバージョンが古く通信不安定 | `npm install -g wrangler@latest` へ更新 |
| fatal: not a git repository | フォルダがGit管理対象外 | `git init` を実行 |
| [rejected] main -> main | リモートに別の履歴が存在 | `--allow-unrelated-histories` で統合 |
| .DS_Store が消えない | Gitが既に追跡(track)中 | `git rm --cached` でキャッシュを削除 |

---

## 5. 運用確認用コマンド

### 接続方式の確認
URLが `git@github.com:` で始まっていればSSH接続である。
```bash
git remote -v
```

### 履歴と同期状態の確認
```bash
git log --oneline --graph --all -n 5
```

---

**記録日**: 2026年4月5日（最終更新）
**作成者**: shizentaiga