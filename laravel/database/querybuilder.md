# Query Builder 
- Là 1 class trong Laravel cung cấp các phương thức để làm việc với DB thuận tiện hơn
- Sử dụng PDO parameter binding để thực thi các câu lệnh giúp tránh được lỗi `SQL injection`. Vì thế không 

# 1 số câu lệnh thực thi trong DB 

## Lấy all dữ liệu trong table 
- Sử dụng phương thức `table` để chỉ định table và lấy all ra thì sử dụng `get()`
    ```php
    use Illuminate\Support\Facades\DB;

    $users = DB::table('users')->get();
    ```
    - Lấy ra 1 dòng dữ liệu sử dụng `first()` - Limit kết quả trả về query và trả về 1 PHP stdClass nếu có dữ liệu và nếu không có thì sẽ trả về null 
        - VD: Lấy ra user đầu trong bảng `users`
            ```php 
            $user = DB::table('users')->first();
            ```
            - Ta cũng có thể thêm điều kiện `where` hoặc lấy theo `id`
                ```php
                $user = DB::table('users')->where('name', 'Zu')->first(); 
                $user = DB::table('users')->find(3);
                ```

## Chunk giá trị trả về 
- Sử dụng `chunk` để chia nhỏ data  mỗi lần lấy 
- Dùng trong trường hợp khi ta muốn lấy số lượng bản ghi lớn nhưng sợ DB quá tải 
- VD: Chia nhỏ data mỗi lần lấy 50 bản ghi 
    ```php 
    DB::table('users')->orderBy('id')->chunk(100, function ($users) {
        foreach ($users as $user) {
            //
        }
    });
    ```
    - Nếu muốn dừng việc `chunk` data lại ta có thể return false để báo cho Laravel dừng lại 

## Đếm số lượng bản ghi trả về 
- Sử dụng phương thức `count()`
    ```php
    $users = DB::table('users')->count();
    ```
- Ngoài ra có thể sử dụng 1 số phương thức khác hỗ trợ sẵn 
    - `max, min`: Lấy giá trị lớn nhất và nhỏ nhất 
    - `avg, sum`: Lấy trung bình và tổng giá trị 
        ```php
        $price = DB::table('orders')->max('price');
        ```

## Kiểm tra sự tồn tại của dữ liệu 
- Để kiểm tra câu query có tồn tại giá trị trong DB không ta sử dụng `exist()` và ngược lại `doesntExist ()` và đều trả về `true` `false`
    ```php
    if (DB::table('orders')->where('finalized', 1)->exists()) {
        // ...
    }
    ```

## Select data trong table 
- Sử dụng `select` để xác định column lấy trong DB 
    ```php
    $users = DB::table('users')
            ->select('name', 'email')
            ->get();
    ```
    - Hoặc cũng có thể truyền dữ liệu vào mảng 
        ```php 
            $users = DB::table('users')
                    ->select(['name', 'email'])
                    ->get();
        ```
    - Muốn thêm column khác sử dụng `addSelect`
        ```php
        $query = DB::table('users')->select('name');

        $users = $query->addSelect('age')->get();
        ```
    - Sử dụng `distinct()` để loại bỏ bản ghi trùng lặp 
        ```php
        $users = DB::table('users')->distinct()->get();
        ```
    - Cũng có thể sử dụng `raw()` để đưa câu lệnh SQL logic vào 
        ```php
            $users = DB::table('users')
            ->select(DB::raw('count(*) as user_count, status'))
            ->where('status', '<>', 1)
            ->groupBy('status')
            ->get();
        ```

## Join table 
- Sử dụng `join()` để join table. Và tương tự cũng có thể dùng `leftJoin, rightJoin, crossJoin`
    ```php
    $users = DB::table('users')
                ->join('contacts', 'users.id', '=', 'contacts.user_id')
                ->join('orders', 'users.id', '=', 'orders.user_id')
                ->select('users.*', 'contacts.phone', 'orders.price')
                ->get();
    ```
- Nếu chứa điều kiện phức tạp có thể truyền tham số thứ 2 là 1 `closure` để thực thi logic 
    ```php
    DB::table('users')
            ->join('contacts', function ($join) {
                $join->on('users.id', '=', 'contacts.user_id')
                     ->where('contacts.user_id', '>', 5);
            })
            ->get();
    ```

- Và ta cũng có thể join với 1 sub query khác 
    ```php 
    $latestPosts = DB::table('posts')
                       ->select('user_id', DB::raw('MAX(created_at) as last_post_created_at'))
                       ->where('is_published', true)
                       ->groupBy('user_id');

    $users = DB::table('users')
            ->joinSub($latestPosts, 'latest_posts', function ($join) {
                $join->on('users.id', '=', 'latest_posts.user_id');
            })->get();
    ```

## Union query
- Sử dụng `union()` để gộp 2 hoặc nhiều câu truy vấn lại với nhau để trở thành 1 danh sách kết quả duy nhất 
    ```php 
    use Illuminate\Support\Facades\DB;

    $first = DB::table('users')
                ->whereNull('first_name');

    $users = DB::table('users')
                ->whereNull('last_name')
                ->union($first)
                ->get();
    ```

## Where
- Khi sử dụng `where()` nhiều lần thì Laravel sẽ tự động convert các lần sau thành `and where`
    ```php
    $users = DB::table('users')
                    ->where('votes', '=', 100)
                    ->where('age', '>', 35)
                    ->get();
    ```
- Còn nếu sử dụng `where()` với 2 tham số truyền vào thì sẽ hiểu là `=` 
    ```php 
    DB::table('users')->where('votes', '=', 100);

    // Tương tự

    DB::table('users')->where('votes', 100);
    ```
- Có thể truyền array vào `where()`
    ```php 
    DB::table('users')->where('votes', 100)->where('age', 15);

    // Tương tự
    DB::table('users')->where(['votes' => 100, 'age' => 15]);
    ```

- Sử dụng `orWhere()`  
    ```php 
    $users = DB::table('users')
                        ->where('votes', '>', 100)
                        ->orWhere('name', 'John')
                        ->get();
    ```

    - Tương tự có thể sử dụng `whereNull, whereNotNull, orWhereNull và orWhereNotNull` Để thực thi các câu lệnh WHERE IS NULL, WHERE IS NOT NULL, OR WHERE IS NULL, OR WHERE IS NOT NULL trong database.

- Có thể sử dụng các phương thức `whereDate, whereMonth, whereDay, whereYear, whereTime` để truy vấn các column dữ liệu date 
    ```php 
    $users = DB::table('users')
                    ->whereDate('created_at', '2016-12-31')
                    ->get();

    $users = DB::table('users')
                        ->whereMonth('created_at', '12')
                        ->get();

    $users = DB::table('users')
                        ->whereDay('created_at', '31')
                        ->get();

    $users = DB::table('users')
                        ->whereYear('created_at', '2016')
                        ->get();

    $users = DB::table('users')
                        ->whereTime('created_at', '=', '11:20:45')
                        ->get();
    ```

