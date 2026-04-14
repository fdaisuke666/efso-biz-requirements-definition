# EFSO アーキテクチャ判断資料

World の EC フルスタック再構築（EFSO）プロジェクトにおける、未解決横断課題の AS-IS / TO-BE 整理ドキュメントです。クライアント折衝用の資料として使用します。

## 公開URL（GitHub Pages）

https://fdaisuke666.github.io/efso-biz-requirements-definition/

## ディレクトリ構成

```
efso-biz-requirements-definition/
├── README.md
├── index.html                                       … トップページ（ドキュメント一覧）
├── inventory/                                       … 在庫系 Epic
│   ├── issue09_warehouse-location.html              … #9  倉庫ロケーション管理の責務境界
│   ├── issue12_wholesale-boundary.html              … #12 EC卸売とGWCS卸売の責務境界
│   └── issue15_inventory-transfer.html              … #15 移動出荷/入荷のCore管理範囲
└── purchasing/                                      … 仕入れ系 Epic
    └── issue11_purchase-management.html              … #11 仕入管理のCoreスコープ
```

## 運用ルール

- ドキュメントの追加時は、対象 Epic に対応するディレクトリに `issue{番号}_{slug}.html` の命名規則で配置する
- index.html のカード一覧にリンクを追加し、GitHub Pages 経由で閲覧できるようにする
