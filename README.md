# README

# FURIMAのER図

## テーブル設計

### users テーブル

| Column               | Type   | Options     |
| ------------------- | ------ | ----------- |
| id                  | integer| null: false |
| nick_name           | string | null: false |
| email               | string | null: false |
| encrypted_password  | string | null: false |
| last_name           | string | null: false |
| first_name          | string | null: false |
| last_name_katakana  | string | null: false |
| first_name_katakana | string | null: false |
| birth_date          | date   | null: false |

### Association
- has_many :items
- has_many :orders

### items テーブル

| Column                 | Type       | Options                        |
| --------------------- | ---------- | ------------------------------ |
| id                    | integer    | null: false                    |
| images                | string     | null: false                    |
| description           | text       | null: false                    |
| item_name             | string     | null: false                    |
| category_id           | integer    | null: false                    |
| sales_status_id       | integer    | null: false                    |
| users_id              | references | null: false, foreign_key: true |
| price                 | integer    | null: false                    |
| shipping_fee_status_id| integer    | null: false                    |
| prefecture_id         | integer    | null: false                    |
| scheduled_delivery_id | integer    | null: false                    |

### Association
- belongs_to :user
- has_one :order

### orders テーブル

| Column    | Type       | Options                        |
| --------- | ---------- | ------------------------------ |
| id        | integer    | null: false                    |
| users_id  | references | null: false, foreign_key: true |
| item_id   | references | null: false, foreign_key: true |

### Association
- belongs_to :user
- belongs_to :item
- has_one :shipping_address

### shipping_addresses テーブル

| Column        | Type       | Options                        |
| ------------- | ---------- | ------------------------------ |
| id            | integer    | null: false                    |
| post_number   | string     | null: false                    |
| prefecture_id | integer    | null: false                    |
| town_city_name| string     | null: false                    |
| block_name    | string     | null: false                    |
| building_name | string     |                                |
| phone_number  | string     | null: false                    |
| order_id      | references | null: false, foreign_key: true |

### Association
- belongs_to :order

※imageはActive Storageで実装するため、テーブルは作成しません。
※category_id, sales_status_id, shipping_fee_status_id, prefecture_id, scheduled_delivery_idはActive Hashで実装するため、integer型で設計しています。