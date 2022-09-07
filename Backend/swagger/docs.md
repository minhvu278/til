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
    - **Swagger-Editor**: Dùng để design lên các APIs hoàn toàn mới hoặc edit lại các APIs có sẵn thông qua 1 file config 
    - **Swagger-Codegen**: Dùng để generate ra code từ các file config có sẵn 
    - **Swagger-UI**: Dùng để generate ra file html,css,... từ 1 file config

- Có thể vào http://petstore.swagger.io/ để demo xem swagger như nào
    - Với mỗi API có thể biết được chi tiết input và output cũng như trường nào bắt buộc gửi lên, kết quả trả về có thể nhận những status nào
    - Đặc biệt có thể input data để kiểm tra kết quả 

# Cấu trúc cơ bản của swagger 
- Xem cấu trúc cơ bản tại link: https://editor.swagger.io
- 1 file swagger có thể viết bằng JSON hoặc YAML 
    - **Metadata**: Mọi thông số kỹ thuật đều bắt đầu với phiên bản Swagger(Xác định cấu trúc tổng thể đặc tả API - Những gì có thể ghi lại và cách ghi lại nó). Ngoài ra các thông tin chi tiết như tiêu đề, mô tả, version đều được ghi ở đây 
    - **Base Url**: Định nghĩa host của serve, đường dẫn cơ bản và giao thức https và http
    - **Consumes & Produces**: Xác định các loại `MINE` được hỗ trợ 
    - **Paths**: Là phần chứa các thông tin API trông như nào bằng đường dẫn API, các phương thức, các request, response 

# API Host and Base Url
- Rest APIs có 1 url cơ sở mà các đường dẫn điểm cuối được nối vào. - - Đường dẫn URL này được định nghĩa bởi `schema, host, basePath`.
