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
- Nếu ứng dụng có nhiều file environment (.env, .env.staging), bạn có thể chỉ định môi trường được mã hoá bằng cách cung cấp tên môi trường qua option `--env`
```
php artisan env:encrypt --env=staging
```
## Decryption
- Để giải mã (decryption) 1 environment file, bạn có thể sử dụng lệnh env:decrypt. Lệnh này yêu cầu decryption từ `LARAVEL_ENV_ENCRYPTION_KEY` environment variable:
```
php artisan env:decrypt
```
- Hoặc key có thể được cung cấp trực tiếp cho command qua option `--key`
```
php artisan env:decrypt --key=3UVsEgGVK36XN82KKeyLFMhvosbZN1aF
```
- Khi lệnh `env:decrypt` được gọi, Laravel sẽ decrypt nội dung của file `.env.encrypted` và đặt nội dung đã giải mã vào file .env
- Option `--cipher` có thể được cung cấp cho command `env:decrypt` để sử dụng mã hoá tuỳ chỉnh
```
php artisan env:decrypt --key=qUWuNRdfuImXcKxZ --cipher=AES-128-CBC
```
- Nếu ứng dụng của bạn có nhiều biến môi trường thì sử dụng
```
php artisan env:decrypt --env=staging
```
- Để ghi đè environment file hiện có, bạn có thể cung cấp option `--force` cho lệnh `env:decrypt`
```
php artisan env:decrypt --force
```

# Accessing Configuration Values
- Bạn có thể dễ dàng truy cập các giá trị config của mình bằng cách sử dụng `Config` facade hoặc global `config()` từ bất kỳ đâu trong ứng dụng của bạn. Có thể truy cập giá trị config bằng "dot", bao gồm tên file & option bạn muốn chọn. Giá trị mặc định cũng có thể được chỉ định
```php
use Illuminate\Support\Facades\Config;

// Ví dụ trong file config/app.php có dòng 'timezone' => 'UTC'
$value = Config::get('app.timezone');

$value = config('app.timezone');

// Retrieve a default value if the configuration value does not exist...
$value = config('app.timezone', 'Asia/Seoul');
```
- Để thiết lập các configuration value khi chạy, có thể sử dụng Config facade hoặc truyền 1 mảng cho config()
```php
Config::set('app.timezone', 'America/Chicago');

config(['app.timezone' => 'America/Chicago']);
```
- `Config` facade không chỉ cho phép lấy giá trị của config mà còn cung cấp các phương thức đặc biệt để lấy giá trị với kiểu dữ liệu cụ thể. Nếu config value được lấy không khớp với loại dữ liệu mong muốn, 1 exception sẽ được đưa ra
```php
Config::string('config-key');
Config::integer('config-key');
Config::float('config-key');
Config::boolean('config-key');
Config::array('config-key');
```
# Configuration Caching
- Để ứng dụng chạy nhanh hơn, bạn có thể sử dụng command `php artisan config:cache`. Lệnh này sẽ gộp tât cả các option từ nhiều file trong thư mục `config/` thành 1 file duy nhất. File này sẽ được load nhanh hơn bởi framework, thay vì đọc từng file cấu hình riêng lẻ mỗi khi app khởi động
- Bạn thường nên chạy lệnh `php artisan config:cache` trên PRD. Không nên chạy ở local vì các config thường xuyên thay đổi
- Sau khi config được lưu vào cached (`thường là bootstrap/cache/config.php`), Laravel sẽ không đọc file `.env` nữa khi xử lý các request hoặc chạy Artisan command(như php artisan server). Lúc này hàm env() chỉ có thể lấy được các environment variable từ hệ thống chứ không phải file `.env`
- Vì env() không hoạt động với file `.env` sau khi được cache, chỉ nên dùng env() trong các file config (thư mục config/). Thay vào đó, để lấy giá trị config ở bất cứ đâu trong app, hãy sử dụng `config()` (Nếu đã cache, config() sẽ lấy giá trị từ cache, nếu chưa thì lấy trong config/)
- Lệnh `config:clear` có thể được sử dụng để xoá config đã lưu trong cache config
```
php artisan config:clear
```

# Configuration Publishing
- Hầu hết các config của Laravel đều được publish trong folder `config` của app; tuy nhiên, 1 số config như `cors.php` và `view.php` không được publish theo mặc định vì hầu hết các app sẽ không bao giờ cần sửa đổi chúng
- Tuy nhiên, bạn có thể sử dụng Artisan command `config:publish` để publish bất kỳ config nào không được publish theo mặc định
```php
php artisan config:publish

php artisan config:publish --all
```

# Debug Mode
- Option `debug` trong `config/app/php` quyết định mức độ chi tiết thông tin lỗi được hiển thị cho người dùng khi có lỗi xảy ra. Theo mặc định, option này dựa vào `APP_DEBUG` trong file .env. Trong lúc code nên để là true, lên PRD nên để false để tránh dữ liệu nhạy cảm

# Maintenance Mode
- Khi ứng dụng của bạn ở chế độ maintenance mode tất cả các request gửi đến ứng dụng sẽ hiển thị 1 UI custom thay vì hoạt động như bình thường. Điều này giúp bạn dễ dàng tạm tắt ứng dụng khi đang update hoặc maintain. Laravel sẽ tự động kiểm tra maintenance mode trong middleware mặc định, và nếu ứng dụng đang ở chế độ này, nó sẽ trả về lỗi HTTP 503. Bạn có thể bật maintenance mode bằng `php artisan down`
- Khi bật maintenance mode bằng `php artisan down`, có thể sử dụng thêm option `--refresh` để gửi Header `Refresh` trong response HTTP, yêu cầu trình duyệt tự động làm mới trang sau 1 số giây nhất định. Ngoài ra cũng có thể sử dụng option `retry` để đặt Header `Retry-After`, báo cho browser hoặc client thử lại sau bao lâu, dù Header này thường được bỏ qua

## Bypassing Maintenance Mode
- Có thể sử dụng thêm option `--secret` để tạo 1 secret token, cho phép ai đó truy cập ứng dụng mà không bị ảnh hưởng đến maintenance mode
```
php artisan down --secret="1630542a-246b-4b66-afa1-dd72a4c43515"
```
- Sau khi truy cập URL với token này, Laravel sẽ cấp 1 cookie đặc biệt cho browser, giúp bạn truy cập app bình thường
```
https://example.com/1630542a-246b-4b66-afa1-dd72a4c43515
```
- Bạn cũng có thể để Laravel tự tạo token bằng `--with-secret`
```
php artisan down --with-secret
```
- Khi bạn truy cập vào URL chứa token, Laravel sẽ chuyển hướng về trang chủ (/) của ứng dụng. Sau đó nhờ cookie đã được cung cấp, bạn có thể duyệt ứng dụng như bình thường
  - Khi 1 trình duyệt có cookie bypass, bạn có thể sử dụng ứng dụng mà không bị ảnh hưởng bởi maintenance mode, như thể chưa từng bị tắt
  - Secret token chỉ nên chứa (a-z A-Z), (0-9) và có thể có -. Tránh dùng ký tự đặc biệt như `&, ?` vì chúng có ý nghĩa đặc biệt trong URL, có thể gây lỗi

## Maintenance Mode on Multiple Servers
- Theo mặc định, Laravel dùng hệ thống dựa trên file để bật chế độ bảo trì, yêu cầu bạn sử dụng lệnh `php artisan down` trên từng server riêng lẻ (`Khi chạy down, laravel sẽ tạo file storage/framework/down` trên server. Nếu có 3 server riêg lẻ, sẽ phải chạy từng cháu). Tuy nhiên, Laravel cũng hỗ trợ cách dựa trên cache, chỉ cần chạy lệnh 1 lần trên 1 server, miễn là bạn cấu hình cache chung (shared cache) cho tất cả các server trong .env. Cần chỉnh sửa trong file `.env` bằng cách thêm 2 biến
```
APP_MAINTENANCE_DRIVER=cache
APP_MAINTENANCE_STORE=database
```
  - Ví dụ có 2 server A và B. Đảm bảo cả 2 đều dùng chung 1 Redis server

## Pre-Rendering the Maintenance Mode View
- Khi chạy down trong quá trình deploy, người dùng vẫn có thể gặp 1 số lỗi trong 1 số trường hợp (Quá trình cập nhật code hay composer i). Lỗi xảy ra khi người dùng truy cập ứng dụng đúng lúc đang cập nhật các dependency Composer. Lý do Laravel cần khởi động (boot) một phần lớn framework để:
  - Kiểm tra xem app có ở chế độ bảo trì ko (dựa vào file `storage/framework/down`)
  - Render trang bảo trì bằng công cụ templating (như Blade)
- Nếu composer dependency chưa sẵn sàng (Vd file class bị thiếu), quá trình khởi động sẽ thất bại và gây lỗi (thay vì hiển thị trang bảo trì)

- Để giải quyết vấn đề này, Laravel cho phép bạn render trước 1 trang maintain được trả về ngay đầu chu kỳ request, trước khi framework khởi động đầy đủ (Trang này không cần Blade hoặc dependency chỉ là HTML tĩnh hoặc template đơn giản). Trang pre-rendered được hiển thị trước bất kỳ dependency nào (như Composer, database) được tải nên tránhd được lỗi thiếu dependency. Bạn có thể tuỳ chọn template để pre-render bằng option `--render` khi chạy down
```
php artisan down --render="errors::503"
```
  - `errors::503` trỏ đến file `resources/views/errors/503.blade.php`

## Redirecting Maintenance Mode Requests
- Khi ở maintenance mode, mọi URL mà người dùng truy cập sẽ hiển thị trang bảo trì mặc định. Nếu muốn bạn có thể yêu cầu Laravel chuyển hướng đến 1 URL cụ thể thay vì hiển thị trang bảo trì. Dùng option `--redirect` khi chạy down
```
php artisan down --redirect=/
```

## Disabling Maintenance Mode
- Để tắt chế độ bảo trì, đưa ứng dụng trở lại
```
php artisan up
```
  - Hành động này sẽ xoá file `storage/framework/down` hoặc status cache và ứng dụng sẽ hoạt động bình thường


## Customizing Maintenance Mode Template
- Có thể tuỳ chỉnh trang bảo trì mặc định bằng cách tạo file `resources/views/errors/503.blade.php`
  ```
  <!-- resources/views/errors/503.blade.php -->
  <h1>Đang bảo trì</h1>
  <p>Chúng tôi sẽ quay lại sớm!</p>
  ```

## Maintenance Mode and Queues
- Khi ở chế độ bảo trì, các job trong hàng đợi (queued job) sẽ không được xử lý. Khi chạy up mới hoạt động bình thường

## Alternatives to Maintenance Mode
- Vì chế độ bảo trì gây ra downtime (thời gian app ngừng hoạt động), bạn có thể cân nhắc sử dụng nền tảng như Laravel Cloud để triển khai mà không bị gián đoạn

