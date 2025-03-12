# Docker là gì?
- Hãy tưởng tượng chúng ta có 1 bộ đồ chơi LEGO. 
  - Mỗi lần chơi chúng ta phải lấy ra từng mảnh rồi sau đó ghép lại thành hình, rồi xong lại tháo cất đi. 
  - Nhưng nếu chúng ta chơi ở nhà bạn hoặc ở công ty chúng ta phải mang hết tất cả các mảnh đi, đôi khi sẽ bị thiếu mất 1 vài mảnh khiến bộ LEGO của chúng ta sẽ không thành hình được. Khá là rắc rối đúng không ?
- **Docker** - giống như chiếc **hộp kì diệu**. Chúng ta lắp xong -> Bỏ vào hộp. Sau đó bế đi muôn nơi - ra nhà bạn, đến công ty - chỉ cần mở ra, LEGO nguyên vẹn, không sợ thiếu hay mất công lắp lại. **Docker** cũng làm tương tự vậy

# Docker hoạt động như thế nào?
- Trên máy tính, để chạy 1 phần mềm (Như các ứng dụng hoặc game), bạn cần cài rất nhiều thứ như: vào đúng trang để download, ứng dụng cần công cụ nào hỗ trợ để cài, cài đặt đúng cách,.... Nếu chúng ta mang phần mềm sang máy khác, đôi khi nó sẽ không chạy vì máy đó sẽ bị thiếu thứ gì đó (Giống như việc thiếu mảnh lego ở trên vậy)
- Docker **đóng gói** tất cả mọi thứ cần thiết để chạy phần mềm vào 1 `container` (hay gọi là hộp kì diệu như bên trên). Trong container có:
  - Phần mềm (như ứng dụng hoặc game)
  - Các công cụ hỗ trợ (hướng dẫn cài đặt, chơi game,...)
  - Cách sắp xếp để mọi thứ để chạy (Như bản thiết kế LEGO)
- Khi chúng ta bế container này sang máy khác, nó vẫn sẽ chạy được ngon lành vì mọi thứ đã có hết ở bên trong

## Ví dụ đơn giản
- Giả sử chơi game "Xếp hình". Chúng ta cài ở máy cá nhân, nhưng muốn chơi cả ở trên máy tính ở công ty. Bình thường là chúng ta lại phải lên tải về, cài đặt & tải thêm 1 vài thứ nữa để có thể chơi được. Và đổi khi chỉ cần thiếu 1 thứ gì đó là không chạy được
- Với Docker, chúng ta bỏ game vào `container`. Trong container này chứa
  - Game "Xếp hình"
  - Âm thanh, hình ảnh đính kèm
  - Hướng dẫn để máy tính biết cách chạy
- Bạn ném container đó vào  USB, khi lên công ty, chúng ta chỉ cần chạy container là có thể chơi được luôn mà không cần cài thêm gì

# Tại sao docker lại hữu ích?
- Dễ bế đi
- Chạy được ở mọi nơi
- Tiết kiệm thời gian

# Các tính năng chính của Docker
## Containerization - Đóng gói mọi thứ vào 1 chỗ
- Đóng gói tất cả mọi thứ, lúc cần chỉ cần mở ra để dùng. Giống ví dụ game "Xếp hình bên trên"

## Portability - Chạy được ở mọi nơi
- Chúng ta có mang đi mọi nơi để chạy ngon lành, không cần lo máy có phù hợp không
- Ví dụ như máy ở nhà dùng windown, máy công ty dùng MAC, mở ra vẫn chơi ngậy

## Lightweight - Nhẹ, nhanh
- Docker không giống như việc mang cả cái cây máy tính đi. Nó chỉ mang những thứ cần thiết nên rất nhẹ và nhanh
- Ví dụ thay vì chúng ta bế cả cái cây đi, chúng ta chỉ cần mang 1 cái USB nhỏ chứa container của docker, cắm vào xong - Easy

## Resource Efficiency- Tiết kiệm resource
- Cho phép bạn dùng 1 máy tính để chạy nhiều container cùng lúc. Giống như việc chơi nhiều game khác nhau mà không cần nhiều máy
- Ví dụ trên cùng 1 máy tính, bạn chơi thâp cẩm các trò: Xếp hình, đua xe, lol mà không bị chậm

## Reproducibility - Dễ thay đổi nếu lỗi
- Nếu ứng dụng bị lỗi, chỉ cần lấy bản sao y nguyên từ container mà không phải làm lại từ đầu
- Ví dụ: Nếu game lỗi, xoá đi, lấy lại container từ Docker, mở ra lại như mới

## Modularity - Chia nhỏ công việc
- Docker cho phép tách từng phần nhỏ của ứng dụng thành các container nhỏ để dễ quản lý hơn
- Ví dụ như trong 1 trang web có thể chia thành các container nhỏ như hình ảnh, nút, text. Mỗi container sẽ chạy riêng, hỉng cái nào fix cái đó

## Collaboration - Làm việc nhóm dễ dàng
- Mọi người trong team có thể dùng chung Docker, ai cũng có thể lấy được các container giống nhau để dùng hoặc chỉnh sửa

## Isolation - An toàn hơn
- Mỗi container trong Docker là riêng biệt, nên nếu 1 container lỗi, các container khác sẽ không bị ảnh hưởng

## Docker Hub & Tools - Dễ quản lý với tools
- Docker có 1 store gọi là Docker Hub, nơi có sẵn các container để chúng ta có thể download. Ngoài ra nó còn có tools giúp chúng ta sắp xếp gọn gàng hơn

# ROADMAP
## Hiểu về hệ điều hành & cách cài đặt phần mềm
## Làm quen với Docker
- Cài đặt & chạy thử các lệnh cơ bản
## Hiểu Container & Image
- Container là **hộp kì diệu**, Image là **Bản thiết kế**
- Tạo file đơn giản bằng `Dockerfile`
- Chạy lệnh từ Image bằng `docker build` và `docker run`
## Làm việc với Linux

## Quản lý nhiều Container (Docker compose)
- Chạy nhiều container cùng lúc
- Học viết `docker-compose.yml`
- Thử lệnh `docker-compose up`

## Kết nối mạng (Networking)
- Tìm hiểu lệnh `docker network`
- Thử kết nối 2 container (Như web & CSDL)

## Lưu dữ liệu (Volumes)
- Cách giữ đồ trong container, không bị mất khi tắt đi
- Học lệnh `docker volume` và cách gắn volume vào container

## Tìm hiểu Docker Hub & share
- Register Docker Hub
- Thử lệnh `docker pull` và `docker push`

## Học nâng cao Kubernetes
- Kubernetes giống như người quản lý, quản lý cả trăm Docker, giúp chạy nhiều docker cùng 1 lúc
- Bắt đầu với Minikube (Phiên bản mini của Kubernetes) để thử
- Cách chạy nhiều container trên cloud