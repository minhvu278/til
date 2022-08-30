# CSRF Protection

## Ngăn chặn các Request CSRF
- Laravel sẽ tự động tạo ra 1 mã `CSRF "token"` cho mỗi phiên của người dùng 
    - Mã này để xác minh người dùng được xác thực là người thực sự đưa ra yêu cầu đối với ứng dụng 
    - Lưu trữ trong phiên của người dùng & thay đổi mỗi khi session được tạo lại 
    - Ứng dụng độc hại bên ngoài sẽ không truy cập được nó 

- Bất cứ khi nào sử dụng `"POST", "PUT", "PATCH", or "DELETE"` nên thêm 1 CSRF hidden `_token` để middleware bảo vệ CSRF có thể xác thực yêu cầu 
    - Để thuận tiện thì ta cũng có thể sử dụng `@csrf`để tạo trường nhập trường `hidden token`
        ```php
        <form method="POST" action="/profile">
            @csrf
        
            <!-- Equivalent to... -->
            <input type="hidden" name="_token" value="{{ csrf_token() }}" />
        </form>
        ```

## X-CSRF-TOKEN
- Ngoài việc kiểm tra mã dưới dạng tham số POST, ta có thể lưu token trong thẻ `meta` của html
    ```php
    <meta name="csrf-token" content="{{ csrf_token() }}">
    ```
    - Sau đó ta dùng các thư viện Jquery để thêm token vào all request header 
    ```php
    $.ajaxSetup({
        headers: {
            'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')
        }
    });
    ```
