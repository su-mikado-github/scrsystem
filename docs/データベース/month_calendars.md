# 月カレンダー (month_calendars)

## テーブル情報

| 項目                           | 値                                                                                                   |
|:-------------------------------|:-----------------------------------------------------------------------------------------------------|
| システム名                     | 学食予約システム                                                                                     |
| サブシステム名                 |                                                                                                      |
| 論理エンティティ名             | 月カレンダー                                                                                         |
| 物理エンティティ名             | month_calendars                                                                                      |
| 作成者                         | Shuji Ushiyama                                                                                       |
| 作成日                         | 2023/07/17                                                                                           |
| タグ                           | ビュー                                                                                               |



## カラム情報

| No. | 論理名                         | 物理名                         | データ型                       | Not Null | デフォルト           | 備考                           |
|----:|:-------------------------------|:-------------------------------|:-------------------------------|:---------|:---------------------|:-------------------------------|
|   1 | 年                             | year                           |                                |          |                      |                                |
|   2 | 月                             | month                          |                                |          |                      |                                |
|   3 | 月初日                         | day                            |                                |          |                      |                                |
|   4 | 月初日付                       | date                           |                                |          |                      |                                |
|   5 | 月末日                         | last_date                      |                                |          |                      |                                |
|   6 | 月末日付                       | last_day                       |                                |          |                      |                                |
|   7 | 前月年                         | previous_year                  |                                |          |                      |                                |
|   8 | 前月月                         | previous_month                 |                                |          |                      |                                |
|   9 | 前月月初日                     | previous_day                   |                                |          |                      |                                |
|  10 | 前月月初日付                   | previous_date                  |                                |          |                      |                                |
|  11 | 次月年                         | next_year                      |                                |          |                      |                                |
|  12 | 次月月                         | next_month                     |                                |          |                      |                                |
|  13 | 次月月初日                     | next_day                       |                                |          |                      |                                |
|  14 | 次月月初日付                   | next_date                      |                                |          |                      |                                |
|  15 | 当月を含む初週の開始日         | start_date                     |                                |          |                      |                                |
|  16 | 当月を含む末週の終了日         | end_date                       |                                |          |                      |                                |



## ソース
```
SELECT
    T.year -- 年
    , T.month -- 月
    , T.day -- 月初日
    , T.date -- 月初日付
    , T.last_date -- 月末日
    , T.last_day -- 月末日付
    , T.previous_year -- 前月年
    , T.previous_month -- 前月月
    , T.previous_day -- 前月月初日
    , T.previous_date -- 前月月初日付
    , T.next_year -- 次月年
    , T.next_month -- 次月月
    , T.next_day -- 次月月初日
    , T.next_date -- 次月月初日付
    , (
        SELECT MAX(ST.date) FROM calendars ST WHERE ST.date <= T.date AND ST.weekday = 7
      ) AS start_date -- 当月を含む初週の開始日
    , (
        SELECT MIN(ST.date) FROM calendars ST WHERE ST.date >= T.last_date AND ST.weekday = 6
      ) AS end_date -- 当月を含む末週の終了日
FROM
    (
        SELECT
            T.year
            , T.month
            , T.day
            , T.date
            , MAX(T1.date) AS last_date
            , MAX(T1.day) AS last_day
            , T2.year AS previous_year
            , T2.month AS previous_month
            , T2.day AS previous_day
            , T2.date AS previous_date
            , T3.year AS next_year
            , T3.month AS next_month
            , T3.day AS next_day
            , T3.date AS next_date
        FROM
            calendars T 
            INNER JOIN calendars T1 ON (
                T1.year = T.year 
                AND T1.month = T.month 
            )
            INNER JOIN calendars T2 ON (
                T2.date = SubDate(T.date, INTERVAL 1 MONTH) 
            )
            INNER JOIN calendars T3 ON (
                T3.date = AddDate(T.date, INTERVAL 1 MONTH) 
            )
        WHERE
            T.day = 1 
        GROUP BY
            T.year
            , T.month
            , T.day
            , T.date
            , T2.year
            , T2.month
            , T2.day
            , T2.date
            , T3.year
            , T3.month
            , T3.day
            , T3.date 
    ) T


```



## インデックス情報

| No. | インデックス名                 | カラムリスト                             | ユニーク   | オプション                     | 
|----:|:-------------------------------|:-----------------------------------------|:-----------|:-------------------------------|



## リレーションシップ情報

| No. | 動詞句                         | カラムリスト                             | 参照先                         | 参照先カラムリスト                       |
|----:|:-------------------------------|:-----------------------------------------|:-------------------------------|:-----------------------------------------|



## リレーションシップ情報(PK側)

| No. | 動詞句                         | カラムリスト                             | 参照元                         | 参照元カラムリスト                       |
|----:|:-------------------------------|:-----------------------------------------|:-------------------------------|:-----------------------------------------|
|   1 |                                | year,month                               | calendars                      | year,month                               |


