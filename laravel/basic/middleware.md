# Introduction 
- Middleware cung cấp 1 cơ chế thuận tiện để kiểm tra và lọc các request HTTP trước khi vào ứng dụng
    - Ví dụ như khi người dùng request vào nhưng chưa authenticated thì sẽ chuyển hướng về trang login và ngược lại 
- Ngoài xác thực ra middleware có thể thực hiện nhiều tác vụ khác nhau 
    - Có thể ghi lại các yêu cầu đến ứng dụng của bạn 
    - Có 1 số middleware bao gồm trong khuôn khổ của laravel framework: Gồm authentication & CSRF 
    - Tất cả các middleware đều nằm trong `app/Http/Middleware`

## Defining Middleware 
- Có thể tạo mới 1 middleware sử dụng `make:middleware` Artisan 
    ```
    php artisan make:middleware EnsureTokenIsValid
    ```
    - Nó sẽ tạo ra 1 new `EnsureTokenIsValid` ở trong `app/Http/Middleware`
    - Và trong middleware này sẽ chỉ cho phép truy cập vào nếu cung cấp đúng `token`, còn nếu k sẽ redirect về URL `home` 
        ```php
        <?php
 
        namespace App\Http\Middleware;
        
        use Closure;
        
        class EnsureTokenIsValid
        {
            /**
            * Handle an incoming request.
            *
            * @param  \Illuminate\Http\Request  $request
            * @param  \Closure  $next
            * @return mixed
            */
            public function handle($request, Closure $next)
            {
                if ($request->input('token') !== 'my-secret-token') {
                    return redirect('home');
                }
        
                return $next($request);
            }
        }
        ```
- Nôm na là middleware giống như ông bảo vệ muốn lấy được xe thì phải có vé 

## Middleware & Response 
- Có thể thực hiện tác vụ trước hoặc sau khi chuyển vào ứng dụng
    - Ex, Middleware sẽ xử lý 1 số tác vụ trước khi request được ứng dụng xử lý  ` before`
        ```
        <?php
 
        namespace App\Http\Middleware;
        
        use Closure;
        
        class BeforeMiddleware
        {
            public function handle($request, Closure $next)
            {
                // Perform action
        
                return $next($request);
            }
        }
        ```
    - Tuy nhiên middleware sẽ thực hiện nhiệm vụ của nó sau khi ứng dụng xử lý yêu cầu `after`
        ```
        <?php
 
        namespace App\Http\Middleware;
        
        use Closure;
        
        class AfterMiddleware
        {
            public function handle($request, Closure $next)
            {
                $response = $next($request);
        
                // Perform action
        
                return $response;
            }
        }
        ```
    
# Registering Middleware 

## Global Middleware 
- Nếu muốn chạy trong mọi request HTTP đến ứng dụng thì khai báo bên trong thuộc tính `$middleware` của class `app/Http/Kernel.php`

## Gán Middleware cho Router
- Nếu muốn gán middleware cho route cụ thể khai báo trong `$routeMiddleware`
    ```php
    protected $routeMiddleware = [
        'auth' => \App\Http\Middleware\Authenticate::class,
        'auth.basic' => \Illuminate\Auth\Middleware\AuthenticateWithBasicAuth::class,
        'bindings' => \Illuminate\Routing\Middleware\SubstituteBindings::class,
        'cache.headers' => \Illuminate\Http\Middleware\SetCacheHeaders::class,
    ];
    ```
    - Sau đó có thể gán cho router
        ```php
        Route::get('/profile', function () {
            //
        })->middleware('auth');
        ```
    - Có thể gán nhiều middleware cho 1 router 
        ```php
        Route::get('/', function () {
            //
        })->middleware(['first', 'second']);
        ```
    - Có thể chuyển tên lớp với đầy đủ điều kiện 
        ```php 
        use App\Http\Middleware\EnsureTokenIsValid;
        
        Route::get('/profile', function () {
            //
        })->middleware(EnsureTokenIsValid::class);
        ```

## Excluding Middleware 
- Khi gán middleware cho 1 group routes, đôi khi ta cần loại bỏ 1 số route ra khỏi group. Ta có thể thực hiện điều này bằng method `withoutMiddleware`
    ```php
    use App\Http\Middleware\EnsureTokenIsValid;
    
    Route::middleware([EnsureTokenIsValid::class])->group(function () {
        Route::get('/', function () {
            //
        });
    
        Route::get('/profile', function () {
            //
        })->withoutMiddleware([EnsureTokenIsValid::class]);
    });
    ```

## Middleware groups 
- Nhóm 1 số middleware dưới 1 `key` duy nhất để giúp dễ dàng hơn trong việc gán routes 
- Để làm được việc này thì ta sử dụng thuộc tính `$middlewareGroups` trong HTTP kernel 
- Laravel đi kèm với các nhóm middleware `web` & `api` chứa middleware phổ biến mà bạn có thể áp dụng cho các route `web` và `api`
- Các middleware groups được ứng dụng tự động áp dụng `App\Providers\RouteServiceProvider`
    ```php
    /**
     * The application's route middleware groups.
    *
    * @var array
    */
    protected $middlewareGroups = [
        'web' => [
            \App\Http\Middleware\EncryptCookies::class,
            \Illuminate\Cookie\Middleware\AddQueuedCookiesToResponse::class,
            \Illuminate\Session\Middleware\StartSession::class,
            \Illuminate\View\Middleware\ShareErrorsFromSession::class,
            \App\Http\Middleware\VerifyCsrfToken::class,
            \Illuminate\Routing\Middleware\SubstituteBindings::class,
        ],
    
        'api' => [
            'throttle:api',
            \Illuminate\Routing\Middleware\SubstituteBindings::class,
        ],
    ];
    ```