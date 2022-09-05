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

## 1 số hàm request thường dùng 
- `request->all()`: Lấy tất cả nội dung request và trả về 1 array tương ứng
- `request->except()`: Loại bỏ một vài input nằm trong whitelist
- `request->only()`: Chỉ lấy một vài input nằm trong whitelist
- `request->has()` và `request->exists()`: Đều dùng để kiểm tra 1 tham số có nằm trong request hay không 
    - **has**: trả về FALSE nếu 1 tham số tồn tại bên trong request và nó khồng có giá trị(null hoặc rỗng)
    - **exists**: Chỉ kiểm tra tham số có tồn tại trong request và trả về true nếu nó có tồn tại
- `request->input()`: trả về 1 field trong request và cũng có thể truyền giá trị mặc định nếu field không tồn tại bên trong request
    ```php 
    $var = $request->input('field', 'default-value');
    ```
- `attach()`: Dùng để chèn thêm 1 bản ghi vào bảng trung gian
     