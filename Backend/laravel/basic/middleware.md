# Middleware 

## Vòng đời của laravel 
- image.png

## Middleware dùng để làm gì 
- Là thành phần trung gian nằm giữa route và controller kiểm tra request có hợp lệ không

## 1 số loại middleware 
- Nằm trong file `Kernel.php` 
    - **$middleware**: Là global - Ví dụ khi user vào hệ thống bắt buộc phải đăng nhập thì ta khai báo ở đây
    - **$middlewareGroups**: 