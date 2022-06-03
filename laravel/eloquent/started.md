# Eloquent Model 
- Là 1 modul trong laravel core. 
- Là object-relational mapper (ORM) giúp tương tác dữ liệu trong DB 1 cách đơn giản linh hoạt hơn 
- Khi sử dụng Eloquent mỗi table trong DB sẽ được gán với 1 model và ta có thể tương tác với bảng đó như CRUD qua Eloquent Model 

## Tạo Eloquent model 
- Để tạo model ta có thể sử dụng command 
    ```
    php artisan make:model ModelName
    ```
    - Và cũng có thể tạo ra 1 số thứ như `migration, seed,...` bằng cách thêm flag -- vào cuối 
        ```
        // Tạo model đồng thời tạo cả migration
        php artisan make:model Flight --m
        ```
    - Cũng có thể tạo 1 lúc nhiều cái 
        ```
        php artisan make:model Flight -mfsc
        ```

## Cấu hình Eloquent Model 
- Tên bảng
    - Sẽ sử dụng tên bảng là tên của model và được viết dưới dang `snake_case` và thể hiện ở dạng số nhiều 
        - VD tên model là UserController thì table name sẽ là `user_controllers`
    - Hoặc ta cũng có thể xác định thủ công bằng cách gán chúng vào `$table`
        ```php
         protected $table = 'my_flights';
         ```
- Primary key
    - Mặc định sẽ nhận định column `id` sẽ là khóa chính trong model, tuy nhiên thì ta cũng có thể định nghĩa trong `$primaryKey` 
        ```php
        protected $primaryKey = 'flight_id';
        ```
    - Ngoài ra thì Laravel sẽ coi mặc định khóa chính có kiểu dữ liệu là `increment` và sẽ tự convert khóa chính thành kiểu số. 

    - Nếu khóa chính không phải `increment` hoặc không muốn ép về kiểu số thì ta thiết lập thuộc tính `$incrementing` về false 
        ```php 
        public $incrementing = false;
        ```
    - Sử dụng `$keyType` để xác định lại kiểu dữ liệu
        ```php 
        protected $keyType = 'string';
        ```

- Timestamp 
    - Mặc định Laravel sẽ coi như trong table có 2 column là `created_at` và `updated_at` và sẽ mặc định set giá trị cho 2 cột dữ liệu này trong trường hợp tạo mới hoặc update. Nếu không muốn ta có thể set `$timestamp` về false 
        ```php 
        public $timestamps = false;
        ```
    
- Giá trị mặc định 
    - Mặc định khi ta instance 1 model class nó sẽ không chứa giá trị của 1 attribute nào(attribute ở đây chính là column trong table trong DB)
    - Nếu muốn xác định giá trị mặc định cho cho attribute nào đó thì thiết lập trong `$attributes`
        ```php 
        protected $attributes = [
            'delayed' => false,
        ];
        ```

- Database connection 
    - Mặc định sẽ sử dụng connection default được thiết lập trong ứng dụng. 
    - Có thể sử dụng connection khác bằng cách sử dụng `$connection`
        ```php
        protected $connection = 'sqlite';
        ```

# Query với Eloquenr ORM

## Query
- Có thể coi như là 1 bản nâng cấp của query builder với nhiều tính năng hơn 
- Sử dụng `all()` giống như query builder để lấy ra all các bản ghi của model tron Eloquent 
    ```php 
    use App\Models\Flight;

    foreach (Flight::all() as $flight) {
        echo $flight->name;
    }
    ```
    - Ta có thể hiểu tương tự như 1 query builder được định sẵn table (Mặc dù chính xác là chúng đc base trên 2 class khác nhau) vì thế nên ta cũng có thể build query qua các method như builder query và sử dụng `get()` để lấy dữ liệu 
        ```php
        $flights = Flight::where('active', 1)
        ->orderBy('name')
        ->take(10)
        ->get();
        ```
    - Làm mới dữ liệu từ 1 eloquent đã được query trước đó bằng cách sử dụng `fresh()` - nó sẽ thực hiện query lại đến DB để lấy dữ liệu mới nhất của bản ghi 
        ```php
        $flight = Flight::where('number', 'FR 900')->first();

        $freshFlight = $flight->fresh();
        ```
    - `refresh()`: Lấy dữ liệu mới nhất trong bản ghi trong DB đồng thời lấy cả các dữ liệu mới của relationship nếu có 
        ```php 
        $flight = Flight::where('number', 'FR 900')->first();

        $flight->number = 'FR 456';

        $flight->refresh();

        $flight->number; // "FR 900"
        ```

    