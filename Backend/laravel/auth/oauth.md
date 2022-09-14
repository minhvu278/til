# OAuth 
- Ứng dụng: Tính năng liên kết giữa các mạng xã hội 
VD: Đăng ảnh FB mà IG nhìn được thì cần liên kết tài khoản - Để đảm nhiệm vai trò tính năng liên kết này sử dụng OAuth 
## Auth không phải là xác thực 
- Auth thực ra không phải viết tắt của xác thực - `Authentification` mà là `Authorization` - cấp phép 
    - **Authentification**: Xác nhận 1 đối tượng là ai
    - **Authorization**: Cho phép đối tượng được cấp quyền làm 1 việc nào đó - Tức là chỉ định mới được làm
- Chữ O có thể hiểu là viết tắt của open
## Token 
- Cần có quy tắc cho việc cấp quyền, nếu không có quy tắc hay quy định gì thì sẽ dễ bị tấn công từ bên ngoài
- Sử dụng access token - Là token biển thị request được cho phép (Vai trò giống như chìa khóa) - token này được authorization server cấp cho client application
- OAuth 2.0 được tiêu chuẩn hóa theo RFC6749 - quy trình response một access token request đã được tiêu chuẩn hóa
    - OAuth được sử dụng trong việc liên kết SNS (các tài khoản SNS khác như Twitter, Tumblr, v.v) bởi nó là thủ tục để 1 application có được những thông tin mong muốn
    - Server của application sẽ được nhận access token thông qua API & tiến hành phân tích token - Nếu được cấp phép server sẽ xử lý và trả về các thông tin cần thiết

## Mối quan hệ của OAuth và OpenID
- Việc cấp quyền bằng cách sử dụng OAuth rất tiện lợi nhưng không phải là vạn năng. Việc không có chức năng login thể hiện sự tạm thời, không ổn định. Chính vì vậy, OAuth 2.0 được mở rộng, thêm vào chức năng xác thực và get thuộc tính, trở thành phương pháp liên kết ID với tên gọi OpenID Connect.

- Ở đây, hãy lưu ý OpenID Connect và OpenID 2.0 có chung một phần tên gọi, nhưng đây là 2 khái niệm khác nhau. OpenID có tên gọi chính thức là OpenID Authentication, là việc chia sẻ xác thực người dung thông qua Internet.

- Khi một người dung đồng thời sử dụng nhiều application và website, việc quản lý nhiều bộ thông tin userID, password rất phiền phức.

- OAuth và OpenID là những kỹ thuật được sử dụng nhằm tiếp cận mục đích này.