# Overview
- Để sử dụng thành thạo server, cần học theo từng bước từ cơ bản đến nâng cao sau
## Hiểu về Server & hệ điều hành
- Tìm hiểu khái niệm về server và hệ điều hành của nó
- Làm quen với các hệ điều hành phổ biến trên server: Linux (Ubuntu, CentOS, Debian) và Windows Server

## Làm quen với Linux (Quan trọng nếu dùng VPS hoặc cloud)
- Học các lệnh cơ bản trong Linux (cd, ls, mkdir, rm, cp, mv,...)
- Hiểu về quyền user, quản lý file, thư mục và quyền truy cập (chmod, chown)
- Quản lý tiến trình (ps, kill, htop)
- Cách sử dụng SSH để truy cập server từ xa (Lệnh ssh trên terminal)

## Quản lý dịch vụ trên Server
- Cách cài đặt và quản lý các dịch vụ: Apache/Nginx, MySQL/MongoDB, Redis, Node.js, PHP/Laravel
- Cách khởi động/dừng dịch vụ (`systemctl start/stop/restart`)
- Đọc log lỗi (journalctl, tail -f /var/log/...)

## Làm việc với Network & Firewall
- Kiểm tra kết nối (ping, netstat, curl, traceroute)
- Cấu hình firewall (ufw, iptables)
- Cấu hình domain & DNS (dig, nslookup)

## Triển khai ứng dụng lên Server
- Cách deploy 1 website (HTML, PHP, React, Nextjs) lên server
- Cấu hình Nginx/Apache làm web server
- Cài đặt SSL (HTTPS) với Let's Encrypt

## Bảo mật Server
- Đổi port SSH, cài đặt Fail2Ban để chống brute-force
- Tạo user và quản lý quyền với sudo
- Backup dữ liệu (dùng rsync, scp, cronjob)

## Làm việc với Cloud & Containerization
- Làm quen với AWS, Google Cloud, Azure
- Tìm hiểu về Docker & Kubernetes
