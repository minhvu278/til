## Bài 1 + 2: Cài đặt laravel
- Cài đặt bằng composer: 
    ```php
        composer create-project laravel/laravel example-app
    ```

## Bài 3: Tạo tài khoản admin
- Cấu hình DB trong file .env
- Tạo bảng chạy : php artisan migrate 
- Mã hóa mật khẩu để chèn vào DB trong laravel:
    - php artisan tinker (Chạy câu lệnh php bên trong)
    - echo bcrypt('123456)

## Bài 4: Cài đặt giao diện đăng nhập admin
- Vào adminlte.io để download 
- Tạo file controller chia thư mục:
    ```php
    php artisan make:controller Admin\Users\LoginController -mc
    ```
- Copy thư mục dist & plugin ở file adminlte -> public 
- Dùng @include để import file 
- Gọi controller trong route
    ```php
    [LoginController::class, 'index']
    ```

## Bài 5,6,7,8: Đăng nhập
- Gửi dữ liệu từ form lên serve phải có @csrf (Nó sẽ tạo ra 1 mã token)
- Request $request : Nhận các thông tin từ form gửi lên serve
- Validate: 
    ```php
    $this->validate($request, [
        'name' => 'required'
    ])
    ```
- Tạo ra file hiển thị lỗi. VD: alert.blade.php
    ```php
    @if ($errors->any())
        <div class="alert alert-danger">
            <ul>
                @foreach ($errors->all() as $error)
                    <li>{{ $error }}</li>
                @endforeach
            </ul>
        </div>
    @endif
    ```
- Auth::attempt(): Kiểm tra thông tin người dùng nhập vào có khớp với data không (Có thì vào k thì next)
    VD: 
    ```php
        if(Auth::attempt([
            'email' => $request->input('email')
        ], $request->input('remember')))  // Kiểm tra nếu có thì true không thì false

        return redirect()->route('admin'); // Dùng tên đã đặt ở route 

        return redirect()->back(); //Quay lại 
    ```

- Sử dụng Session để in ra thông báo 
VD: 
    ```php
        Session::flash('error', 'Tài khoản hoặc mật khẩu sai')
    ```

- Kiểm tra xem có tồn tại Session không. Nếu có thì in ra lỗi. VD 

    ```php
        @if(Session::has('error'))
            <div class="alert alert-danger">
                {{Session::get('error')}}
            </div>
        @endif
    ```
- Kiểm tra đã đăng nhập chưa sử dụng middleware 
- Sử dụng group để nhóm nhưng thứ cần đăng nhập mới vào được
    VD: 
    ```php
        Route::middleware(['auth'])->group(function (){
            Route::get('/admin', [LoginController::class, 'index'])->name('admin')

        }
    ```

## Bài 9: Menu tạo bảng 
- Dùng migration để tạo bảng menu


