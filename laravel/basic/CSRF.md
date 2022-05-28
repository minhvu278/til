# CSRF Protection

## Gỉai thích về lỗ hổng bảo mật 
- Ví dụ trong ứng dụng có 1 route `/user/email` có method là `POST` để thay đổi địa chỉ email của người dùng đã xác thực. Route này yêu cầu 1 field nhập email mới. Nếu không có CSRF thì 1 trang web có thể tạo 1 biểu mẫu HTML trỏ đến đường dẫn `/user/email` của ứng dụng và gửi email của hách cơ 
