# biz-issue-doc HTML テンプレートルール

## セクション構成

| セクション | 番号 | 色 | 内容 |
|-----------|------|-----|------|
| AS-IS | 01 | amber | 現行システム構成図（sys-grid）、在庫異動/責務テーブル、業務フロー図（flow-row） |
| 論点整理 | 02 | amber | 3 カラムの論点カード（issue-grid） |
| 選択肢比較 | 03 | amber | 2 カラムの Option カード（options-grid）、メリデメ（pc-grid） |
| 比較表 | 04 | amber | テーブル比較（cmp-table） |
| 推奨方針 | 05 | green | 推奨バッジ + 根拠（verdict）、TO-BE スコープ図（scope-grid） |
| 確認事項 | 06 | amber | チェックリスト（checklist） |
| ブロッカー | 07 | red | ブロッカーカード（blocker-grid）、優先度バッジ |
| TO-BE & Next Action | 08 | orange | フェーズ別アクション（phase-list）、アンロック項目（unlock-box） |
| 用語解説（任意） | 09 | blue | 最下部に配置する補足セクション。専門用語の「たとえ」付き解説（glossary-grid） |

## CSS ルール

- フォント: `Noto Sans JP`（本文） + `IBM Plex Mono`（コード・ラベル）
- CSS 変数:

```css
:root {
  --bg:#f4f5f7; --surface:#fff; --surface2:#f8f9fb; --border:#e2e6ea;
  --text:#1a202c; --muted:#64748b;
  --blue:#2563eb; --green:#059669; --amber:#d97706; --red:#dc2626;
  --purple:#7c3aed; --teal:#0d9488; --orange:#ea580c; --cyan:#0891b2;
  --pad:clamp(20px,5vw,72px);
}
```

## カバー構成

```html
<a class="back-link" href="../index.html">&larr; ドキュメント一覧に戻る</a>

<div class="cover">
  <div class="cover-tag">EFSO アーキテクチャ判断資料</div>
  <h1><em>#{番号}</em> {タイトル}</h1>
  <p class="cover-sub">{一文サマリ}</p>
  <div class="cover-meta">
    <!-- 関連課題、Owner、Status、影響ドメイン、優先度 -->
  </div>
</div>
```

- `back-link` の `href` はディレクトリ深さに応じて調整（`inventory/` 配下なら `../index.html`）

## カバーメタ項目（必須）

| 項目 | 説明 |
|------|------|
| 関連課題 | 本課題の番号 + 連動する課題 |
| Owner | `open-decisions.md` の owner 列 |
| Status | 現在のステータス + 次の先行タスク |
| 影響ドメイン | `open-decisions.md` の影響ドメイン列 |
| 優先度 | 高（赤）/ 中（amber）/ 低（muted） |

## 主要 CSS クラス

| クラス | 用途 | セクション |
|--------|------|-----------|
| `sys-grid` | 3 カラムのシステム構成図 | 01 |
| `flow-row` | 水平フローチャート | 01 |
| `issue-grid` | 3 カラムの論点カード | 02 |
| `options-grid` | 2 カラムの選択肢カード | 03 |
| `pc-grid` | メリット/デメリット 2 カラム | 03 |
| `cmp-table` | 比較表 | 04 |
| `verdict` | 推奨方針ボックス | 05 |
| `scope-grid` | TO-BE スコープ 3 カラム | 05 |
| `checklist` | チェックリスト | 06 |
| `blocker-grid` | ブロッカーカード 2 カラム | 07 |
| `phase-list` | フェーズ別アクション | 08 |
| `unlock-box` | アンロック項目 | 08 |
| `glossary-grid` | 用語解説カード 2 カラム | 09 |
| `note-bar` | 補足・注意事項バー | 任意 |
| `resp-table` | 汎用テーブル | 任意 |

## 色の使い分け

| 色 | 用途 |
|----|------|
| amber (`--amber`) | AS-IS 情報、課題タグ、注意バー |
| green (`--green`) | 推奨、メリット、確定事項 |
| red (`--red`) | ブロッカー、デメリット、リスク |
| orange (`--orange`) | TO-BE、ネクストアクション |
| blue (`--blue`) | 用語解説（補足セクション） |
| purple (`--purple`) | 外部システム（GWCS 等）、Option B |
| cyan (`--cyan`) | WMS、IL 関連 |
| muted (`--muted`) | 補足テキスト、ラベル |

## 用語解説セクション（Section 09）

- **配置**: 最下部（Section 08 の後）
- **目的**: 専門用語の補足解説。担当者が用語を理解している場合はスキップできる位置
- **構成**: `glossary-grid`（2 カラム）に `glossary-card` を配置
- 各カードに `glossary-term`（用語名）、`glossary-def`（定義）、`glossary-example`（「たとえ」付き解説）

## index.html カード追加ルール

- `.card.amber` クラスで追加
- `card-num`, `card-title`, `card-desc`, `card-meta`（owner/status/domain バッジ）
- note テキストに関連課題の連動情報を追記

## 参照テンプレート

既存の HTML を参照テンプレートとして使用:
- `src/issue09_warehouse-location.html` — 用語解説セクション付きのフル構成
- `src/issue12_wholesale-boundary.html` — 基本 8 セクション構成
