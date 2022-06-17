# Json Web Token
- Định nghĩa 1 cách nhỏ gọn, khép kín để truyền thông tin 1 cách an tòan giữa các bên dưới dạng JSON 
- Có thể được xác minh và đáng tin vì nó chứa dãy số
- Vd: JWT Token 
    ```css 
    eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjEzODY4OTkxMzEsImlzcyI6ImppcmE6MTU0ODk1OTUiLCJxc2giOiI4MDYzZmY0Y2ExZTQxZGY3YmM5MGM4YWI2ZDBmNjIwN2Q0OTFjZjZkYWQ3YzY2ZWE3OTdiNDYxNGI3MTkyMmU5IiwiaWF0IjoxMzg2ODk4OTUxfQ.uKqU9dTB6gKwG6jQCuXYAiMNdfNRw98Hw_IWuA5MaMo
    ```
- Tuy nhìn khác phức tạp nhưng đơn giản là cấu trúc của JWT như sau 
    ```css
    <base64-encoded header>.<base64-encoded payload>.<base64-encoded signature>
    ```

- JWT là sự kết hợp(Bởi dấu .) 
    - 1 `Object Header` được định dạng JSON đươc encode base64.
    - 1 `payload` object dưới định dạng JSON được encode base64 
    - 1 `Signature` cho URL cũng được mã hóa dưới dạng base64 

- 3 thành phần của JWT 
    - Header : Gồm 2 phần chính 
        - Loại token (mặc định là JWT - Cho biết đây là 1 Token JWT)
        - Dùng thuật toán để mã hóa (HMAC SHA256 - HS256 hoặc RSA).
            ```json
            {
                "alg": "HS256",
                "typ": "JWT"
            }
            ```
    - Payload : Chứa các claims 
        - Claims là 1 biểu thức về 1 thực thể(Ví dụ như `user`) và 1 số metadata phụ trợ. Có 3 loại claims thường gặp trong payload: `reserved`, `public` và `private claims` 
            - Reserved claims: Là 1 số metadata được định nghĩa trước trong đó có 1 số là bắt buộc còn lại phải tuân theo để JWT hợp lệ và đủ thông tin:  `iss (issuer), iat (issued-at time) exp (expiration time), sub (subject)`
            - VD: 
                ```json
                {
                    "iss": "jira:1314039",
                    "iat": 1300819370,
                    "exp": 1300819380,
                    "qsh": "8063ff4ca1e41df7bc90c8ab6d0f6207d491cf6dad7c66ea797b4614b71922e9",
                    "sub": "batman",
                    "context": {
                        "user": {
                            "userKey": "batman",
                            "username": "bwayne",
                            "displayName": "Bruce Wayne"
                        }
                    }
                }
                ```

                ```json 
                {
                    "iss": "scotch.io",
                    "exp": 1300819380,
                    "name": "Chris Sevilleja",
                    "admin": true
                }
                ```

        - Public Claims: Được công nhận và sử dụng rộng rãi

        - Private Claims: Claims tự định nghĩa, không trùng với 2 cái bên trên. Tạo ra để chia sẻ thông tin giữa 2 parties đã thỏa thuận và thống nhất trước đó 
        
    - Signature
        - Là 1 chuỗi được mã hóa bởi header, payload cùng với 1 chuỗi bí mật theo nguyên tắc 
            ```json 
                HMACSHA256(
                base64UrlEncode(header) + "." +
                base64UrlEncode(payload),
                secret)
            ```
        - Do Signature đã bao gồm cả header và payload nên Signature có thể dùng để kiểm tra tính toàn vẹn của dữ liệu khi truyền tải 

- 1 số trường hợp sử dụng JWT 
    - Authentication: Khi user login mỗi request tiếp theo sẽ đính kèm chuỗi token JWT cho phép truy cập đường dẫn được phép ứng với token đó 
    - Infomation Exchange: JWT cũng là 1 cách hữu hiệu và bảo mật để trao đổi thông tin giữa nhiều ứng dụng. 
        - Vì JWT phải sử dụng cặp public/private key nên không hoặc khó có thể mạo danh bằng JWT  
        - Cấu trúc của JWT đơn giản nên JWT có thể dễ dàng bị decode vì thế nên ta không nên dùng JWT để transfer các thông tin nhạy cảm 
    
- JWT sử dụng như thế nào 
    - Khi user đăng nhập thành công (Browser sẽ post username & password về Server) -> Server sẽ trả về 1 chuỗi JWT về browser -> Token JWT này cần được lưu lại trong Browser người dùng(LocalStorage hoặc Cookie). Thay vì cách truyền thống tạo 1 session trên Server và trả về cookie 

    - Bất cứ khi nào mà `User` muốn đăng nhập vào Route được bảo vệ(User đã đăng nhập), Browser sẽ gửi token JWT này trong header Header Authorization, Bearer schema của request gửi đi 
        ```
        Authorization: Bearer <token>
        ```
    - Đây gọi là trạng thái stateless(phi trạng thái) authentication làm việc trạng thái của user không được lưu trong bộ nhớ của server mà được đóng gói hẳn vào trong JWT - Server sẽ kiểm tra Token JWT có hợp lệ không 