# Git SSH接続設定およびプロジェクト同期 実施記録

## 1. 概要
本資料は、GitHubへのアクセス方式を従来の「HTTPS（パスワード認証）」から「SSH（公開鍵認証）」へと切り替え、開発環境の利便性とセキュリティを向上させた際の記録である。また、未初期化の既存プロジェクトをGit管理下に置き、リモートリポジトリと同期させる際の手順についても詳述する。

---

## 2. SSH接続の設定（共通基盤）

### 2.1 SSH鍵ペアの作成
ターミナルにて以下のコマンドを実行し、GitHub用の鍵ペアを作成した。

- 実行者: tshizen2506@gmail.com  
- 保存場所: `~/.ssh/id_ed25519` (Mac標準のユーザー設定ディレクトリ)

```bash
# 鍵の生成（パスフレーズは空のままEnter連打で設定）
ssh-keygen -t ed25519 -C "tshizen2506@gmail.com"
```

### 2.2 公開鍵のGitHub登録
作成された公開鍵（.pub）の中身をクリップボードにコピーし、GitHubの  
Settings > SSH and GPG keys に登録した。

- Title: My Mac 2026-04-04
- Key type: Authentication Key

```bash
# 公開鍵の中身をコピー
pbcopy < ~/.ssh/id_ed25519.pub
```

### 2.3 疎通確認
以下のコマンドで、GitHubとの信頼関係（SSH接続）が正常に構築されたことを確認した。

```bash
ssh -T git@github.com
# 成功メッセージ例:
# Hi shizentaiga! You've successfully authenticated...
```

---

## 3. プロジェクト別 同期フェーズ

### 3.1 既存リポジトリのURL切り替え (aletheia-proto)
すでに `.git` 管理下にあるプロジェクトは、リモートURLをSSH形式に上書きするだけで移行が完了する。

```bash
git remote set-url origin git@github.com:shizentaiga/aletheia-proto.git
```

### 3.2 未初期化プロジェクトの新規同期 (shizentaiga-official)

.git ディレクトリが存在しないフォルダを、GitHubのリポジトリと紐付けた際の手順。

#### Gitの初期化とローカルコミット

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin git@github.com:shizentaiga/shizentaiga-official.git
```

#### リモートの履歴（History）の強制統合

GitHub側に既存ファイル（README等）がある場合、通常のpushは拒否されるため、以下の手順を踏む。

```bash
# 合流方針を「マージ」に固定
git config pull.rebase false

# 履歴の繋がりがないリモートブランチを強制的にプル
git pull origin main --allow-unrelated-histories
```

※ 実行時にエディタ（Vim）が開いた場合は `:wq` で保存終了する。

#### 最終プッシュ

```bash
git push -u origin main
```

---

## 4. トラブルシューティング（解決済みの課題）

| 現象 | 原因 | 解決策 |
|------|------|--------|
| fetch failed (Wrangler) | ツールバージョンが古くCloudflare APIとの通信が不安定 | `npm install -g wrangler@latest` (v4.80.0) へ更新 |
| fatal: not a git repository | フォルダがGit管理対象になっていなかった | `git init` を実行 |
| [rejected] main -> main | GitHub側に別の履歴が存在していた | `--allow-unrelated-histories` で統合 |

---

## 5. 運用確認用コマンド

今後の開発において、正常に同期されているかを確認するための主要コマンド。

### 同期の確認

```bash
git status
```

`Your branch is up to date with 'origin/main'.` と表示されればOK。

### 接続方式の確認

```bash
git remote -v
```

URLが `git@github.com:` で始まっていればSSH接続。

### 履歴グラフの確認

```bash
git log --oneline --graph --all -n 5
```

ローカル(HEAD)とリモート(origin/main)が同じ位置に存在することを確認。

---

記録日: 2026年4月4日  
作成者: shizentaiga