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
- Docker lưu volume trong thư mục mặc định trên máy host
```
/var/lib/docker/volumes/
```
- Khi bạn gán volume vào container, Docker sẽ tạo 1 thư mục ở đó và `mount` nó vào vị trí cụ thể trong container
- Ví dụ chúng ta tạo ra 1 volume như sau
```
docker volume create mydata
```
- Sau đó, chúng ta dùng volume khi chạy container
```
docker run -d -v mydata:/app/data my_image
```
  - `mydata` là tên volume
  - `/app/data`: Thư mục bên trong container

# Ví dụ thực tế: Dự án ReactJs + Volume
- Dùng lại dự án trước, chúng ta sẽ thêm Volumes để giữ dữ liệu Mongo
```js
version: "3"
services:
  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
  backend:
    build: ./backend
    ports:
      - "5000:5000"
    depends_on:
      - database
  database:
    image: mongo
    ports:
      - "27017:27017"
    volumes:
      - mongo-data:/data/db
volumes:
  mongo-data:
```
- `volumes: - mongo-data:/data/db`
  - `mongo-data`: Tên két sắt bạn tạo
  - `/data/db`: Nơi mongoDB lưu dữ liệu trong container
- `volumes: mongo-data`: Khai báo két sắt này ở cuối file
## Chạy test thử
- Chạy dự án
  - Chạy `docker-compose up`
  - Backend thêm dữ liệu vào MongoDB
- Tắt & xoá container
  - Gõ `docker-compose down`
  - Container bị xoá những dữ liệu vẫn nằm trong `mongo-data`
- Chạy lại
  - Gõ `docker-compose up`
  - Mongo khởi động, list danh sách vẫn còn

# Cách dùng Volumes thủ công (Không sử dụng Docker Compose)
- Nếu chúng ta chạy container riêng lẻ

## Tạo Volume
- Gõ: `docker volume create mongo-db`

## Chạy container với Volume
- Gõ: `docker run --name db -v mongo-data:/data/db -p 27017:27017 mongo`
  - `-v mongo-data:/data/db`: Gán két sắt `mongo-data` và `/data/db`

## Kiểm tra
- Thêm dữ liệu, tắt container (docker stop db), bật lại (docker start db), dữ liệu vẫn còn

# Điều tuyệt vời với Volumes
- Dữ liệu bền vững: Tắt container đi nhưng không mất dữ liệu
- Dễ di chuyển: Két sắt có thể bế sang máy khác
- Tái sử dụng: Một volume có thể sử dụng cho nhiều container nếu cần