---
name: biz-issue-doc
description: >-
  横断課題のAS-IS/TO-BE整理HTMLを生成し、efso-biz-requirements-definitionにデプロイ。
  "/biz-issue-doc"、"課題ドキュメント作成"、"issue HTML"、"横断課題まとめ"、
  "biz issue doc"、"課題HTML生成" 等で発動。
argument-hint: "[generate|deploy] {課題番号}"
---

# biz-issue-doc — 横断課題ドキュメント生成 & デプロイ

## 概要

スプレッドシート「機能マッピング一覧」の未解決横断課題を、efso-document の AS-IS 分析をもとに HTML ドキュメントとして整理し、`fdaisuke666/efso-biz-requirements-definition` リポジトリにデプロイするワークフロー。

## サブコマンド

| サブコマンド | 説明 |
|------------|------|
| `generate {番号}` | efso-document を参照し、HTML を `src/` に生成 |
| `deploy {番号}` | 生成済み HTML を暗号化し公開ディレクトリに配置・プッシュ |
| (引数なし) | generate → deploy を連続実行 |

## リポジトリ間の関係

| リポジトリ | 役割 |
|-----------|------|
| `~/Projects/efso-document` | 情報源（AS-IS 分析・横断課題・efs-business） |
| `~/Projects/efso-biz-requirements-definition`（本リポ） | HTML 生成・暗号化・デプロイ |

## generate ステップ

1. efso-document（`~/Projects/efso-document`）の `efs-business/decisions/open-decisions.md` から対象課題の情報を取得
2. efso-document の `as-is/` を探索し、関連する AS-IS 情報を収集
3. HTML テンプレートルール（`.claude/rules/biz-issue-doc/html-template.md`）に従い HTML を生成
4. **本リポジトリの** `src/issue{番号}_{slug}.html` に出力（暗号化前のソース）
5. ブラウザまたはプレビューで表示確認

## deploy ステップ

### 前提

- 本リポジトリ内で作業する（`~/Projects/efso-biz-requirements-definition`）
- パスワード: Notion `未解決問題.md` に記載（`PASS:world`）

### 1. StatiCrypt で暗号化

```bash
staticrypt src/issue{番号}_{slug}.html \
  -p world \
  --remember 7 \
  --short \
  -d {epic}/ \
  -c false \
  --template-title "EFSO アーキテクチャ判断資料" \
  --template-color-primary "#2563eb" \
  --template-color-secondary "#f4f5f7"
```

**必須オプション（省略するとデフォルトの緑テーマになり、他ページと不一致になる）:**

| オプション | 値 | 説明 |
|-----------|-----|------|
| `--template-title` | `"EFSO アーキテクチャ判断資料"` | パスワードページのタイトル |
| `--template-color-primary` | `#2563eb` | ボタン色（EFSO blue） |
| `--template-color-secondary` | `#f4f5f7` | 背景色（EFSO light gray） |
| `--remember 7` | `7` | Remember Me の有効日数 |
| `--short` | - | 短いパスワードの警告を抑制 |
| `-c false` | - | .staticrypt.json を生成しない |

### 2. index.html にカード追加

`.card.amber` クラスで追加。`card-num`, `card-title`, `card-desc`, `card-meta`（owner/status/domain バッジ）を含める。

### 3. README.md 更新

- 「ドキュメント一覧」テーブルに行追加
- 「ファイル構成」テーブルに行追加

### 4. コミット & プッシュ

```bash
git add .
git commit -m "feat: #{番号} {タイトル}"
git push origin main
```

### 5. 確認

- GitHub Pages URL で暗号化ページが正しく表示されること
- パスワード入力後にコンテンツが復号されること
- パスワードページの UI が他のページと統一されていること（青ボタン・ライトグレー背景）

## Epic ディレクトリの対応

| 課題の影響ドメイン | ディレクトリ |
|-------------------|------------|
| 在庫管理、共通マスタ管理 | `inventory/` |
| 仕入管理 | `purchasing/` |
| 会員管理 | `member/` |
| 受注管理 | `order/` |
| その他 | ドメインに応じて新規作成 |

## ファイル命名規則

`issue{番号}_{英語slug}.html`

例: `issue09_warehouse-location.html`, `issue12_wholesale-boundary.html`
