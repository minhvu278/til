# Resquest 
- Là 1 object chứa các thông tin liên quan đến HTTP request hiện tại. Dựa vào object ta có thể lấy các thông tin như `input, cookie, file,...` 

## Truy vấn thông tin URL/PATH 
- Để lấy path của request sử dụng method `path`
    ```php 
    use Illuminate\Http\Request;
    use Illuminate\Support\Facades\Route;

    Route::get('/', function (Request $request) {
        return "Path: " . $request->path();
    });
    ```
    - Lấy `fullUrl`
        ```php 
        return "Path: " . $request->fullUrl();
        ```
     