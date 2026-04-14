# EFSO アーキテクチャ判断資料

World の EC フルスタック再構築（EFSO）プロジェクトにおける、クライアント折衝用アーキテクチャ判断資料です。

## ドキュメント一覧

| # | タイトル | Owner | 推奨案 |
|---|---------|-------|-------|
| [#9](inventory/issue09_warehouse-location.html) | 倉庫ロケーション管理の責務境界 | CTO + 開発 | Option A |
| [#15](inventory/issue15_inventory-transfer.html) | 移動出荷/入荷のCore管理範囲 | CTO + 開発 | Option A |
| [#11](purchasing/issue11_purchase-management.html) | 仕入管理のCoreスコープ | CTO + 開発 | Option A |
| [#12](inventory/issue12_wholesale-boundary.html) | EC卸売とGWCS卸売の責務境界 | CTO + 開発 | Option A（条件付き） |

## 公開URL（GitHub Pages）

https://fdaisuke666.github.io/efso-biz-requirements-definition/

## ディレクトリ構成

```
efso-biz-requirements-definition/
├── README.md                          # 本ファイル
├── index.html                         # トップページ（ドキュメント一覧）
├── inventory/                         # 在庫系 Epic
│   ├── issue09_warehouse-location.html   # #9 倉庫ロケーション管理の責務境界
│   ├── issue12_wholesale-boundary.html   # #12 EC卸売とGWCS卸売の責務境界
│   └── issue15_inventory-transfer.html   # #15 移動出荷/入荷のCore管理範囲
└── purchasing/                        # 仕入れ系 Epic
    └── issue11_purchase-management.html   # #11 仕入管理のCoreスコープ
```
