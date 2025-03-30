> https://laravel.com/docs/12.x/configuration

# Introduction
- Tất cả các file config cho Laravel đều được lưu trữ trong thư mục `config`. Mỗi option đều được ghi lại, vì vậy có thể thoải mái xem qua các file và làm quen với các option có sẵn.
- Các file config này cho phép bạn cấu hình những thứ như kết nối database, your mail server, cũng nhiều config khác như URL ứng dụng và encryption key

## The about command
- Laravel có thể hiển thị overview về config, drivers và environment của ứng dụng của bạn thông qua Artisan command
```
php artisan about
```
- Nếu bạn chỉ quan tâm đến một phần cụ thể, bạn có thể filter bằng `--only` option
```
php artisan about --only=environment
```
- Hoặc để khám phá chi tiết các giá trị của file cấu hình cụ thể, có thể sử dụng lệnh `config:show`
```
php artisan config:show database
```

# Environment Configuration
- Thường hữu ích khi có các giá trị cấu hình khác nhau dựa trên environment mà ứng dụng đang chạy. Ví dụ, bạn có thể sử dụng ` "cache driver" (công cụ lưu trữ tạm thời) khác khi làm việc ở local (local) so với khi chạy trên PRD server
- Để dễ dàng hơn, laravel sử dụng thư viện PHP DotEnv. Trong cài đặt Laravel mới, thư mục gốc của ứng dụng của bạn sẽ chứa file `.env.example` định nghĩa nhiều biến môi trường phổ biến. Trong quá trình cài đặt Laravel, file này sẽ được tự động copy vào `.env`
- File `.env` mặc định của Laravel chứa 1 số cấu hình chung có thể khác nhau phụ thuộc vào ứng dụng của bạn đang chạy ở môi trường nào. Các giá trị này sau đó được đọc bởi các file config bằng cách sử dụng hàm env của Laravel.
- Nếu đang phát triển với 1 team, thường sẽ giữ các biến thường dùng trong `.env.example` để các dev khác có thể biết các biến nào cần thiết để chạy ứng dụng
  - Bất kỳ biến nào trong file `.env` của bạn đều được ghi đè bởi các biến môi trường bên ngoài như system-level hoặc environment variables


## Environment File Security
- File `.env` của bạn không nên cố định vì mỗi dev có thể có các yêu cầu môi trường khác nhau. Hơn nữa, đây sẽ là một rủi ro bảo mật, có thể bị hacker có quyền truy cập và kiểm soát mã nguồn của bạn, vì vậy thông tin nhạy cảm sẽ bị lộ
- Tuy nhiên, bạn có thể mã hoá file môi trường của mình bằng `environment encryption`. Environment encryption có thể được đưa vào kiểm soát nguồn 1 cách an toàn

## Additional Environment Files
- Trước ứng dụng Laravel bắt đầu sử dụng các biến môi trường (như thông tin DB, cache,...), nó sẽ kiểm tra xem có các biến `APP_ENV` nào được cung cấp từ bên ngoài hay không. Dựa vào đó, Laravel sẽ quyết định load file `.env` nào để dùng
  - Nếu có file `.env.[APP_ENV]` (ví dụ: `.env.production`), nó sẽ dùng file đó
  - Nếu không tìm thấy file phù hợp, nó sẽ dùng file `.env` mặc định

# Environment Variable Types
- Tất cả các giá trị trong .env mà bạn viết đều được Laravel đọc dưới dạng string. Tuy nhiên, để hỗ trợ nhiều kiểu dữ liệu khác (Như boolean, null), Laravel có 1 số giá trị đặc biệt mà bạn sẽ dùng với hàm `env()`, nó sẽ tự động chuyển đổi thành kiểu dữ liệu phù hợp
- Nếu cần định nghĩa biến môi trường có giá trị khoảng trắng, có thể thực hiện bằng cách đặt giá trị trong dấu ngoặc kép
```
APP_NAME="My Application"
```
# Retrieving Environment Configuration
- Tất cả các biến được liệt kê trong file .env sẽ được load vào `$_ENV` PHP super global khi ứng dụng nhận được request. Tuy nhiên, bạn có thể sử dụng hàm env để lấy giá trị từ các biến này trong file cấu hình của bạn. Trên thực tế, nếu bạn xem lại các file cấu hình Laravel, bạn sẽ thấy nhiều option đã sử dụng tính năng này
```php
'debug' => env('APP_DEBUG', false),
```
- Giá trị thứ 2 được truyền vào hàm env là giá trị mặc định.

# Determining the Current Environment
- Environment hiện tại được xác định thông qua biến `APP_ENV` từ file .env (Như local, PRD, STG). Có thể truy cập giá trị này thông qua environment method trên App facade (Có thể lấy giá trị này hoặc kiểm tra môi trường bằng cách sử dụng method `environment()`)
```php
use Illuminate\Support\Facades\App;

$environment = App::environment();
```
  - $environment sẽ chứa giá trị của `APP_ENV` ("local")
- Cũng có thể truyền đối số cho environment method để xem environment có khớp với giá trị nhất định hay không.
```php
if (App::environment('local')) {
    // The environment is local
}

if (App::environment(['local', 'staging'])) {
    // The environment is either local OR staging...
}
``` 
  - Có thể ghi đè giá trị trong `APP_ENV` trong file `.env` bằng cách đặt 1 biến `APP_ENV` ở cấp server. Ví dụ nếu server đặt `APP_ENV=production` thì dù .env có ghi APP_ENV=local, ứng dụng vẫn dùng production

# Encrypting Environment Files
- Các environment file không được mã hoá không bao giờ được lưu trữ trong hệ thống quản lý mã nguồn (git). Tuy nhiên, Laravel cho phép bạn mã hoá file .env để bạn có thể thêm nó vào source control 1 cách an toàn cùng với các phần khác của ứng dụng

## Encryption
- Để mã hoá environment file, bạn có thể sử dụng `env:encrypt`
```php
php artisan env:encrypt
```
- Chạy lệnh env:encrypt sẽ mã hoá file .env của bạn và đặt nội dung được mã hoá vào file`.env.encrypt` chứa nội dung đã mã hoá. Khoá giải mã (decryprtion key) sẽ được hiển thị trong kết quả lệnh, có thể lưu trữ nó vào nơi an toàn. Cũng có thể tự cung cấp khoá mã riêng bằng cách cung cấp option `--key`, nhưng khoá phải có độ dài phù hợp với thuật toán mà Laravel dùng
```
php artisan env:encrypt --key=3UVsEgGVK36XN82KKeyLFMhvosbZN1aF
```
