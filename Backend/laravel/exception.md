# Exceptions trong laravel 
- Thông thường khi code nếu có lỗi xảy ra nó sẽ trả về  `"Whoops, something went wrong"` hoặc có thể tệ hơn là để lộ source code dẫn đến trải nghiệm không tốt cho môi trường product - Vì thế nên ta cần sử dụng kỹ thuật xử lý ngoại lệ 
- 1 ví dụ đơn giản là làm 1 chức năng search user 
    - Khi tìm id user có tồn tại thì ok, ngon trả ra view ổn - Nhưng mà khi tìm đến 1 id không tồn tại trong DB thì nó sẽ trả ra thông báo lỗi `Try to get property of non-object` và 1 giao diện đen xì và 1 vài dòng code báo lỗi nhìn khá chán (Lộ code)
        - Tuy nhiên thì để giấu lỗi này đi thì cũng khá dễ  đó là vào file **.env** set lại `APP_DEBUG = false` - Nó sẽ trả về trang lỗi có code = 500 với message lỗi `"Whoops, something went wrong on our servers."` 
        - Cũng có 1 cách cũng khá nhanh và đơn giản đó là thay **find()** thành **findOrFail()** - Nó sẽ trả về page 404 cùng với dòng text `"Sorry, the page you are looking for could not be found."`. Tuy nhiên thì page 404 này là mặc định cho từng dự án nên việc custome lại sẽ không phù hợp với từng chức năng
    - Vì thế nên cách sử lý tối ưu nhất đó là sử dụng `try catch` để xử lý exception và chuyển hướng về form với 1 message dễ hiểu 
        - Ta cần biết loại ngoại lệ và tên lớp mà nó sẽ trả về. Trong trường hợp findOrFails() nó sẽ ném ra 1 Eloquent exception là **ModelNotFoundException** 
            ```php
            public function search(Request $request)
            {
                try {
                    $user = User::findOrFail($request->input('user_id'));
                } catch (ModelNotFoundException $exception) {
                    return back()->withError($exception->getMessage())->withInput();
                }
                
                return view('users.search', compact('user'));
            }
            ```
            - Hiển thị lỗi ở view 
            ```php 
            @if (session('error'))
                <div class="alert alert-danger text-center">{{ session('error') }}</div>
            @endif
            ```
            - Nó sẽ bắn ra 1 message mặc định, ta có thể customer lại message 
            ```php
            return back()->withError('User has ID = ' . $request->input('user_id') . ' does not exist')->withInput();
            ```
## Sử dụng Services để xử lý Error message 
- Service là 1 design pattern làm cho controller đỡ cồng kềnh hơn 
//TODO:

## Cách exception hoạt động trong laravel 
- Tất cả các exception được xử lý bởi class **App\Exception\Handler**
    ```php 
    <?php

    namespace App\Exceptions;

    use Illuminate\Foundation\Exceptions\Handler as ExceptionHandler;
    use Throwable;

    class Handler extends ExceptionHandler
    {
        /**
        * A list of the exception types that are not reported.
        *
        * @var array
        */
        protected $dontReport = [
            //
        ];

        /**
        * A list of the inputs that are never flashed for validation exceptions.
        *
        * @var array
        */
        protected $dontFlash = [
            'password',
            'password_confirmation',
        ];

        /**
        * Report or log an exception.
        *
        * @param  \Throwable  $exception
        * @return void
        *
        * @throws \Exception
        */
        public function report(Throwable $exception)
        {
            parent::report($exception);
        }

        /**
        * Render an exception into an HTTP response.
        *
        * @param  \Illuminate\Http\Request  $request
        * @param  \Throwable  $exception
        * @return \Symfony\Component\HttpFoundation\Response
        *
        * @throws \Throwable
        */
        public function render($request, Throwable $exception)
        {
            return parent::render($request, $exception);
        }
    }
    ```
- Thuộc tính **$dontReport**
    - Chứa 1 mảng các kiểu exception sẽ không cần log 
    - Trong class cha của class Handler ta sẽ thấy có 1 mảng các Exception đã được thêm vào sẵn ở thuộc tính **$internalDontReport**
- Thuộc tính **$dontFlash**: 
    - Chứa 1 mảng input sẽ không bao giờ được truyền đi nếu có exception validate 
- Phương thức **report**
    - Sử dụng để log các exception hoặc gửi đến các dịch vụ bên ngoài như Bugsnag hoặc Sentry 
    - Mặc đinh thì nó chỉ đẩy các exception về class nơi mà exception được log lại - Tuy nhiên có thể tùy biến theo ý muốn 
    - Nếu cần report nhiều kiểu exception theo nhiều cách khác nhau có thể sử dụng toán tử kiểm tra của PHP `instanceof`
        ```php 
        public function report(Exception $exception)
        {
            if ($exception instanceof UserException) {
                \Log::debug('user not found');
            }
            parent::report();
        }
        ```
- Phương thức **render**: 
    - Có trách nhiệm chuyển 1 exception thành 1 HTTP response để trả lại cho trình duyệt 
    - Mặc định thì 1 exception được đẩy tới class cơ sở để tạo 1 response. Tuy nhiên có thể kiểm tra thoải mái kiểu dữ liệu exception trả về response tùy biến theo ý 
        ```php 
        public function render($request, Throwable $e)
        {
            if ($e instanceof UserException) {
                return response()->view('errors.user');
            }
            return parent::render($request, $e);
        }
        ```
## Tạo exception 
- Ta có thể tự tạo exception của riêng 
    ```
    php artisan make:exception UserException
    ```
    - Thêm vào 2 method report và render 
    - Thay vì kiểm tra các loại exception trong report và render của Handler mà ta có thể định nghĩa trong tùy chỉnh exception của bạn. Khi các phương thức đó tồn tại nó sẽ được tự động gọi đên bởi framework 
        ```php 
        <?php

        namespace App\Exceptions;

        use Exception;

        class UserException extends Exception
        {
            /**
            * Report or log an exception.
            *
            * @return void
            */
            public function report()
            {
                \Log::debug('User not found');
            }

            public function render($request)
            {
                return response()->view('errors.user');
            }
        }
        ```