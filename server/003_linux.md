# Làm quen với Linux & các lệnh cơ bản
- Hầu hết các server trên internet chạy Linux
- Linux nhẹ, bảo mật, free và hỗ trợ tốt cho lập trình web, backend
- Để quản lý server, bạn phải dùng câu lệnh thay vì UI như Windows
  - VD: Khi bạn thuê 1 server VPS, bạn sẽ quản lý nó bằng cách kết nối SSH và gõ lệnh thay vì click chuột như trên windows

# Cách connect vào Server Linux qua SSH
- Nếu bạn có 1 server (hoặc VPS), bạn sẽ dùng SSH để kết nối từ máy tính cá nhân
- Trên windows sử dụng PowerShell hoăc phần mềm PuTTY
- Trên MacOS/Linux sử dụng terminal có sẵn
```
ssh user@server-ip
```
- VD
```
ssh root@192.168.1.100
```
- `root` là user quản trị cao nhất trên Linux
- `192.168.1.100` là địa chỉ IP của server
- Nếu thành công, bạn sẽ thấy dấu nhắc lệnh (prompt) của Linux
```
root@server:~#
```

# Các lệnh Linux cơ bản cần biết
- Sau khi connect vào server, bạn sẽ làm việc với CLI thay vì UI

## Quản lý file và thư mục
- `ls`: Liệt kê file và thư mục hiện tại
- `ls -l`: Hiển thị chi tiết (Kích thước, quyền, ngày tạo)
- `cd <tên thư mục>`: Di chuyển vào thư mục
- `pwd`: Hiển thị thư mục hiện tại
- `mkdir <tên thư mục>`: Tạo thư mục mới
- `rm <tên file>`: Xoá file
- `rm -r <tên file>`: Xoá thư mục và tất cả các file bên trong
- `cp <file nguồn< <file đích>`: Sao chép file
- `mv <file nguồn< <file đích>`: Di chuyển hoặc đổi tên file

## Quản lý user & quyền truy cập
- `whoami`: Xem user hiện tại
- `adduser <tên user>`: Thêm user mới
- `passwd <tên user>`: Đổi mật khẩu user
- `su <tên user>`: Chuyển sang user khác
- `sudo <lệnh>`: Chạy lệnh với quyền admin
- `chmod 777 <file>`: Thay đổi quyền truy cập file
- `chown user:user <file>`: Đổi chủ sở hữu file
- Ví dụ: Tạo user admin, đặt pass cho user, rồi chuyển sang user đó
```
adduser admin
passwd admin
su admin
whoami
```
## Quản lý tiến trình & tài nguyên hệ thống
- `top`: Xem các tiếnt trình đang chạy
- `htop`: Xem tiến trình đẹp hơn (Cần cài: `sudo apt install htop)
- `ps aux`: Xem danh sách tiến trình đang chạy
- `kill <PID>`: Dừng 1 tiến trình theo ID
- `free -h`: Kiểm tra RAM
- `df -h`: Kiểm tra dung lượng ổ đĩa
- `uptime`: Kiểm tra thời gian hoạt động của server

## Quản lý mạng & kiểm tra kết nối
- `ifconfig/ip a`: Kiểm tra địa chỉ ip của server
- `ping <tên miền/IP`: Kiểm tra kết nối đến 1 server khác
- `netstat -tulnp`: Xem các cổng đang mở
- `curl <URL>`: Kiểm tra response của 1 trang web
- `wget <URL>`: Tải 1 file từ internet
- VD kiểm tra kết nối đến GG: `ping google.com`

# Tự động hoá với Cronjob
- Cronjob là hệ thống giúp tự động chạy lệnh theo lịch trình
- Cấu trúc của cronjob
```
* * * * * lệnh_cần_chạy
- - - - -
| | | | |
| | | | |_____ Thứ trong tuần (0 - 7) (0 và 7 là Chủ Nhật)
| | | |_______ Tháng (1 - 12)
| | |_________ Ngày trong tháng (1 - 31)
| |___________ Giờ (0 - 23)
|_____________ Phút (0 - 59)
```
- VD: Mở trình chỉnh sửa cronjob
```
crontab -e
```
- Thêm dòn này để chạy script `/home/user/backup.sh` mỗi ngày lúc 2h sáng
```
0 2 * * * /home/user/backup.sh
```

# Summary
- Học cách kết nối vào server
- Chạy lệnh Linux cơ bản để quản lý file, user, tiến trình & mạng
- Biết cách tự động hoá công việc với cronjob


