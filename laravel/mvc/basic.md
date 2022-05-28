# Mô hình mvc
- `htaccess`: Đóng vai trò như bảo vệ của serve, dữ liệu muốn vào phải thông qua nó 
    - RewriteEngine On
    - RewriteRule ^(.+)$ index.php?url=$1
