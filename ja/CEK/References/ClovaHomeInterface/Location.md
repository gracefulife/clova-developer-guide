{% if book.TargetCountryCode == "KR" %}

| `location`の値 | 位置情報          |
|------------------|------------------|
| `ATTIC`                     | 屋根裏部屋  |
| `BALCONY`                   | ベランダ  |
| `BALCONY_IN_LIVING_ROOM`    | リビングのベランダ  |
| `BALCONY_IN_MAIN_ROOM`      | 寝室のベランダ  |
| `BALCONY_KITCHEN`           | キッチンのベランダ  |
| `BATH_ROOM`                 | トイレ  |
| `BATH_ROOM_IN_LIVING_ROOM`  | リビングのトイレ |
| `BATH_ROOM_IN_MAIN_ROOM`    | 寝室のトイレ |
| `BED_ROOM`                  | ベッドルーム |
| `BIG_BATH_ROOM`             | メイントイレ  |
| `BIG_CHILD_ROOM`            | 上の子の部屋  |
| `BIG_ROOM`                  | 大きな部屋  |
| `BOILER_ROOM`               | ボイラー室 |
| `DINING_ROOM`               | ダイニング |
| `DRESS_ROOM`                | ドレスルーム |
| `ENTRANCE`                  | 玄関 |
| `FAMILY_ROOM`               | 家族の部屋  |
| `FATHER_ROOM`               | お父さんの部屋 |
| `FIFTH_ROOM`                | 部屋5  |
| `FIRST_ROOM`                | 部屋1 |
| `FOURTH_ROOM`               | 部屋4 |
| `HALLWAY`                   | 廊下 |
| `KITCHEN`                   | キッチン |
| `LIBRARY`                   | 書斎 |
| `LIVING_ROOM`               | リビング |
| `MAIN_GATE`                 | 正門 |
| `MAIN_ROOM`                 | 寝室 |
| `MOTHER_ROOM`               | お母さんの部屋 |
| `MY_ROOM`                   | 私の部屋  |
| `PARENTS_ROOM`              | 両親の部屋  |
| `PLAY_ROOM`                 | 遊び部屋  |
| `POWDER_ROOM`               | 洗面所 |
| `ROOM`                      | 部屋  |
| `SECOND_ROOM`               | 部屋2 |
| `SMALL_CHILD_ROOM`          | 下の子の部屋 |
| `SMALL_LIVING_ROOM`         | 小さなリビング  |
| `SMALL_ROOM`                | 小さな部屋 |
| `SMALL_KITCHEN`             | 小さなキッチン  |
| `SMALL_BATH_ROOM`           | トイレ |
| `STAIRS`                    | 階段 |
| `THIRD_ROOM`                | 部屋3 |
| `UPSTAIRS_ROOM`             | 上の階の部屋 |
| `UTILITY_ROOM`              | ユーティリティルーム |
| `WAREHOUSE`                 | 倉庫 |
| `YARD`                      | 庭 |

{% elif book.TargetCountryCode == "JP" %}

{% if book.language == "en" %}

| `location` field value |    Location details       |    Location details(JP)      |
|------------------|------------------|------------------|
| `ATTIC`                     | Attic                      | 屋根裏部屋  |
| `BALCONY`                   | Balcony                    | ベランダ |
| `BATH_ROOM`                 | Bathroom                   | バスルーム |
| `BED_ROOM`                  | Bedroom                    | ベッドルーム |
| `DINING_ROOM`               | Dining room                | ダイニング |
| `ENTRANCE`                  | Entrance                   | 玄関 |
| `FIRST_ROOM`                | First room                 | 部屋1 |
| `HALLWAY`                   | Hallway                    | 廊下 |
| `KITCHEN`                   | Kitchen                    | キッチン |
| `LIBRARY`                   | Library                    | 書斎 |
| `LIVING_ROOM`               | Living room                | リビング |
| `POWDER_ROOM`               | Powder room                | 洗面所 |
| `ROOM`                      | Room                       | 部屋 |
| `SECOND_ROOM`               | Second room                | 部屋2 |
| `SMALL_CHILD_ROOM`          | Younger child's room       | 子供部屋 |
| `SMALL_BATH_ROOM`           | Toilet                     | トイレ |
| `STAIRS`                    | Stairs                     | 階段 |
| `THIRD_ROOM`                | Third room                 | 部屋3 |
| `WAREHOUSE`                 | Warehouse                  | 倉庫 |
| `YARD`                      | Yard                       | 庭 |
| `JAPANESE_STYLE_ROOM`       | Japanese Style Room        | 和室 |

{% elif book.TargetCountryCode == "JP" %}

| `location`の値 | 位置情報     |
|------------------------|------------------------------|
| `ATTIC`                | 屋根裏部屋 |
| `BALCONY`              | ベランダ |
| `BATH_ROOM`            | バスルーム |
| `BED_ROOM`             | ベッドルーム |
| `DINING_ROOM`          | ダイニング |
| `ENTRANCE`             | 玄関 |
| `FIRST_ROOM`           | 部屋1 |
| `HALLWAY`              | 廊下 |
| `KITCHEN`              | キッチン |
| `LIBRARY`              | 書斎 |
| `LIVING_ROOM`          | リビング |
| `POWDER_ROOM`          | 洗面所 |
| `ROOM`                 | 部屋 |
| `SECOND_ROOM`          | 部屋2 |
| `SMALL_CHILD_ROOM`     | 子供部屋 |
| `SMALL_BATH_ROOM`      | トイレ |
| `STAIRS`               | 階段 |
| `THIRD_ROOM`           | 部屋3 |
| `WAREHOUSE`            | 倉庫 |
| `YARD`                 | 庭 |
| `JAPANESE_STYLE_ROOM`  | 和室 |

{% endif %}

{% endif %}
