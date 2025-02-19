# Quản lý dịch vụ trên server
- Bây giờ, khi đã quen với Linux, chúng ta cần học cách cài đặt và quản lý các dịch vụ quan trọng trên server gồm
- Nginx/Apache (Web server)
- MySQL/MariaDB/PostgreSQL (Database server)
- Redis (Cache)
- Node.js/PHP/Laravel (Chạy ứng dụng web)
- Quản lý dịch vụ với systemctl

# Web Server: Cài đặt & Cấu hình Nginx
- Web server chịu trách nhiệm xử lý yêu cầu từ trình duyệt và trả về trang web. Có 2 loại phổ biến
  - Nginx
    - Nhanh, nhẹ, hỗ trợ nhiều kết nối
    - Nhưng cấu hình khó
  - Apache
    - Dễ cài đặt, phổ biến
    - Tốn tài nguyên hơn Nginx
- Chúng ta sẽ dùng Nginx, vì nó mạnh và tối ưu hơn Apache
## Cài đặt Nginx trên ubuntu
```sh
sudo apt update
sudo apt install nginx -y
```
## Khởi động & kiểm tra Nginx
```sh
sudo systemctl start nginx   # Bắt đầu chạy Nginx
sudo systemctl enable nginx  # Cho phép chạy tự động khi reboot
sudo systemctl status nginx  # Kiểm tra trạng thái
```
- Bạn có thể mở trình duyệt & nhập địa chỉ IP server để kiểm tra. Nếu thấy trang `Welcome to Nginx` nghĩa là đã thành công
## Cấu hình Virtual Host cho website
- Mở file cấu hình
```sh
sudo nano /etc/nginx/sites-available/default
```
- Thay đổi nội dung
```sh
server {
    listen 80;
    server_name yourdomain.com;

    root /var/www/html;
    index index.html index.php;

    location / {
        try_files $uri $uri/ =404;
    }
}
```
- Lưu file (Ctrl + X, Y, Enter), rồi restart Nginx
```sh
sudo systemctl restart nginx
```

# Database Server: Cài đặt & Quản lý MySQL
## Cài đặt MySQL Server
```sh
sudo apt install mysql-server -y
```
## Bảo mật MySQL
```sh
sudo mysql_secure_installation
```
- Nó sẽ hỏi:
  - Đặt mật khẩu cho `root`
  - Xoá user ẩn danh
  - Cấm truy cập root từ xa
  - Xoá database test
- Truy cập vào MySQL
```sh
sudo mysql -u root -p
```
- Tạo DB và user
```sh
CREATE DATABASE mydb;
CREATE USER 'admin'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON mydb.* TO 'admin'@'localhost';
FLUSH PRIVILEGES;
```
- Thoát MySQL
```sh
EXIT;
```
# Cài đặt Redis Cache
- Redis giúp tăng tốc ứng dụng bằng cách lưu dữ liệu vào bộ nhớ RAM
## Cài đặt
```sh
sudo apt install redis-server -y
```
- Kiểm tra xem redis có đang chạy không
```sh
sudo systemctl status redis
```
- Mở redis CLI để kiểm tra
```sh
redis-cli
```
- Nhập lệnh
```sh
set name "Hello Redis"
get name
```
- Nếu nó trả về name trên nghĩa là Redis đã hoạt động
# Cài đặt các phần liên quan như node, php,...
- Ví dụ cài đặt Nodejs & npm
```sh
sudo apt install nodejs npm -y
node -v
npm -v
```

