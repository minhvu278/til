# Authentication
- Được laravel xây dựng dựa trên 2 thành phần cốt lõi guard và provider 
- Nằm trong file `config/auth.php`

## Guards
- Là 1 cách cung cấp logic được dùng để xác thực người dùng 
- Thường dùng `session guard` hoặc `token guard`
    - `Session guard` duy trì trạng thái người dùng mỗi lần request bằng cookie 
    - `Token guard` xác thực người dùng bằng cách kiểm tra token hợp lệ mỗi lần request 
- Guard xác định login của việc xác thực và không cần thiết để luôn xác thực bằng cách lấy thông tin hợp lệ từ phía back-end 
- Có thể kiểm tra 1 guard mà chỉ cần kiểm tra sự có mặt của 1 thông tin cụ thể trong headers của request và xác thực người dùng dựa trên điều đó 

## Providers 
- Guard hỗ trợ việc login để xác thực thì `Provider` lấy ra dữ liệu người dùng từ phía BE 
- Nếu `Guard` yêu cầu người dùng phải hợp lệ với bộ lưu trữ ở BE thì việc triển khai truy xuất người dùng sẽ được `Providers` thực hiện 


# Authentication trong laravel 
## Controller 
- Có 1 vài controller Authentication có sẵn trong project laravel, nó nằm ở `app/Http/Controllers/Auth` 
- Để bắt đầu xác thực cần chạy 
    ```php
    php artisan make:auth

    php artisan migrate // Dùng để migrate 2 bảng users và password_resets có sẵn trong project khi mới init
    ```
    - `Đối với > phiên bản 5x trở lên hỗ trợ sẵn auth nên đã bỏ lệnh make:auth`

- Ở trong router sẽ có **Auth::routes();** - Là những lệnh sinh ra để phục vụ cho việc login, logout, register, forgot password. Ta có thể sử dụng lệnh `php artisan route:list` 

## Tùy biến Path trong controller 
- Trong LoginController, RegisterController, ResetPasswordController biến $redirect giúp ta chỉnh lại đường dẫn 
    ```php 
    protected $redirectTo = '/home';
    ```
- Có thể chỉnh trong middleware `RedirectIfAuthenticated`
    ```php 
    public function handle($request, Closure $next, $guard = null)
    {
        if (Auth::guard($guard)->check()) {
            return redirect('/home');
        }

        return $next($request);
    }
    ```
## Tùy biến username, guard 
- Theo mặc định thì sẽ đăng nhập bằng `email`. Nếu muốn tùy chỉnh có thể vào LoginController để định nghĩa lại method `username`
    ```php 
    public function username()
    {
        return 'username';
    }
    ```
- Cũng có thể tùy biến guard để xác thực user 
    - Định nghĩa 1 phương thức trong guard 
        ```php 
        use Illuminate\Support\Facades\Auth;

        protected function guard()
        {
            return Auth::guard('guard-name');
        }
        ```
        - Hàm này trả về 1 thể hiện guard 

## Tùy biến Validator, Storage khi register
- Muốn validate thêm thì ta tạo để thêm trường trong migration
- Validate và thêm dữ liệu mới vào **RegisterController** 
    ```php 
    protected function validator(array $data)
    {
        return Validator::make($data, [
            'name' => 'required|string|max:255',
            'email' => 'required|string|email|max:255|unique:users',
            'password' => 'required|string|min:6|confirmed',
            // thêm validate cho các trường vừa thêm 
            'address' => 'required',
            'phone' => 'required',
        ]);
    }

    /**
     * Create a new user instance after a valid registration.
     *
     * @param  array  $data
     * @return \App\User
     */
    protected function create(array $data)
    {
        return User::create([
            'name' => $data['name'],
            'email' => $data['email'],
            'password' => Hash::make($data['password']),
            'address' => $data['address'],
            'phone' => $data['phone'],
            'role' => 2, // ý muốn là lưu user nếu hệ thông có role = 1 là admin, 2 là user :)))
        ]);
    }
    ```
## Truy xuất nguời dùng đã xác thực 
- Khi đăng nhập thành công thì có thể truy cập thông tin người dùng ở mọi nơi 
- Để dùng được nhớ sử dụng `use Illuminate\Support\Facades\Auth` 
    ```php
    $id = Auth::user()->id; hoặc Auth::id() //Lấy về ID người .
    $user = Auth::user() // Lấy về tất cả các thông tin của người dùng.
    $email = Auth::user()->email // Lây về email người dùng.
    ...
    ```
- Xem người dùng đã xác thực (Đăng nhập vào hệ thống) thì ta sử dụng `Auth::check()` 
    ```php
    if (Auth::check()) {
    echo "Nguoi dung da dang nhap he thong";
    }
    ```
## Middleware 
- Authentication có middleware `auth`. Hệ thống muốn xác thực người dùng phải đăng nhập hệ thống trước khi thao tác 1 số phần với hệ thống 
- Middleware nằm ở `app/Http/Middleware/RedirectIfAuthenticated.php`. Có thể sử dụng ở trong `routes` hoặc trong hàm `__construct()` ở mỗi controller
- Khi dùng middleware auth trong route ta có thể chỉ định guard nào để thực hiện 