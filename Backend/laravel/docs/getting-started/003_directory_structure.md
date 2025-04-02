> https://laravel.com/docs/12.x/structure

# Introduction
- Cấu trúc default mà Laravel cung cấp được tạo ra để bạn dễ dàng bắt đầu, dù làm dự án lớn hay nhỏ. Tuy nhiên không cần phải tuân thủ theo cấu trúc mặc định, bạn có thể tự do sáng tạo cách tổ chức code, miễn là hệ thống vẫn chạy được

# The Root Directory

## The App Directory
- `app` chứa mã cốt lõi của ứng dụng. Hầu hết các class trong ứng dụng của bạn sẽ nằm trong thư mục này

## The Bootstrap Directory
- `bootstrap` chứa file `app.php` dùng để khởi động framework. Folder `cache` trong đó giúp ứng dụng chạy nhanh hơn bằng cách lưu sẵn 1 số dữ liệu thay vì tính toán lại từ đầu mỗi lần

## The Config Directory
- Đúng như với tên gọi, nó chứa all các file cấu hình của ứng dụng. Nên đọc qua các file này

## The Database Directory
- `database` chứa các file migration của db, factory của model và các seed. Cũng có thể sử dụng để lưu 1 CSDL SQLite

## The Public Directory
- Folder public chứa file index.php. Đây là điểm khởi đầu cho tất cả các request gửi đến ứng dụng của bạn và cũng là nơi cấu hình autoloading. Nó còn chứa các asserts như image, js, css

## The Resources Directory
- Chứa các views, nội dung thô chưa biên dịch như Js CSS

## The Routes Directory
- `routes` directory chứa all các định nghĩa route cho app. Theo mặc định sẽ gồm `web.php` và `console.php`
- File `web.php` chứa các route mà Laravel đặt trong `web` middleware group, cung cấp session state, bảo vệ CSRF và mã hoá cookie. Nếu ứng dụng của bạn không phải là 1 API Resful không stateless tức là nó cần lưu trữ thông tin như session, thì bạn sẽ dùng web.php. API Resful stateless thường không dùng section mà dùng token được định nghĩa trong api.php
- `console.php` định nghĩa các lệnh (commnads) chạy trên console. Các command này được viết dưới dạng closure (hàm vô danh trong PHP). Mỗi closure được gắn với 1 command instance, giúp bạn dễ dàng sử dụng các method nhập/xuất (IO method) như in ra màn hình hoặc nhận data từ người dùng (VD có thể sử dụng $this->info() để in thông báo trong console). File console.php không dùng để định nghĩa các route HTTP như trong web.php mà định nghĩa các "điểm vào" cho ứng dụng qua console. Đây là lệnh bạn chạy bằng php artisan. Bạn có thể lên lịch (Schedule) cho các tác vụ trong file này (VD chạy 1 lệnh vào 1 thời điểm nhất định)
  ```php
  use Illuminate\Support\Facades\Artisan;

  Artisan::command('say:hello', function () {
      $this->info('Xin chào từ console!');
  });
  ```
  - Chạy trong terminal: php artisan say:hello
- "Optionally", bạn có thể thêm các route files ngoài 2 file mặc định
  - api.php: Dùng để định nghĩa các route cho API
  - channels.php: Dùng để định nghĩa các channels cho tính năng broadcasting (gửi thông báo realtime như chat)
- Để tạo các file này, bạn có thể sử dụng Artisan: `php artisan install:api`, `php artisan install:broadcasting`
- Các request vào qua `api.php` được xác thực bằng token thay vì dùng cookie hay session như website thông thường. Các route trong này không sử dụng được session vì chúng thuộc nhóm middleware api
- Channels là các kênh mà ứng dụng dùng để phát sóng các event. Bạn định nghĩa ở đây để kiểm soát xem ai được phép nghe (listen) kênh nào

## The Storage Directory
- Thư mục `storage (lưu trữ)` như 1 kho lớn, bên trong chia làm 3 ngăn nhỏ: 1 ngăn cho `app`, 1 ngăn cho hệ thống Laravel (framework), 1 ngăn để ghi lại logs (`Storage là nơi lưu trữ mọi thứ: logs, file hệ thống, file của bạn`). 
- Tưởng tượng `app` là nơi tự do để đồ của mình, `framework` là nơi Laravel tự quản lý đồ của nó, `logs` ghi lại mọi hoạt động
- `storage/app/public` dùng để lưu trữ các file do người dùng tạo ra mà bạn muốn truy cập công khai (ảnh, avatar người dùng). Để những file này có thể truy cập được thông qua browser, bạn cần tạo 1 `symbolic link` (liên kết tượng trưng) từ thư mục `/public/storage` trỏ đến `storage/app/public`. Cần chạy lệnh `php artisan storage:link` để tự động tạo liên kết

## The Tests Directory
- Chứa các automated tests của ứng dụng Laravel. Laravel cung cấp sẵn các ví dụ về:
  - `unit tests`: Kiểm tra từng phần nhỏ trong code
  - `feature tests`: Kiểm tra các tính năng lớn hơn
  - Các test này dùng công cụ `Pest` hoặc `PHPUnit`
- Quy tắc đặt tên: Mỗi class phải có đuôi là `Test` (VD UserTest, LoginTest,...)
- Cách để chạy test: Chạy `./vendor/bin/pest` hoặc `./vendor/bin/phpunit` trong terminal để chạy các test. Nếu muốn kết quả đẹp hơn thì chạy `php artisan test`, lệnh này giúp kết quả dễ nhìn hơn

## The Vendor Directory
- `vendor` chứa all các thư viện, dependencies mà ứng dụng sử dụng. Composer là công cụ quản lý thư viện trong PHP, khi cài đặt 1 thư viện, nó sẽ được tải về trong thư mục vendor

# The App Directory
- `app` là nơi chứa phần lớn code mà bạn viết. Mọi thư mục trong `app` mặc định được đặt trong namespace App (Hay Namespace App là họ của các file tronng đó). Điều này giúp tổ chức code tránh xung đột với các thư viện khác (1 file User.php trong app/Models sẽ có tên đầy đủ là `App\Model\User`). Composer autoload các file trong thư mục app theo chuẩn PSR-4. Nghĩa là bạn không cần phải tự tay include từng file, Composer sẽ làm điều đó giúp bạn

