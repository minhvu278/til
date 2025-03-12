# Docker Compose - Quản lý nhiều Container

# Docker Compose là gì?
- Là công cụ giúp bạn chạy & quản lý nhiều container cùng lúc
- Ví dụ: Bạn có 1 hộp "Xếp hình" và hộp "Máy nghe nhạc". Bình thường bạn phải mở từng hộp riêng lẻ. Docker Compose mở cả 2 cùng lúc, đảm bảo chúng "nói chuyện" được với nhau

# Tại sao cần Docker Compose
- Với 1 dự án ReactJs, 1 trang web không chỉ có React mà còn các phần khác:
  - **ReactJs**: Giao diện (FE)
  - **Backend**: Xử lý dữ liệu
  - **Database**: Lưu trữ dữ liệu
- Nếu bạn chạy riêng lẻ bằng `docker run`, bạn phải gõ lệnh cho từng container & kết nối chúng thủ công. Docker sẽ giúp bạn làm tất cả trong 1 lần

# Ví dụ thực tế: Xây dựng dự án ReactJS với Backend và Database
- ReactJs
- Node.js
- MongoDB

## Cách làm với Docker Compose
### Tạo file cấu hình (docker-compose.yml)
- Tạo file tên `docker-compose.yml` trong thư mục dự án
- Nội dung file
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
- `version`: Phiên bản cú pháp của Docker Compose - Phiên bản 3 là phổ biến & tương thích tốt với Docker hiện tại
- `service`: Nơi định nghĩa các container của ứng dụng. Mỗi container gọi là 1 service
- `frontend`: Hộp chứa ReactJs, chạy cổng 3000
- `backend`: Hộp chứa Node, chạy cổng 5000, cần connect với DB 
- `database`: Hộp MongoDB, chạy cổng 27017
- `build`: Nói Docker dùng code trong thư mục frontend & backend
- `image: mongo`: Dowload hộp MongoDB sẵn có từ Docker Hub
- `depends_on`: Backend đợi database sẵn sàng trước khi chạy

### Chuẩn bị thư mục dự án
- Tạo cấu trúc thư mục
```
project/
├── frontend/         # Thư mục chứa ReactJS
├── backend/          # Thư mục chứa Node.js
└── docker-compose.yml
```

### Code cho từng phần
#### FE (ReactJs)
- Trong `frontend/`, dùng `npx create-react-app .` để tạo dự án
- Tạo `Dockerfile`
```js
FROM node:18
WORKDIR /app
COPY package.json ./
RUN npm install
COPY . .
CMD ["npm", "start"]
```

#### Backend (Node.js)
- Trong `backend/`, tạo file `server.js` đơn giản
```js
const express = require('express');
const app = express();
app.get('/api', (req, res) => {
  res.json([{ name: "Superman", power: "Fly" }]);
});
app.listen(5000, () => console.log("Backend running"));
```
- Tạo file `package.json`
```js
{
  "name": "backend",
  "scripts": { "start": "node server.js" },
  "dependencies": { "express": "^4.17.1" }
}
```
- Tạo `Dockerfile`
```js
FROM node:18
WORKDIR /app
COPY package.json ./
RUN npm install
COPY . .
CMD ["npm", "start"]
```

### Chạy tất cả bằng Docker Compose
- Mở terminal trong thư mục `project/`
- Gõ : `docker-compose up`
- Kết quả
  - ReactJS chạy trên `http://localhost:3000`
  - Backend chạy trên `http://localhost:5000/api`
  - MongoDB chạy ngầm, sẵn sàng lưu dữ liệu

# Điều tuyệt vời với Docker Compose
- **Chạy cùng lúc**: Một lệnh `docker-compose up` mở 3 hộp (frontend, backend, database)
- **Kết nối dễ dàng**: Container tự "nói chuyện" với nhau (React gọi backend, backend gọi database)
- **Tắt gọn gàng**: Chạy `docker-compose down` để dừng tất cả
```
[Frontend - port 3000]  <---> Người dùng
      |
      v
[Backend - port 5000]  <---> MongoDB (port 27017)
```
