<img src="managing_hierarchical-01.png" alt="Categories">

# General

Với những bài toán thể hiện tree data model trên database, chúng ta có nhiều cách giải quyết (thuật toán) để làm việc này.

Dữ liệu dạng cây trong các ứng dụng website, desktop hay mobile như: menu (navigation) phân cấp, categories phân cấp ...

Cây dữ liệu gồm các node: root node, other nodes( trong đó có nodes tận cùng là các leaf nodes - các node lá).

Như hình trên cây dữ liệu có 4 cấp và có root node (ELECTRONICS), các leaf node (ở cấp thứ 3: TUBE, LCD, PLASMA  - ở cấp thứ tư: PLASH).

Sau đây sẽ giới thiệu 2 thuật toán giải quyết tree data model:

## 1. The Adjacency List Model (Parent-child model)

### Introduction:

`categories` table:

+-------------+----------------------+-----------+
|      id     | name                 | parent_id |
+-------------+----------------------+-----------+
|           1 | ELECTRONICS          |      NULL |
|           2 | TELEVISIONS          |         1 |
|           3 | TUBE                 |         2 |
|           4 | LCD                  |         2 |
|           5 | PLASMA               |         2 |
|           6 | PORTABLE ELECTRONICS |         1 |
|           7 | MP3 PLAYERS          |         6 |
|           8 | FLASH                |         7 |
|           9 | CD PLAYERS           |         6 |
|          10 | 2 WAY RADIOS         |         6 |
+-------------+----------------------+-----------+

- parent_id: là các category_id cha của nó

### Get
    - **Get full tree**

    - **Get node**

    - 

### Save

### Edit/Update

### Delete

## 2. The Nested Set Model

### Introduction:

### Get

### Save

### Edit/Update

### Delete

