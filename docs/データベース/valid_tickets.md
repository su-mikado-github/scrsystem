# 有効回数券 (valid_tickets)

## テーブル情報

| 項目                           | 値                                                                                                   |
|:-------------------------------|:-----------------------------------------------------------------------------------------------------|
| システム名                     | 学食予約システム                                                                                     |
| サブシステム名                 |                                                                                                      |
| 論理エンティティ名             | 有効回数券                                                                                           |
| 物理エンティティ名             | valid_tickets                                                                                        |
| 作成者                         | Shuji Ushiyama                                                                                       |
| 作成日                         | 2023/09/10                                                                                           |
| タグ                           | ビュー                                                                                               |



## カラム情報

| No. | 論理名                         | 物理名                         | データ型                       | Not Null | デフォルト           | 備考                           |
|----:|:-------------------------------|:-------------------------------|:-------------------------------|:---------|:---------------------|:-------------------------------|
|   1 | 購入回数券ID                   | buy_ticket_id                  |                                |          |                      |                                |
|   2 | ユーザーID                     | user_id                        |                                |          |                      |                                |
|   3 | 購入日時                       | buy_dt                         |                                |          |                      |                                |
|   4 | 回数券ID                       | ticket_id                      |                                |          |                      |                                |
|   5 | 購入回数券枚数                 | ticket_count                   |                                |          |                      |                                |
|   6 | 利用回数券枚数                 | use_ticket_count               |                                |          |                      |                                |
|   7 | 有効回数券枚数                 | valid_ticket_count             |                                |          |                      |                                |
|   8 | 支払日時                       | payment_dt                     |                                |          |                      |                                |



## ソース
```
SELECT
    T.id AS buy_ticket_id -- 購入回数券ID
    , T.user_id -- ユーザーID
    , T.buy_dt -- 購入日時
    , T.ticket_id -- 回数券ID
    , T.ticket_count -- 購入回数券枚数
    , IFNULL(T1.use_ticket_count, 0) AS use_ticket_count -- 利用回数券枚数
    , T.ticket_count - IFNULL(T1.use_ticket_count, 0) AS valid_ticket_count -- 有効回数券枚数
    , T.payment_dt -- 支払日時
FROM
    buy_tickets T
    LEFT OUTER JOIN (
        SELECT
            ST.buy_ticket_id
            , COUNT(*) AS use_ticket_count
        FROM
            use_tickets ST
        WHERE
            ST.is_delete = 0
        GROUP BY
            ST.buy_ticket_id
    ) T1 ON (
        T1.buy_ticket_id = T.id
    )
WHERE
    T.is_delete = 0


```



## インデックス情報

| No. | インデックス名                 | カラムリスト                             | ユニーク   | オプション                     | 
|----:|:-------------------------------|:-----------------------------------------|:-----------|:-------------------------------|



## リレーションシップ情報

| No. | 動詞句                         | カラムリスト                             | 参照先                         | 参照先カラムリスト                       |
|----:|:-------------------------------|:-----------------------------------------|:-------------------------------|:-----------------------------------------|
|   1 |                                | user_id                                  | users                          | id                                       |
|   2 |                                | buy_ticket_id                            | buy_tickets                    | id                                       |



## リレーションシップ情報(PK側)

| No. | 動詞句                         | カラムリスト                             | 参照元                         | 参照元カラムリスト                       |
|----:|:-------------------------------|:-----------------------------------------|:-------------------------------|:-----------------------------------------|
|   1 |                                | buy_ticket_id                            | use_tickets                    | buy_ticket_id                            |


