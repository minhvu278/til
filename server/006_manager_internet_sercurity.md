# Quản lý mạng & bảo mật server
- Khi vận hành 1 server, bảo mật là ưu tiên hàng đầu để tránh bị tấn công. Dưới đây là các bước để **bảo vệ và quản lý mạng trên server**

# Cấu hình tường lửa (Firewall)
- Firewall giúp chặn các truy cập không mong muốn vào server
- Kiểm tra firewall có đang hoạt động không
```sh
sudo ufw status
```
  - Nếu là inactive thì là đang hoạt động
- Bật firewall và cho phép các dịch vụ quan trọng
```sh
sudo ufw allow OpenSSH  # Cho phép kết nối SSH
sudo ufw allow 80       # Mở cổng HTTP (truy cập website)
sudo ufw allow 443      # Mở cổng HTTPS (SSL)
sudo ufw enable         # Kích hoạt tường lửa
```
- Nếu bạn đang dùng 1 ứng dụng như Nginx hoặc Apache, có thể dùng 
```sh
sudo ufw allow 'Nginx Full'  # Mở cả HTTP & HTTPS cho Nginx
```
- Nếu cần mở 1 cổng cụ thể
```sh
sudo ufw allow 3000
```

# Chặn IP không mong muốn (Fail2Ban)
- Hacker có thể đoán **mật khẩu SSH hoặc tấn công website**, vì vậy cần chặn ip có dấu hiệu xấu
- Cài đặt Fail2ban để chặn các ip đáng ngờ
```sh
sudo apt install fail2ban -y
```
- Kiểm tra trạng thái
```sh
sudo systemctl status fail2ban
```
- Tạo file cấu hình bảo vệ SSH
```sh
sudo nano /etc/fail2ban/jail.local
```
- Thêm nội dung vào
```sh
[sshd]
enabled = true
port = 22
maxretry = 5
bantime = 600
```
  - maxretry = 5 : Nếu sai mật khẩu ssh 5 lần, ip đó sẽ bị chặn
  - bantime = 600 : Chặn ip đó trong 10 phút
- Lưu file và restart lại
```sh
sudo systemctl restart fail2ban
```
- Xem danh sách các ip bị chặn
```sh
sudo fail2ban-client status sshd
```
- Gỡ chặn 1 ip
```sh
sudo fail2ban-client set sshd unbanip 192.168.1.100
```

# Bật xác thực bằng SSH (thay vì password)
- Để tránh bị hack mật khẩu, chỉ cho phép đăng nhập bằng ssh key thay vì mật khẩu
- Tạo ssh key trên máy tính cá nhân (nếu chưa có)
```sh
ssh-keygen -t rsa -b 4096
```
  - Nhấn Enter liên tục để tạo key
  - Mặc định, key sẽ nằm ở
  ```sh
  ~/.ssh/id_rsa (private key)
  ~/.ssh/id_rsa.pub (public key)
  ```
- Thêm ssh key vào server. Giả sử, ip server có IP 123.456.78.90, chạy lệnh
```sh
ssh-copy-id user@123.456.78.90
```
- Nếu không có `ssh-copy-id`, có thể làm thủ công
```sh
cat ~/.ssh/id_rsa.pub | ssh user@123.456.78.90 "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

## Tắt đăng nhập bằng mật khẩu (Chỉ dùng SSH key)
- Mở cấu hình ssh
```sh
sudo nano /etc/ssh/sshd_config
```
- Tìm dòng
```sh
PasswordAuthentication yes
```
- Sửa thành
```sh
PasswordAuthentication no
```
- Lưu file và restart SSH
```sh
sudo systemctl restart ssh
```
- **Lưu ý**: Mất ssh key, bạn sẽ không thể truy cập vào được server

# Giới hạn truy cập SSH
- Không nên đăng nhập bằng user `root`, vì tài khoản này quá dễ đoán
- Tạo user mới thay vì dùng root
```sh
sudo adduser myuser
sudo usermod -aG sudo myuser  # Cấp quyền sudo
```
## Cấm root SSh
- Mở file `/etc/ssh/sshd_config`
```sh
sudo nano /etc/ssh/sshd_config
```
- Tìm dòng
```sh
PermitRootLogin yes
```
- Sửa thành
```sh
PermitRootLogin no
```
- Lưu và restart SSH
```sh
sudo systemctl restart ssh
```

# Cấu hình HTTPS với SSL free (Let's Encrypt)
- Khi chạy website, ta cần `SSH (HTTPS)` để bảo mật dữ liệu giữa người dùng và server
- Cài đặt Certbot (Let's Encrypt)
```sh
sudo apt install certbot python3-certbot-nginx -y
```
- Cấp SSL cho website (Nginx)
```sh
sudo certbot --nginx -d mywebsite.com -d www.mywebsite.com
```
- Nếu thành công, website của bạn sẽ chạy HTTPS
- Tự động gia hạn SSL
```sh
sudo certbot renew --dry-run
```
- Chạy lệnh này mỗi tháng để kiểm tra
