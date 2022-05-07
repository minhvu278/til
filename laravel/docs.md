# The Basic 

## Routing 

- Basic routing 
    - Cung cấp 1 phương pháp xác định các route 1 cách đơn giản mà không cần đến các tệp cấu hình route phức tạp 
    ```
    use Illuminate\Support\Facades\Route;
 
    Route::get('/greeting', function () {
        return 'Hello World';
    });
    ```

- Route mặc định 
    - Các đường dẫn trong Laravel đều được xác định trong thư mục route 
    - Các files được tải tự động bởi `App\Providers\RouteServiceProvider`
    - `routes/web.php` - Xác định các route cho web 
        ```
        use App\Http\Controllers\UserController;
 
        Route::get('/user', [UserController::class, 'index']);
        ```
       
- Router Methods 
    - Cho phép đăng kí các router để đáp ứng với các hành động trên HTTP
        ```
        Route::get($uri, $callback);
        Route::post($uri, $callback);
        Route::put($uri, $callback);
        Route::patch($uri, $callback);
        Route::delete($uri, $callback);
        Route::options($uri, $callback);
        ```
    - Có thể đăng kí router đáp ứng nhiều method thì ta sử dụng `match`
        ```
        Route::match(['get', 'post'], '/', function () {
            //
        });
        ```
    - Route có thể đáp ứng tất cả cả method thì dùng `any`
        ```
        Route::any('/', function () {
            //
        });
        ```

- Redirect Routes 
    - Để chuyển hướng route sử dụng `Route::redirect`
        ```
        Route::redirect('/here', '/there');
        ```
        - Mặc định thì `Route::redirect` sẽ trả về `302` tuy nhiên ta có thể chỉnh nó bẳng cách thêm tham số thứ 3 vào 
            ```
            Route::redirect('/here', '/there', 301);
            ```
        - Hoặc cũng có thể sử dụng `Route::permanentRedirect` để trả về trạng thái `301`

- View route
    - Nếu yêu cầu chỉ cần trả về view thì ta có thể sử dụng `Route::view`
        - Khá giống với `redirect` là ta không cần viết 1 route đầy đủ hay controller
            ```
            Route::view('/welcome', 'welcome');
            ```
            - URL lầ đối số đầu tiên và view sẽ là đối số thứ 2
        
- Router Parameter 
    - Có thể lấy id người dùng thông qua URL 
        ```
        Route::get('/user/{id}', function ($id) {
            return 'User '.$id;
        });
        ```
    - Có thể xác định nhiều tham số trên URL 
        ```
        Route::get('/posts/{post}/comments/{comment}', function ($postId, $commentId) {
            //
        });
        ```
    