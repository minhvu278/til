# OpenAPI là gì? 
- OpenAPI Specification là 1 định dạng mô tả API dành cho REST APIs. Một file OpenAPI cho phép mô tả toàn bộ API bao gồm: 
    - Cho phép những endpoints(/users) và cách thức hoạt động của mỗi endpoint(GET, POST, PUT, DELETE)
    - Các tham số đầu vào và đầu ra của từng API 
    - Phương thức xác thực 
    - Thông tin liên hệ, chứng chỉ (HTTP, HTTPS), điều khoản sử dụng và các thông tin khác 

- API Specification có thể được viết bằng YAML hoặc JSON. Định dạng này dễ đọc, dễ hiểu cho cả người dùng lẫn ngôn ngữ máy tính 

# Swagger là gì? 
- Là 1 bộ mã nguồn mở để xây dựng OpenAPI specifications giúp ta thiết kế và sử dụng REST APIs 
- Swagger cung cấp 3 tools chính cho các developers: 
    - Swagger-Editor: Dùng để design lên các APIs hoàn toàn mới hoặc edit lại các APIs có sẵn thông qua 1 file config 
    - Swagger-Codegen: Dùng để generate ra code từ các file config có sẵn 
    - Swagger-UI: Dùng để generate ra file html,css,... từ 1 file config 
- Việc viết document cho swagger có 2 cách tiếp cận chính như sau: 
    - Top-down approach: Thiết kế API trước khi code 
    - Bottom-up approach: Từ các API có sẵn thiết kế file config để mô tả chúng 
- Có thể vào http://petstore.swagger.io/ để demo xem swagger như nào
    - Với mỗi API có thể biết được chi tiết input và output cũng như trường nào bắt buộc gửi lên, kết quả trả về có thể nhận những status nào
    - Đặc biệt có thể input data để kiểm tra kết quả 

# Cấu trúc cơ bản của swagger 
- Xem cấu trúc cơ bản tại link: https://editor.swagger.io
### info 
- Mỗi OpenAPI specifications sẽ bắt đầu với từ khóa openapi để khai báo phiên bản (VD: openapi: 3.0.0) - Phiên bản này sẽ định nghĩa toàn bộ cấu trúc của API 
- Phần `info` sẽ chứa các thông tin của API 
    - title: Tên api
    - description: Thông tin mô tả API và có hỗ trợ cú pháp Markdown 
    - info: Thông tin 
    - version: Phiên bản API

### basePath
- Đường dẫn gốc đến thư mục API của project 

### tags
- Định nghĩa những tags, có thể sử dụng để gom những API trong cùng 1 controllers về 1 nhóm 
//TODO: https://topdev.vn/blog/gioi-thieu-swagger-cong-cu-document-cho-restfull-apis/

# Add swagger laravel 8
-  Cài darkaonline
    ```php
    composer require "darkaonline/l5-swagger" --ignore-platform-reqs
    // Có thể cài cho phiên bản php nào
    composer require "darkaonline/l5-swagger:5.8.*"
    ```
    - `--ignore-platform-reqs` thêm vào nếu lỗi problem
- Để sử dụng **@SWG** (Swagger Annotations)
    ```php
    composer require zircote/swagger-php
    // Mặc định sẽ sử dụng swagger phiên bản 3.0. Có thể hạ phiên bản
    composer require 'zircote/swagger-php:2.*'
    ```
- Publish L5-Swagger config and view files
    ```php
    php artisan vendor:publish --provider "L5Swagger\L5SwaggerServiceProvider"
    ```
- Thêm swagger vào Controller
    ```php
    /**
     * @OA\Info(title="My First API", version="0.1")
    * * @OA\Get(
    *     path="/",
    *     description="Home page",
    *     @OA\Response(response="default", description="Welcome page")
    * )
    */
    ```
- Generate Swagger UI
    ```
    php artisan l5-swagger:generate
    ```
    - Để mỗi lần thay đổi không cần phải gen lại thì ta set `L5_SWAGGER_GENERATE_ALWAYS=true` là đựt
- Truy cập để test api: http://localhost:8000/api/documentation
- Ví dụ đơn giản cho func store()
    ```
        /**
     * @SWG\Post(
     *   path="api/users",
     *   summary="Create A User",
     *   operationId="store",
     *   tags={"Users"},
     *   security={
     *       {"ApiKeyAuth": {}}
     *   },
     *   @SWG\Parameter(
     *       name="name",
     *       in="formData",
     *       required=true,
     *       type="string"
     *   ),
     *   @SWG\Parameter(
     *       name="email",
     *       in="formData",
     *       required=true,
     *       type="string"
     *   ),
     *   @SWG\Parameter(
     *       name="team_id",
     *       in="formData",
     *       required=true,
     *       type="integer"
     *   ),
     *   @SWG\Response(response=200, description="successful operation"),
     *   @SWG\Response(response=406, description="not acceptable"),
     *   @SWG\Response(response=500, description="internal server error")
     * )
     *
     */
    ```
    - Một số keys:
        - @SWG\Swagger: Chứa thông tin cơ bản của SW
        - Info: Thông tin cấu hình
        - SercuritySchema: Mô tả các phương thức xác thực được sử dụng trong API
        - security: API nhận access_token xác thực từ sercuritySchema