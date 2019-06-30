# Migrations

## 1 - migrate order theo time trên tên của file migrate.

Chú ý thứ tự migrate khi chạy lệnh `php artisan migrate` sẽ theo time trên tên của file migrate.
=> Tạo file migrate: tạo table khoá chính trước => tạo table có khoá ngoại sau => cuối cùng table trung gian.

## 2 - id và foreign_id nên là cùng loại data:
- Nếu khoá chính là: `$table->increments('id');` (kiểu int) => foreign_id cũng phải là kiểu int (unsignedInteger).

- Nếu `$table->bigIncrements('id'):` (kiểu bigInt) => foreign_id cũng phải là kiểu bigInt (unsignedBigInteger).

- Nếu primary và foreign_id tương ứng mà khác kiểu => sẽ gặp lỗi khi `php artisan migrate` :
khi với việc tạo khoá ngoại (foreign):
`$table->foreign('foreign_id')->references('id')->on('foreign_table')->onDelete('cascade');`

## 3 - Chú ý số tham số truyền vào của các hàm type data
Ex:
`$table->tinyInteger('status');` // Hàm này chỉ có 1 tham số
`$table->char('name', 100);` // Hàm này có 2 tham số, tham số thứ 2 có default value

