# 修正履歴：Dify 講座群（Docker Compose の版と起動手順）

## 1. 主な修正内容
| 項目 | 修正前 | 修正後（公式の現在の記載） | 出典 |
|---|---|---|---|
| Docker Compose の版 | 2.24.0 以上 | **2.35.0 以上** | Dify 公式（インストール・Docker Compose デプロイ）【直接取得・確認済】 |
| 起動前の設定 | .env.example をコピー | 加えて `openssl rand -hex 32` で生成したトークンを `DIFY_AGENT_LOCAL_SANDBOX_AUTH_TOKEN` に設定 | 同上 |
| 設定の構成 | .env の編集が中心 | `.env` に加え、`envs/` の `.defaults` と上書きファイル（例：`envs/infrastructure/nginx.env`） | 同上 |
| ポートの変更 | 記載が不十分 | `EXPOSE_NGINX_PORT`（既定 80） | 同上 |
| 再起動 | down → up -d | `up -d` を使う（`restart` は古い環境変数を保持するため不可） | 同上 |
| アップグレード | 退避 → 停止 → 更新 → 確認 | 停止 → 退避（volumes・.env・envs・カスタム compose）→ git stash → checkout → 設定の見直し → `config --quiet` → pull → `up -d` → `ps --all` | 同上 |
| 確認コマンド | ps | `docker compose ps --all`（init_permissions は Exited (0) が正常） | 同上 |

## 2. 修正したファイル
- PowerPoint（再作成）：Udemy講座（受講生用・講師用）、DXエンジニア実務（受講生用・講師用）、実務リファレンス、Windows対応・コマンド全集、初期設定、8段階スロープ（受講生用・講師用）、ネットワークとブラウザの基礎（訂正ページ追加）
- まとめ版（再生成）：全教材（292枚）、受講生用まとめ（180枚）、受講生用全部まとめ（254枚）、初期設定込み（255枚）、前提付き（62枚）、前提とChatGPT講座（243枚）、ChatGPT講座まとめ（50枚）
- Markdown：Dify開発環境構築ガイド、アップグレードの記事（Zenn用・差分を追記）、DX実務講座のレビュー、アップグレードのレビュー（追記）

## 3. 未確認・残課題
- Dify公式の直接取得は、Docker Compose デプロイのページと、インストールのページの2件。対象の版で再確認すること。
- 出典URLのうち、直接確認できたのは Dify 公式の3件（上記）、Marketplace の OpenAI プラグイン、RFC 9110（検索結果）。その他の URL は「要確認」。
- Docker Desktop の画面名、WSL コマンドの細部、VSCode の操作は未検証。
- Dify入門（セクション1〜3）は概念の資料で、起動手順を含まないため変更なし。

## 4. 確認の方法
公開または受講前に、次を行うこと。
1. 対象の Dify 版の公式ドキュメントで、Compose 版・トークン・envs の記載を確認する
2. 検証環境で起動からアップグレードまでを一度通す
3. 「要確認」の URL を開き、版と日付を記録する
