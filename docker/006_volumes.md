# Volumes trong Docker là gì?
- Volumes là cách Docker lưu dữ liệu lâu dài bên ngoài container, giống như việc bạn lưu điểm số cao nhất của game để lần sau chơi tiếp mà không bị mất
- Ví dụ trong dự án của bài trước, bạn không muốn mất list danh sách dữ liệu lấy từ BE khi tắt container. Volumes giúp chúng ta làm điều đó

# Tại sao cần Volumes?
- Container giống như "Hộp đồ chơi tạm thời". Khi bạn tắt nó (`docker stop` hoặc `docker-compose down`), mọi thứ bên trong (dữ liệu, file) thường bị xoá sạch
- Với Volumes, bạn gắn 1 cái két sắt vào container để giữ dữ liệu an toàn, dù container có tắt hay bị xoá

# Cách volume hoạt động
- **Volumes**: Là két sắt nằm ngoài container, trên máy tính hoặc server
- **Gắn vào container**: Bạn nói Docker "Cất dữ liệu của MongoDB vào két sắt này"
- **Kết quả**: Dữ liệu vẫn nguyên vẹn qua nhiều lần bật tắt container