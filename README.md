# README

## ER Diagram

![freemarket_sample_68b (3)](https://user-images.githubusercontent.com/59346949/74318084-e6883580-4dbf-11ea-9b32-e2581b593492.png)



* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...




## userテーブル
|Column|Type|Options|
|nickname|string|null: false|
|email|string|null: false,uniqueness:{case_sensitive: false},
  format: {with: /\A[\w+\-.]+@[a-z\d\-.]+\.[a-z]+\z/i}|
|password|String|null: false, length: {minimum: 7}|
|password_conform|String|null: false|
|first_name|String|null: false, format: {with: /^[ -~｡-ﾟ]*$/}|
|last_name|String|null: false, format: {with: /^[ -~｡-ﾟ]*$/}|
|first_ruby|String|null: false, format: {with: /^[ -~｡-ﾟ]*$/}|
|last_ruby|String|null: false, format: {with: /^[ -~｡-ﾟ]*$/}|

### Association
- has_many :products,contract_history
- has_many :users, through:  :users_groups
- has_one  :address
- has_one  :pay_jp



## products
|Column|Type|Options|
|name|String|null: false|
|description|Text|null: false|
|price|Integer|null: false|
|condition|Integer|null: false（enum）|
|status|Integer|null: false(enum)|
|brand|String|
|send_price|Integer|null: false(enum)|
|ship_day|Integer|null: false（enum）|
|user_id|Integer|null: false, foreign_key: true|
|small_category|Integer|null: false,foreign_key: true|
|ship_from_id|Integer|null: false,foreign_key: true|

### Association
- has_many :product_images
- has_one  :contract_history
- belongs_to :small_category,ship_from
- belongs_to :users



## address
|Column|Type|Options|
|user_id|Integer|null:false,foreign_key: true|
|postal_code|String|null: false, format: {with:/\A\d{3}[_]\d{4}\z/}|
|prefectures|String|null: faise|
|municipality|String|null: faise|
|block_number|String|null: faise|
|apartment_name|String|

### Association
- belongs_to :users



## pay_jp
|Column|Type|Options|
|user_id|Integer|null: false,foreign_key: true|
|customer_id|String|null: false|
|card_id|String|null: false|

### Association
- belongs_to :users



## ship_from
|Column|Type|Options|
|products_id|Integer|null: false|
|name|String|null: false|

### Association
- belongs_to :products



## contract_history
|Column|Type|Options|
|product_id|Integer|null: false,foreign_key:true|
|user_id|Integer|null: false,foreign_key: true|

### Association
- belongs_to :products
- belongs_to :users



## product_images
|Column|Type|Options|
|products_id|Integer|foreign_key: true|
|name|String|null: false|

### Association
- belongs_to :products



## small_category
|Column|Type|Options|
|middle_category_id|Integer|null: false,foreign_key: true|

### Association
- has_many :products
- belongs_to :middle_category



## middle_category
|Column|Type|Options|
|big_category_id|Integer|null: false,foreign_key: true|

### Association
- has_many :small_category
- belongs_to :big_category



## big_category
|Column|Type|Options|
|name|String|null: false|

### Association
- has_many :middle_category
