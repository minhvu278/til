# Hiểu Container & Image

# Image là gì?
- Image giống như 1 **Bản thiết kế** hoặc **Hộp đồ chơi đóng gói sẵn**. Nó chứa tất cả những gì cần để tạo ra 1 thứ gì đó (như game, ứng dụng) mà không cần làm lại từ đầu
- Ví dụ: Hãy nghĩ đến bộ LEGO ngôi nhà. Khi bạn mua về, bạn có 1 hộp LEGO với đầy đủ các mảnh ghép và hướng dẫn lắp. Image chính là cái hộp đó - Nó sẵn sàng để bạn **mở ra chơi**
- Trong Docker, Image chứa
  - Phần mềm (Như game xếp hình)
  - Công cụ hỗ trợ
  - Hướng dẫn cài đặt

# Container là gì?
- Container giống như **Ngôi nhà LEGO đã lắp xong** từ Image (Bản thiết kế). Khi bạn "mở hộp" và sắp xếp theo hướng dẫn, bạn có 1 thứ có thể dùng ngay - đó là container
- Ví dụ: Bạn lấy hộp LEGO "Ngôi nhà" (Image), xếp thành ngôi nhà hoàn chỉnh (Container). Bây giờ bạn có thể chơi với ngôi nhà đó, mang đi đâu cũng được
- Trong Docker, Container là lúc bạn "chạy: Image, biến nó thành 1 thứ đang hoạt động (Như game đang được mở lên màn hình)

# Image & Container khác nhau như thế nào?
- **Image**: Là *hộp đồ chơi chưa mở*, đứng yên, không hoạt động. Bạn có thể copy nó, gửi cho bạn bè
- **Container**: Là *đồ chơi đã mở & đang chơi*, đang hoạt động. Tắt đi là hết nhưng có thể mở lại từ image bất cứ lúc nào
- Ví dụ
  - Image: Hộp LEGO đóng gói trên kệ
  - Container: Ngôi nhà LEGO đa xếp xong, để lên bàn để chơi

# Docker làm gì với Image & Container
## Tạo Image
- Bạn viết hướng dẫn (gọi là `Dockerfile`) để đóng gói phần mềm vào hộp
  - VD lấy game xếp hình, thêm âm thanh, nút bấm, đóng hộp lại
- Dùng lệnh docker build để tạo Image

## Chạy container
- Bạn mở hộp image ra để chơi, chạy lệnh `docker run`

# Tại sao Image & Container lại quan trọng
- Dễ bế đi: Image nhỏ gọn
- Chạy nhanh: Container mở ra là chạy được ngay, không cần cài lại từ đầu
- Tiết kiệm: 1 Image có thể tạo ra được nhiều container

# Thực hành basic
- Cài đặt Docker
- Thử Image có sẵn
  - Mở terminal
  - Gõ `docker run hello-world`
  - Kết quả: Bạn sẽ thấy 1 tin nhắn "Hello from Docker!". Đây là Container chạy từ image `hello-word`
- Xem Image & Container
  - Gõ `docker images` để thấy `hello-world`
  - Gõ `docker ps -a` để thấy Container vừa chạy

# Thử với 1 dự án sử dụng ReactJs
- Giả sử chúng ta sẽ tạo 1 trang web đơn giản bằng ReactJs. Để chạy trang web, chúng ta cần
  - **ReactJS**: Thư viện chính để xây dựng trang web
  - **Node.js**: Công cụ để chạy Js (Giống như pin đồ chơi)
  - **File code**: Các file bạn viết (`App.js`, `index.js`)
  - **Cài đặt**: Cần đúng thứ tự, nếu không sẽ bị lỗi
- Nhưng nếu bạn mang code sang máy khác (Máy đồng đội trong team hoặc server), có thể máy đó thiếu Node hoặc phiên bản không khớp, dẫn đến web không chạy. Đây là lúc Docker hiện lên và giúp bạn

## Bước 1: Tạo Image cho dự án ReactJs
- Image giống như **Hộp đồ chơi** chứa mọi thứ cần để chạy trang web ReactJs
### Cách làm:
- **Viết hướng dẫn (Dockerfile)**:
  - Tạo file `Dockerfile` (Không có đuôi) trong thư mục dự án ReactJs
  ```js
  FROM node:18

  WORKDIR /app

  COPY package.json ./
  COPY package-lock.json ./
  RUN npm install

  COPY . .

  CMD ["npm", "start"]
  ```
  - `FROM node: 18`: Lấy phiên bản node 18
  - `WORKDIR /app`: Tạo 1 "Góc chơi" trong hộp
  - `COPY`: Đưa code vào hộp
  - `npm install`: Cài các công cụ cần thiết (Như React)
  - `CMD`: Khi mở hộp, chạy lệnh `npm start` để khởi động web

- **Tạo Image**: 
  - Mở terminal, cd vào thư mục dự án
  - Gõ lệnh `docker build -t react-dragonball .`
  - `-t react-dragonball`: Đặt tên hộp là "react-dragonball"
  - `.`: Dùng fie trong thư mục hiện tại
  - Kết quả chúng ta có 1 Image tên `react-dragonball`, giống hộp LEGO đã đóng gói

## Bước 2: Chạy container từ Image
- Container là lúc bạn "Mở hộp" và chạy trang web

### Cách làm:
- Gõ lệnh `docker run -p 3000:3000 react-dragonball`
  - `-p 3000:3000`: Kết nối cổng 3000 của máy bạn với cổng 3000 trong container
- Kết quả: Trang web chạy trên `http://localhost:3000`

## Bước 3: Stop container (nếu cần)
- Nếu cần dừng chạy docker, bạn hãy gõ docker-ps. Nó sẽ list ra các container đang chạy. Chúng ta chỉ cần lấy `CONTAINER ID` - ví dụ CONTAINER ID ở đây là a1b2c3d4e5f6
- Sau khi có `CONTAINER ID` rồi, chúng ta muốn dừng container thì chạy lệnh
  - `docker stop a1b2c3d4e5f6`
  - Sau đó gõ `docker ps`, chúng ta sẽ không thấy container nữa
  - `docker ps -a`: Sẽ hiển thị cả các container đã dừng
- Trường hợp nếu chúng ta muốn xoá, cho pay màu container đó
  - `docker rm a1b2c3d4e5f6`

# Ví dụ thực tế
- Giẩ sử chúng ta làm việc nhóm

## Bạn tạo dự án
- Viết code React trên máy cá nhân
- Đóng gói thành Image `react-dragonball`

## Chia sẻ với team
- Đẩy Image lên Docker Hub (như gửi hộp LEGO qua bưu điện)
- Ae trong team tải về bằng lệnh `docker pull yourname/react-dragonball`

## Chạy trên server
- Team dùng lệnh `docker run` để triển khai trang web lên server

# Điều tuyệt vời với ReactJS và Docker
- **Chạy ở mọi nơi**: Windows, Linux hay Mac đều chạy ngon lành, miễn là có Docker
- **Không lo lỗi cài đặt**: Image chứa Node.js, react & code - Không cần cài thủ công
- **Nhanh chóng**: Chỉ cần `docker run`, trang web sẽ chạy
