# ユーザー (users)

## テーブル情報

| 項目                           | 値                                                                                                   |
|:-------------------------------|:-----------------------------------------------------------------------------------------------------|
| システム名                     | 学食予約システム                                                                                     |
| サブシステム名                 |                                                                                                      |
| 論理エンティティ名             | ユーザー                                                                                             |
| 物理エンティティ名             | users                                                                                                |
| 作成者                         | Shuji Ushiyama                                                                                       |
| 作成日                         | 2023/07/17                                                                                           |
| タグ                           |                                                                                                      |



## カラム情報

| No. | 論理名                         | 物理名                         | データ型                       | Not Null | デフォルト           | 備考                           |
|----:|:-------------------------------|:-------------------------------|:-------------------------------|:---------|:---------------------|:-------------------------------|
|   1 | ユーザーID                     | id                             | BIGINT AUTO_INCREMENT          | Yes (PK) |                      |                                |
|   2 | 姓                             | last_name                      | TEXT                           |          |                      |                                |
|   3 | 名                             | first_name                     | TEXT                           |          |                      |                                |
|   4 | 姓かな                         | last_name_kana                 | TEXT                           |          |                      |                                |
|   5 | 名かな                         | first_name_kana                | TEXT                           |          |                      |                                |
|   6 | 誕生日                         | birthday                       | DATE                           |          |                      |                                |
|   7 | 性別                           | sex                            | TINYINT                        |          |                      |                                |
|   8 | メールアドレス                 | email                          | VARCHAR(256)                   |          |                      |                                |
|   9 | 電話番号                       | telephone_no                   | VARCHAR(16)                    |          |                      |                                |
|  10 | 学年ID                         | school_year_id                 | BIGINT                         |          |                      |                                |
|  11 | 所属ID                         | affiliation_id                 | BIGINT                         |          |                      |                                |
|  12 | 所属詳細ID                     | affiliation_detail_id          | BIGINT                         |          |                      |                                |
|  13 | LINEユーザーID                 | line_user_id                   | BIGINT                         |          |                      |                                |
|  14 | システム管理者フラグ           | is_admin                       | TINYINT                        | Yes      | 0                    | 0:一般 1:システム管理者        |
|  15 | システム管理者パスワード       | admin_password                 | VARCHAR(256)                   | Yes      | '*'                  | 強制的に管理者でログインする場合のパスワード |
|  16 | リセット・トークン             | reset_token                    | VARCHAR(256)                   |          |                      |                                |
|  17 | 最終ログイン日時               | last_login_dt                  | DATETIME                       |          |                      |                                |
|  18 | チェックイン・トークン         | checkin_token                  | VARCHAR(256)                   |          |                      |                                |
|  19 | 初期設定済フラグ               | is_initial_setting             | TINYINT                        | Yes      | 0                    |                                |
|  20 | 登録日                         | regist_date                    | DATE                           |          |                      |                                |
|  21 | 退会日                         | unregist_date                  | DATE                           |          |                      |                                |
|  22 | 削除フラグ                     | is_delete                      | TINYINT                        | Yes      | 0                    |                                |
|  23 | 登録ユーザーID                 | created_id                     | BIGINT                         |          |                      |                                |
|  24 | 登録タイムスタンプ             | created_at                     | TIMESTAMP(6)                   |          |                      |                                |
|  25 | 更新ユーザーID                 | updated_id                     | BIGINT                         |          |                      |                                |
|  26 | 更新タイムスタンプ             | updated_at                     | TIMESTAMP(6)                   |          |                      |                                |
|  27 | データ・バージョン             | data_version                   | BIGINT                         | Yes      | 1                    |                                |



## インデックス情報

| No. | インデックス名                 | カラムリスト                             | ユニーク   | オプション                     | 
|----:|:-------------------------------|:-----------------------------------------|:-----------|:-------------------------------|



## リレーションシップ情報

| No. | 動詞句                         | カラムリスト                             | 参照先                         | 参照先カラムリスト                       |
|----:|:-------------------------------|:-----------------------------------------|:-------------------------------|:-----------------------------------------|
|   1 |                                | school_year_id                           | school_years                   | id                                       |
|   2 |                                | affiliation_detail_id                    | affiliation_details            | id                                       |
|   3 |                                | line_user_id                             | line_users                     | id                                       |
|   4 |                                | affiliation_id                           | affiliations                   | id                                       |



## リレーションシップ情報(PK側)

| No. | 動詞句                         | カラムリスト                             | 参照元                         | 参照元カラムリスト                       |
|----:|:-------------------------------|:-----------------------------------------|:-------------------------------|:-----------------------------------------|
|   1 |                                | id                                       | valid_tickets                  | user_id                                  |
|   2 |                                | id                                       | use_tickets                    | user_id                                  |
|   3 |                                | id                                       | buy_tickets                    | user_id                                  |
|   4 |                                | id                                       | reserves                       | user_id                                  |


