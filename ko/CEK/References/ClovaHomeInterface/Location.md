{% if book.TargetCountryCode == "KR" %}

| `location` 필드 값 | 위치 정보          |
|------------------|------------------|
| `ATTIC`                     | 다락방  |
| `BALCONY`                   | 베란다  |
| `BALCONY_IN_LIVING_ROOM`    | 거실베란다  |
| `BALCONY_IN_MAIN_ROOM`      | 안방베란다  |
| `BALCONY_KITCHEN`           | 주방베란다  |
| `BATH_ROOM`                 | 화장실  |
| `BATH_ROOM_IN_LIVING_ROOM`  | 거실 화장실 |
| `BATH_ROOM_IN_MAIN_ROOM`    | 안방 화장실 |
| `BED_ROOM`                  | 침실 |
| `BIG_BATH_ROOM`             | 큰 화장실  |
| `BIG_CHILD_ROOM`            | 큰아이 방  |
| `BIG_ROOM`                  | 큰 방  |
| `BOILER_ROOM`               | 보일러실 |
| `DINING_ROOM`               | 식당 |
| `DRESS_ROOM`                | 드레스룸 |
| `ENTRANCE`                  | 현관 |
| `FAMILY_ROOM`               | 가족룸  |
| `FATHER_ROOM`               | 아버님방 |
| `FIFTH_ROOM`                | 다섯째 방  |
| `FIRST_ROOM`                | 첫째 방 |
| `FOURTH_ROOM`               | 넷째 방 |
| `HALLWAY`                   | 복도 |
| `KITCHEN`                   | 주방 |
| `LIBRARY`                   | 서재 |
| `LIVING_ROOM`               | 거실 |
| `MAIN_GATE`                 | 대문 |
| `MAIN_ROOM`                 | 안방 |
| `MOTHER_ROOM`               | 어머님방 |
| `MY_ROOM`                   | 내 방  |
| `PARENTS_ROOM`              | 부모님 방  |
| `PLAY_ROOM`                 | 놀이방  |
| `POWDER_ROOM`               | 파우더룸 |
| `ROOM`                      | 방  |
| `SECOND_ROOM`               | 둘째 방 |
| `SMALL_CHILD_ROOM`          | 작은아이 방 |
| `SMALL_LIVING_ROOM`         | 작은 거실  |
| `SMALL_ROOM`                | 작은 방 |
| `SMALL_KITCHEN`             | 작은 주방  |
| `SMALL_BATH_ROOM`           | 작은 화장실 |
| `STAIRS`                    | 계단 |
| `THIRD_ROOM`                | 셋째 방 |
| `UPSTAIRS_ROOM`             | 윗층 방 |
| `UTILITY_ROOM`              | 다용도실 |
| `WAREHOUSE`                 | 창고 |
| `YARD`                      | 마당 |

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

| `location` field value | Location details(Japanese)   |
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
