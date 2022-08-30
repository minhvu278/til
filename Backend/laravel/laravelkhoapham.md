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

## Bài 9, 10: Menu tạo bảng 
- Dùng migration để tạo bảng menu

## Bài 10: Validate menu
- Tạo ra 1 class form request
```php 
php artisan make:request Menu\CreateFormRequest
```
- Viết code xử lý bên trong func rules 
    ```php
    public function rules()
    {
        return [
            'name' => 'required'
        ];
    }
    ```
- Có thể custome thông báo lỗi 
    ```php 
    public function messages() : array {
        return  [
            'name.required' => 'Vui lòng nhập tên danh mục'
        ];
    }
    ```
## Bài 11,12: Tạo menu danh mục
- Tạo ra MenuService để xử lý các đoạn code bên trong (Như thêm sửa xoá)
    ```php
    public function create($request){
        try {
            Menu::create([
                'name' => (string) $request->input('name'),
                'parent_id' => (int) $request->input('parent_id'),
                'description' => (string) $request->input('description'),
                'content' => (string) $request->input('content'),
                'active' => (string) $request->input('active'),
                'slug' => Str::slug($request->input('name'), '-')
            ]);

            Session::flash('success', 'Tạo danh mục thành công');
        }catch (\Exception $err){
            Session::flash('error', $err->getMessage());
            return false;
        }
        return true;
    }
    ```
## Bài 13: Tạo danh sách
VD: 

    ```php
        <table class="table">
            <thead>
            <tr>
                <th>ID</th>
                <th>Name</th>
                <th>Active</th>
                <th>Update</th>
                <th>&nbsp;</th>
            </tr>
            </thead>

            <tbody>
            
            </tbody>
        </table>
    ```

- Có thể viết trực tiếp vào trong tbody
- Hoặc tạo ra 1 function để viết
    - Tạo function để viết thì có thể dùng ở nhiều nơi nên cho vào function autoload (composer.json)
    ```php
    "files": [
            "app/Helpers/Helper.php"
        ]
    ```
    - Update lại composer: composer dump-autoload
    - Sử dụng {!! !!} thì nó sẽ biên dịch được html

## Bài 14: Menu xoá danh mục
- Sử dụng ajax để xoá
- Dùng token để gửi dữ liệu 
    - Tạo file main.js
    - Cho vào header: 
    ```php
    <meta name="csrf-token" content="{{ csrf_token() }}">
    ```
    - Cho vào main.js
    ```php
    $.ajaxSetup({
    headers: {
        'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')
    }
    });
    ```
    - Viết code xử lý delete
    ```js
    function removeRow(id, url) {
    if (confirm('Xoá mà không thể khôi phục. Bạn có chắc ?')) {
        $.ajax({
            type: 'DELETE',
            datatype: 'JSON',
            data: {id},
            url: url,
            success: function (result) {
                if (result.error === false) {
                    alert(result.message)
                    location.reload();
                } else {
                    alert('Xoá lỗi vui lòng thử lại')
                }
            }
        })
    }

    }
    ```
## Bài 15, 16: Menu sửa & cập nhật
```php
public function show(Menu $menu)
```
- Các viết này nó sẽ tự động kiểm tra xem trong DB xem id có tồn tại không, nếu k có sẽ lỗi
## Bài 18: Product upload thumb
- Sử dụng ajax để làm 

