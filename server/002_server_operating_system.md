# Hiểu về Server & hệ điều hành
## Server là gì
- Server (máy chủ) là hệ thống máy tính chuyên dụng được thiết kế để cung cấp dữ liệu, dịch vụ hoặc tài nguyên cho các thiết bị khác (gọi là client) thông qua internet hoặc mạng nội bộ
- Ví dụ thực tế
  - Khi bạn truy cập vào 1 trang web như Google.com, trình duyệt gửi yêu cầu đến server Google, server sẽ phản hồi bằng trang web hiển thị trên màn hình của bạn
  - Khi xem video trên YTB, server YTB sẽ gửi dữ liệu video đến thiết bị của bạn để bạn xem trực tiếp mà không cần download

## Các loại server phổ biến
- Có nhiều loại server, mỗi loại phục vụ 1 mục đích khác nhau
  - `Web Server`: Dùng để chạy các website (VD: Nginx, Apache)
  - `Database Server`: Lưu trữ và quản lý dữ liệu (MySQL, PostgresSQL, MongoDB)
  - `File Server`: Dùng để lưu trữ và chia sẻ file (GG Drive, Dropbox)
  - `Application Server`: Chạy các ứng dụng web và API (Nodejs, PHP, Laravel)

## Server hoạt động như thế nào?
- Hãy tưởng tượng server như 1 nhà hàng và client là khách hàng
  - Khi bạn (client) vào nhà hàng, bạn gọi món (gửi request)
  - Đầu bếp (server) nhận đơn, chuẩn bị món ăn (xử lý yêu cầu)
  - Phục vụ mang món ăn đến cho bạn  (trả về kết quả)
- Tương tự, khi bạn truy cập 1 website
  - Trình duyệt của bạn gửi request đến server (HTTP request)
  - Server xử lý yêu cầu, lấy dữ liệu từ DB nếu cần
  - Server gửi lại trang web (HTML, CSS, JS) để trình duyệt hiển thị

# Hệ điều hành trên Server
- Quản lý các tài nguyên, phần mềm và dịch vụ. Có 2 loại phổ biến

## Linux (Phổ biến nhất)
- Hơn 90% server trên thế giới sử dụng Linux vì:
  - Miễn phí, nhẹ, bảo mật cao
  - Tốn ít resource hơn Windows
  - Hỗ trợ tốt cho lập trình web, API, DB

- Các phiên bản Linux phổ biến
  - `Ubuntu Server` - Dễ dùng, phổ biến nhất
  - `CentOS/Rocky Linux` - Ổn định, dùng nhiều cho doanh nghiệp
  - `Debian` - Nhẹ, bảo mật cao

- Làm quen với Linux
  - Linux không có UI đồ hoạ như Windows, chúng ta làm việc qua CLI (Command Line Interface)
  - Truy cập vào server qua SSH (Secure Shell) bằng lệnh
  ```
  ssh user@server-ip
  ```

## Windows Server (Ít phổ biến hơn)
- Có giao diện giống windows thông thường
- Thường dùng cho các phần mềm chạy trên nền tảng Microsoft như ASP.NET, SQL Server
- Không phổ biến bằng Linux vì tốn phí và sử dụng resource nhiều hơn

# Mua và cấu hình Server
- Nếu muốn thực hành, thuê 1 server nhỏ (VPS - Virtual Private Server) từ các nhà cung cấp như:
  - `DigitalOcean` - Dễ dùng, rẻ
  - `Vultr` - Giá tốt
  - `AWS EC2` - Dùng thử free 12 tháng
- Cũng có thể cài sử dụng máy tính làm server bằng cách
  - Cài đặt Ubuntu Server trên máy ảo để thực hành
  - Hoặc dùng WSL (Windows Subsystem for Linux) nếu dùng windows

# Summary
- Server là máy tính chuyên dụng, phục vụ dữ liệu cho client
- Linux là hệ điều hành phổ biến nhất cho server
- Có thể thực hành với 1 VPS hoặc máy ảo trên máy tính cá nhân