# DB設計書 (アドオン：個人経費管理機能)

- [オブジェクト概要](#オブジェクト概要)
- [テーブル定義一覧](#テーブル定義一覧)
  - [ZTM_PEM_USER（経費利用者マスタ）](#ztm_pem_user経費利用者マスタ)
  - [ZTT_PEM_TRANS（経費明細トランザクション）](#ztt_pem_trans経費明細トランザクション)
- [ER図](#er図)

---

# オブジェクト概要

本ドキュメントは、SAPアドオン開発における「個人経費管理（Personal Expense Management）」機能のデータベース設計書である。
命名規則として、マスタテーブルは `ZTM_`、トランザクションテーブルは `ZTT_` のプレフィックスを付与し、機能コードとして `PEM` を使用する。

- **開発パッケージ**: `ZPEM_FIN`
- **移送レイヤ**: `SAP`
- **データクラス**: `APPL0` (マスタ) / `APPL1` (トランザクション)
- **サイズカテゴリ**: `0`

---

# テーブル定義一覧

## ZTM_PEM_USER（経費利用者マスタ）

経費精算および管理を行う利用者を定義するマスタテーブル。

- **技術名称**: `ZTM_PEM_USER`
- **バッファリング**: 未許可
- **データクラス**: `APPL0`

| 項目名 | 項目論理名 | データ要素 | 型 | 長さ | PK | 初期値 | 備考 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **MANDT** | クライアント | `MANDT` | CLNT | 3 | ○ | ○ | SAP標準項目 |
| **ZUSER_ID** | 利用者ID | `ZDE_PEM_USER_ID` | CHAR | 10 | ○ | | 従業員番号等 |
| **ZUSERNAME** | 利用者名称 | `AD_NAMTEXT` | CHAR | 40 | | | |
| **ZEMAIL** | 連絡先アドレス | `AD_SMTPADR` | CHAR | 241 | | | |
| **ERDAT** | 作成日 | `ERDAT` | DATS | 8 | | | システム日付 |
| **ERNAM** | 作成者 | `ERNAM` | CHAR | 12 | | | 登録ユーザー名 |

## ZTT_PEM_TRANS（経費明細トランザクション）

発生した経費明細を記録するトランザクションテーブル。

- **技術名称**: `ZTT_PEM_TRANS`
- **バッファリング**: 未許可
- **データクラス**: `APPL1`

| 項目名 | 項目論理名 | データ要素 | 型 | 長さ | PK | 初期値 | 備考 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **MANDT** | クライアント | `MANDT` | CLNT | 3 | ○ | ○ | SAP標準項目 |
| **ZPEM_UUID** | 経費伝票UUID | `SYSUUID_C32` | CHAR | 32 | ○ | | ユニークキー |
| **ZUSER_ID** | 利用者ID | `ZDE_PEM_USER_ID` | CHAR | 10 | | | ZTM_PEM_USER結合 |
| **ZBUDAT** | 転記日付 | `BUDAT` | DATS | 8 | | | |
| **ZEXP_TYPE** | 経費区分 | `ZDE_PEM_ETYPE` | CHAR | 1 | | | 1:入金, 2:出金 |
| **ZCATG** | 経費カテゴリ | `ZDE_PEM_CATG` | CHAR | 10 | | | 旅費、消耗品等 |
| **DMBTR** | 国内通貨金額 | `DMBTR` | CURR | 13 | | | 参照: ZTT_PEM_TRANS-WAERS |
| **WAERS** | 通貨コード | `WAERS` | CUKY | 5 | | | T005参照 |
| **ERDAT** | 作成日 | `ERDAT` | DATS | 8 | | | |

---

# ER図

SAPのテーブル構造に基づき、クライアントキー（MANDT）を含めたエンティティ定義とする。



```mermaid
erDiagram
    ZTM_PEM_USER {
        CLNT MANDT PK
        CHAR ZUSER_ID PK
        CHAR ZUSERNAME
        CHAR ZEMAIL
        DATS ERDAT
        CHAR ERNAM
    }
    ZTT_PEM_TRANS {
        CLNT MANDT PK
        CHAR ZPEM_UUID PK
        CHAR ZUSER_ID FK
        DATS ZBUDAT
        CHAR ZEXP_TYPE
        CHAR ZCATG
        CURR DMBTR
        CUKY WAERS
        DATS ERDAT
    }
    ZTM_PEM_USER ||--o{ ZTT_PEM_TRANS : "Foreign Key (ZUSER_ID)"
