# Api 
- 1 luồng xử lý login 
    - Route
        ```php 
        Route::post('auth/login', [PassportAuthController::class, 'login'])->name('login');
        ```
    - Controller 
        ```php 
        public function login(Request $request)
        {
            $data = [
                'username' => $request->username,
                'password' => $request->password,
            ];
            $status=$this->userRepository->check($request->username);
            if (auth()->attempt($data) && $status->status !=4) {
                $token = auth()->user()->createToken('LaravelAuthApp')->accessToken;
                return response()->json([
                    'status' => true,
                    'message' => 'Đăng nhập thành công',
                    'token' => $token,
                    'data' => Auth::user()
                ], 200);
            } else {
                return response()->json([
                    'status' => false,
                    'message' => 'Đăng nhập thất bại',
                    'error' => 'Unauthorised'
                ], 401);
            }
        }
        ```
        - `$data`: Lấy ra username, password 
        - `$status`: Check với DB 
            - `check`: Check và lấy user đầu tiên
        - Kiểm tra `status` != 4 là admin (4 là user)
        - Tạo token 
    - Trả về kiểu `json` gồm có: 
        - **status**: Trạng thái là gì 
        - **message**: Thông báo đăng nhập 
        - **token**: Để kiểm tra đối với mỗi phiên
        - **data**: Trả về data 

# APi là gì, tại sao cần dùng API 
- API viết tắt của `Application Programming Interface(Giao diện lập trình ứng dụng)`
    - Api định nghĩa ra các phương thức, giao thức công cụ xây dựng phần mềm ứng dụng - Lập trình viên có thể dễ dàng xây dựng chương trình với API 1 cách dễ dàng hơn 
## Tại sao cần sử dụng API ?
- Ví dụ trong 1 dự án cần chạy trên cả môi trường web và mobile, để đồng bộ hóa thì ta chỉ cần viết API chung cho chúng ló

## HTTP Request 
- Có tất cả 9 loại method
    ```
    GET: được sử dụng để lấy thông tin từ sever theo URI đã cung cấp.
    HEAD: giống với GET nhưng response trả về không có body, chỉ có header
    POST: gửi thông tin tới sever thông qua các biểu mẫu http (đăng kí chả hạn ...)
    PUT: ghi đè tất cả thông tin của đối tượng với những gì được gửi lên
    PATCH: ghi đè các thông tin được thay đổi của đối tượng.
    DELETE: xóa tài nguyên trên server.
    CONNECT: thiết lập một kết nối tới server theo URI.
    OPTIONS: mô tả các tùy chọn giao tiếp cho resource.
    TRACE: thực hiện một bài test loop - back theo đường dẫn đến resource.
    ```

## Router Restful 
- Khi làm việc với Api thì ta sẽ chuyển sang sử dụng file `routes/api`
- Một số setting mặc định 
    - URL: Những router được khai báo trong file này mặc định có prefix url là api - VD: `minhvu278/api/products`
    - Middleware: Mặc định sẽ được gán middleware group là api. Trong file *Kernel* sẽ có 2 middleware thuộc Middleware Group: api là throttle(Giới hạn request/time) và bindings(model binding)
- Mặc định router sẽ được gán middleware `bindings` vì thế nếu muốn sử dụng trong controller ta chỉ cần chỉnh sửa các tham số trong router
    ```php 
    Route::get('products/{product}', 'Api\ProductController@show')->name('products.show');

    Route::put('products/{product}', 'Api\ProductController@update')->name('products.update');

    Route::patch('products/{product}', 'Api\ProductController@update')->name('products.update');

    Route::delete('products/{product}', 'Api\ProductController@destroy')->name('products.destroy');
    ```
- Có thể viết gọn thành 
    ```php 
    Route::apiResource('products', 'Api\ProductController');
    ```

## Resource Controller 
- Khá giống như bên web
    ```
    php artisan make:controller Api/ProductController --api
    ```
- Nếu muốn sử dụng model binding thì khi tạo resource: 
    ```php 
    php artisan make:controller Api/ProductController --api --model=Models/Product
    ```
    - Nó sẽ tự động binding vào 1 số phương thức cần lấy id, VD 
        ```php 
        public function show(Product $product)
        {
            //
        }
        ```
- Mặc định khi sử dụng router apiResource thì dữ liệu trả về mặc định sẽ trả ra kiểu json và status tương ứng ta chỉ cần return
- Và cũng có thể tùy biến status trả về bằng **class Illuminate\Http\Response** 
    ```php 
    <?php

    namespace App\Http\Controllers;

    use App\Models\Product;
    use Illuminate\Http\Request;
    use Illuminate\Http\Response;

    class ProductController extends Controller
    {
        /**
        * Display a listing of the resource.
        *
        * @return \Illuminate\Http\JsonResponse
        */
        public function index()
        {
            $products = Product::all();

            return response()->json($products, Response::HTTP_OK);
        }
    }
    ```
## Eloquent Resource 
- //TODO:


## Một số http status code 
- **405 Method not allowed**: Sai method 
- **400 BAD Request**: Tham số request không đúng với tham số serve để lấy được kết quả

## Các cách khác nhau để gửi dữ liệu Request trong postman 
- Khi chọn sẽ có các option khác nhau để gửi dữ liệu bên trong body 
    - **Form Data**: Giống với việc điền form và được viết dưới dạng KEY - VALUE 
    - **x-www-form-urlencoded**: Khá là giống form data tuy nhiên là khi sử dụng cái này thì url sẽ được mã hóa khi gửi
    - **raw**: Body message
    - **binary**: Dùng để chọn file