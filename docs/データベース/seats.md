# 座席 (seats)

## テーブル情報

| 項目                           | 値                                                                                                   |
|:-------------------------------|:-----------------------------------------------------------------------------------------------------|
| システム名                     | 学食予約システム                                                                                     |
| サブシステム名                 |                                                                                                      |
| 論理エンティティ名             | 座席                                                                                                 |
| 物理エンティティ名             | seats                                                                                                |
| 作成者                         | Shuji Ushiyama                                                                                       |
| 作成日                         | 2023/09/10                                                                                           |
| タグ                           | マスタ                                                                                               |



## カラム情報

| No. | 論理名                         | 物理名                         | データ型                       | Not Null | デフォルト           | 備考                           |
|----:|:-------------------------------|:-------------------------------|:-------------------------------|:---------|:---------------------|:-------------------------------|
|   1 | 座席ID                         | id                             | *自動ID                        | Yes (PK) |                      |                                |
|   2 | 座席番号                       | seat_no                        | *番号                          | Yes      |                      |                                |
|   3 | 座席グループ番号               | seat_group_no                  | *番号                          | Yes      |                      |                                |
|   4 | 削除フラグ                     | is_delete                      | *フラグ                        | Yes      | 0                    |                                |
|   5 | 登録ユーザーID                 | created_id                     | *ユーザーID                    |          |                      |                                |
|   6 | 登録タイムスタンプ             | created_at                     | *タイムスタンプ                |          |                      |                                |
|   7 | 更新ユーザーID                 | updated_id                     | *ユーザーID                    |          |                      |                                |
|   8 | 更新タイムスタンプ             | updated_at                     | *タイムスタンプ                |          |                      |                                |
|   9 | データ・バージョン             | data_version                   | *リビジョン                    | Yes      | 1                    |                                |



## インデックス情報

| No. | インデックス名                 | カラムリスト                             | ユニーク   | オプション                     | 
|----:|:-------------------------------|:-----------------------------------------|:-----------|:-------------------------------|



## リレーションシップ情報

| No. | 動詞句                         | カラムリスト                             | 参照先                         | 参照先カラムリスト                       |
|----:|:-------------------------------|:-----------------------------------------|:-------------------------------|:-----------------------------------------|



## リレーションシップ情報(PK側)

| No. | 動詞句                         | カラムリスト                             | 参照元                         | 参照元カラムリスト                       |
|----:|:-------------------------------|:-----------------------------------------|:-------------------------------|:-----------------------------------------|
|   1 |                                | id                                       | date_time_seats                | seat_id                                  |
|   2 |                                | id                                       | empty_seats                    | seat_id                                  |
|   3 |                                | id                                       | reserve_seats                  | seat_id                                  |


