# Networking trong Docker là gì?
- Networking là cách Docker giúp các container liên lạc với nhau hoặc với máy tính/internet bên ngoài
- Ví dụ trong dự án ReactJs, bạn cần FE hỏi BE để lấy danh sách người dùng chẳng hạn. BE sẽ đi hỏi DB để lấy dữ liệu. `Networking` làm cầu nối cho việc này

# Tại sao cần Networking
- Nếu không có mạng, các container giống như những hộp đồ chơi bị cô lập
  - ReactJs không thể lấy dữ liệu từ BE
  - BE không lấy dữ liệu được từ DB
  - Người dùng không thể truy cập được vào trang web từ trình duyệt
- **Docker Networking** bôi trơn giúp  mọi thứ kết nối trơn chu

# Các loại Networking cơ bản trong Docker
- Docker có 1 vài loại "Đường dây chính"

## Bridge (cầu nối)
- Mặc định khi chạy container
- Giống như việc chúng ta bắn half-life, chúng ta có thể chơi với nhau qua mạng nội bộ
- VD: FE, BE, DB trong `docker-compose.yml` dùng mạng bridge để liên lạc

## Host
- Container dùng thẳng network của máy tính, không cần cầu nối
- VD: Trang React chạy thẳng trên cổng máy của bạn, nhanh hơn nhưng không cô lập

## None
- Container không có dây, hoàn toàn cô lập

# Ví dụ thực tế với ReactJs + Networking
- Chúng ta sẽ sử dụng lại ví dụ ở phần docker compose
- Khi chạy `docker-compose up` với file `docker-compose.yml`
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
```
- **Mạng tự động**: Docker Compose tạo ra 1 mạng "bridge" mặc định gọi là (`project_default`) để 3 container buôn dưa lê với nhau
- **Tên gọi**: FE gọi BE bằng tên `backend`, BE gọi DB bằng `database`
- **Cổng (Ports)**: 
  - `3000:3000` Nối FE từ container ra máy của bạn (localhost:3000)
  - `5000:5000` Nối BE ra ngoài
  - `27017:27017` Nối DB ra ngoài

## Thử connect
- FE gọi BE: Chúng ta sẽ fetch dữ liệu trong `App.js`
```js
fetch("http://backend:5000/heroes")
  .then(res => res.json())
  .then(data => console.log(data));
```
  - **backend:5000** là tên nội bộ trong mạng Docker, không cần dùng localhost
- BE gọi DB: Trong `server.js`, dùng Mongo
```js
const mongoose = require('mongoose');
mongoose.connect('mongodb://database:27017/api', { useNewUrlParser: true });
```
- `database:27017`: Là tên MongoDB trong mạng

# Thực hành thủ công với Networking
- Nếu không dùng Docker Compose, bạn có thể tạo mạng & chạy container riêng lẻ
## Tạo mạng
- Nhập `docker network create my-network`
- Đây là đường dây mới tên "my-network"

## Chạy container với mạng
- Chạy MongoDB
```
docker run --name db --network my-network -p 27017:27017 mongo
```
- Chạy BE
```
docker run --name backend --network my-network -p 5000:5000 my-backend-image
```
- Chạy FE
```
docker run --name frontend --network my-network -p 3000:3000 my-frontend-image
```

## Kiểm tra connect
- Backend gọi `db:27017` để lấy dữ liệu Mongo
- FE gọi `backend:5000` để lấy list

# Điều tuyệt vời với Networking
- **Dễ gọi nhau**: Container dùng tên (như `backend, database`) thay vì ip
- **An toàn**: Mạng bridge cô lập container ra khỏi máy tính, chỉ mở cổng bạn muốn (Như 3000)
- **Linh hoạt**: Có thể tạo nhiều network cho nhiều dự án


