# Introduction 
- Tất cả các config trong laravel đều được lưu trong thư mục `config`
- Các tệp cho phép cấu hình những thứ như: CSDL, server, múi giờ, mã hóa

## Cấu hình môi trường 
- Hữu ích nếu có các cấu hình khác nhau dựa vào môi trường ứng dụng đang chạy 
- File `.env.example` xác định nhiều biến môi trường chung. Trong qúa trình cài đặt sẽ tự động copy vào file `.env`
- `.env` chứa các giá trị cấu hình phổ biến dựa trên việc máy chủ của bạn đang chạy ở local hay server 
- Bất kì biến nào trong `.env` đều có thể bị ghi đè bởi biến môi trường bên ngoài

