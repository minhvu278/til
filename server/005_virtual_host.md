# Cấu hình Virtual Host cho website với Nginx
- `Virtual Host` (hay Server Block trong Nginx) giúp bạn chạy nhiều website trên cùng 1 server bằng cách trỏ các domain khác nhau về thư mục riêng của chúng
- Ví dụ:
  - site1.com trỏ về /var/www/site1.com
  - site2.com trỏ về /var/www/site2.com
- Mặc định, Nginx lưu trữ file cấu hình của Virtual Host trong thư mục
  - `/etc/nginx/sites-availabel/`: Chứa file cấu hình của từng website
  - `/etc/nginx/sites-enabled/`: Chứa các Virtual Host đã được kích hoạt (được Nginx sử dụng)
- Nginx chỉ sử dụng các file nằm trong `sites-enabled` nên ta cần kích hoạt Virtual Host bằng cách tạo 1 liên kết (symlink) từ `sites-availabel/` sang `sites-enabled/`

## Bước 1: Tạo thư mục chứa website
- Giả sử, bạn muốn chạy website mywebsite.com, trước tiên cần tạo thư mục chứa file của website
```sh
sudo mkdir -p /var/www/mywebsite.com
```
- Cấp quyền cho thư mục
```sh
sudo chown -R $USER:$USER /var/www/mywebsite.com
```
- Tạo 1 file index để test
```sh
echo "<h1>Welcome to My Website</h1>" | sudo tee /var/www/mywebsite.com/index.html
```

## Bước 2: Tạo file cấu hình Virtual Host
- Mở file cấu hình Nginx
```sh
sudo nano /etc/nginx/sites-available/mywebsite.com
```
- Nhập nội dung sau
```sh
server {
    listen 80;
    server_name mywebsite.com www.mywebsite.com;

    root /var/www/mywebsite.com;
    index index.html index.php;

    location / {
        try_files $uri $uri/ =404;
    }
}
```
- `listen 80;`: Lắng nghe trên cổng 80 (HTTP)
- `server_name mywebsite.com www.mywebsite.com;`: Xử lý yêu cầu từ domain này
- `server_name mywebsite.com www.mywebsite.com;`: Xử lý yêu cầu từ domain này
- `root /var/www/mywebsite.com;` : Chỉ định thư mục chứa website
- `index index.html index.php;` : File mặc định khi truy cập
- `try_files $uri $uri/ =404;` : Nếu file không tồn tại, trả về 404

## Bước 3: Kích hoạt Virtual Host
- Chúng ta cần bật Virtual Host này bằng cách tạo 1 liên kết (symlink) đến thư mục `sites-enabled`
```sh
sudo ln -s /etc/nginx/sites-available/mywebsite.com /etc/nginx/sites-enabled/
```
- `ls -s` : Tạo 1 đường dẫn ảo từ `sites-available/` sang `sites-enabled/`
- Khi Nginx khởi động, nó chỉ đọc các file có trong `sites-enabled`, vì vậy cần tạo symlink để kích hoạt Virtual Host

## Bước 4: Kiểm tra & Restart Nginx
- Kiểm tra xem cấu hình có lỗi không
```sh
sudo nginx -t
```
- Nếu kết quả là `systax is ok`, thì restart Nginx để áp dụng cấu hình
```sh
sudo systemctl restart nginx
```

## Bước 5: Trỏ Domain về server (DNS)
- Bạn cần trỏ website  về địa chỉ ip của server bằng cách thêm bản ghi A trong quản lý DNS của domain
```sh
Loại	Tên	Giá trị
A	@	IP_SERVER
A	www	IP_SERVER
```

## Bước 6: Kiểm tra website
- Nếu đã trỏ domain xong, hãy mở trình duyệt và nhập
```sh
http://mywebsite.com


// Kết quả
Welcome to My Website
```
- Nếu bạn chưa trỏ domain, có thể chỉnh file hosts trên máy tính để test
```sh
sudo nano /etc/hosts
```
- Thêm dòng
```sh
YOUR_SERVER_IP  mywebsite.com
```
- Lưu file và thử mở http://mywebsite.com trên trình duyệt.
