# Introduct
- Xử lý tất cả các yêu cầu liên quan đến người dùng như: Thêm, sửa xóa 

## Basic Controllers 
- Controller kế thừa từ base controller `App\Http\Controllers\Controller` nên các class phải `extends` nó 
    ```php
    <?php
    
    namespace App\Http\Controllers;
    
    use App\Http\Controllers\Controller;
    use App\Models\User;
    
    class UserController extends Controller
    {
        /**
        * Show the profile for a given user.
        *
        * @param  int  $id
        * @return \Illuminate\View\View
        */
        public function show($id)
        {
            return view('user.profile', [
                'user' => User::findOrFail($id)
            ]);
        }
    }
    ```
    - Ta có thể định nghĩa route đến controller này 
        ```php
        use App\Http\Controllers\UserController;
        
        Route::get('/user/{id}', [UserController::class, 'show']);
        ```
 ## Single Action Controllers
 - Sử dụng phương thức `__invoke` duy nhất trong controller 
    ```php
    <?php
    
    namespace App\Http\Controllers;
    
    use App\Http\Controllers\Controller;
    use App\Models\User;
    
    class ProvisionServer extends Controller
    {
        /**
        * Provision a new web server.
        *
        * @return \Illuminate\Http\Response
        */
        public function __invoke()
        {
            // ...
        }
    }
    ```
    - Khi đăng kí routes cho single action controller, ta không cần chỉ định method cho nó mà ta chỉ cần đưa controller vào 
        ```php 
        use App\Http\Controllers\ProvisionServer;
        
        Route::post('/server', ProvisionServer::class);
        ```
    - Có thể tạo ra 1 controller invokable(không thể xâm phạm) bằng cách sử dụng options `--invokable` trong Artisan command 
        ```
        php artisan make:controller ProvisionServer --invokable
        ```
    
# Controller Middleware 
- Middleware có thể được chỉ định cho các routes của controller 
    ```
    Route::get('profile', [UserController::class, 'show'])->middleware('auth');
    ```

- Hoặc có thể chỉ định middleware trong `constructor` của `controller`, có thể gán các middleware cho các actions của controller 
    ```php 
    class UserController extends Controller
    {
        /**
        * Instantiate a new controller instance.
        *
        * @return void
        */
        public function __construct()
        {
            $this->middleware('auth');
            $this->middleware('log')->only('index');
            $this->middleware('subscribed')->except('store');
        }
    }
    ```

# Resource controller
- 
