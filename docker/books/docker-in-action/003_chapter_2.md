# Part 1: Process isolation and environment-independent computing
- Cách ly là ý tưởng chính trong nhiều mô hình tính toán, cách quản lý resource và theo dõi sử dụng. Nó quan trọng đến mức khó liệt kê hết. Ai học được cách container Linux cách lý chương trình và sử dụng Docker để kiểm soát nó có thể tái sử dụng tốt, tiết kiệm resource và làm hệ thống đơn giản 1 hwon
- Phần khó nhất khi học cách áp dụng container là dịch các nhu cầu của phần mềm mà bạn đang cố gắng cô lập. Các chương trình khác nhau có các yêu cầu khác nhau. Dịch vụ web khác với text editor, package manager, compilers hoặc database. Các container cho mỗi chương trình đó sẽ cần cấu hình khác nhau
- Phần này bao gồm các nguyên tắc cơ bản về cấu hình và vận hành container. Nó mở rộng thành các cấu hình container chi tiết hơn để chứng minh toàn bộ khả năng. Vì lý do đó, chúng tôi khuyên bạn nên cố gắng chống lại sự thôi thúc bỏ qua. Có thể mất thời gian để đi đến câu hỏi cụ thể mà bạn đang nghĩ đến, nhưng chúng tôi tin rằng bạn sẽ có được nhiều khám phá hơn trong suốt quá trình này

# Chapter 2: Running software in containers
- **This chapter covers**
  - Chạy các chương trình terminal tương tác và deamon trong các container
  - Các lệnh & thao tác Docker cơ bản
  - Cô lập các chương trình với nhau và injecting configuration
  - Chạy nhiều chương trình trong 1 container
  - Container bền và vòng đời của container
  - Cleaning up

- Trước khi kết thúc chương này, bạn sẽ hiểu tất cả những điều cơ bản để làm việc với container và cách kiểm soát việc cô lập quy trình cơ bản bằng Docker. Hầu hết ví dụ trong cuốn sách này đều sử dụng phần mềm thực tế. Các ví dụ thực tế sẽ giúp giới thiệu các tính năng của Docker và minh hoạ cách bạn sẽ sử dụng chúng trong các hoạt động hằng ngày. Sử dụng image có sẵn làm giảm thời gian học cho người dùng mới. Nếu bạn có phần mềm muốn chứa trong container và đang vội, thì phần 2 có thể sẽ trả lời nhiều câu hỏi trực tiếp hơn của bạn.
- Trong chương này, bạn sẽ cài đặt 1 server web có tên là NGINX. Web server là chương trình giúp các file và chương trình của trang web có thể truy cập được bằng trình duyệt web qua mạng. Bạn sẽ không xây dựng 1 trang web, nhưng bạn sẽ cài đặt và khởi động máy chủ web với Docker

## 2.1 Controlling containers: Building a website monitor
- Giả sử 1 khách hàng mới bước vào văn phòng của bạn và đưa ra yêu cầu vô lý là xây dựng cho họ 1 tran web mới: Họ muốn 1 trang web được giám sát chặt chẽ. Khách hàng cụ thể này muốn tự vận hành hoạt động của họ, vì vậy họ sẽ muốn giải pháp bạn cung cấp để gửi email cho nhóm của họ khi máy chủ dừng hoạt động. Họ cũng đã nghe về phần mềm máy chủ web phổ biến này có tên là NGINX và yêu cầu cụ thể bạn sử dụng nó. Sau khi đọc về những ưu điểm khi làm việc với Docker, bạn đã quyết định dùng nó trong dự án này. Hình 2.1 hiển thị kiến trúc bạn dự định cho dự án
![2.1 three container example](./images/2.1-example-container-nginx.png)
- Ví dụ này sử dụng 3 container. Cái đầu tiên chạy NGINX; cái thứ 2 sẽ chạy 1 chương trình gọi là *mailer*. Cả 2 đều sẽ chạy như các container tách biệt. *Detached* (Tách biệt) có nghĩa là các container sẽ chạy ở chế độ nền, mà không được gắn vào bất kỳ luồng đầu vào hoặc đầu ra nào (Container chạy ở chế độ nền - background, không hiển thị kết quả trực tiếp trên terminal). Một chương trình thứ 3 có tên là *watcher* sẽ chạy như 1 tác nhân giám sát trong 1 interactive container (Watcher - một script giả định để theo dõi hệ thống. interactive container - container tương tác, có thể nhập lệnh & thấy kết quả trực tiếp trên terminal. Khác với detached, interactive gắn với terminal để bạn điều khiển). Cả tác nhân gửi mail và tác nhân theo dõi đều là các file nhỏ được tạo trong ví dụ này. Trong phần này, bạn sẽ học được cách thực hiện những điều sau:
  - Tạo các detached containers (dùng `-d`) và interactive container (dùng `-it`)
  - Liệt kê các container trên của hệ thống
  - Xem log container
  - Dừng & khởi động lại container
  - Gắn lại thiết bị đầu cuối vào container
  - Tháo ra khỏi container gắn liền
- Không cần chần chừ thêm nữa, chúng ta hãy bắt đầu thực hiện đơn hàng của khách hàng

### 2.1.1 Creating and starting a new container
- Docker gọi tập hợp các file và hướng dẫn cần thiết để chạy 1 chương trình phần mềm là 1 `image`. Khi chúng ta cài đặt phần mềm bằng Docker, thực ra chúng ta đang sử dụng Docker để tải xuống hoặc tạo ra 1 image. Có nhiều cách khác nhau để cài đặt image và một số nguồn image. Image được đề cập chi tiết hơn trong chương 3, nhưng hiện tại bạn có thể coi chúng như những container vận chuyển được sử dụng để vận chuyển hàng hoá vật lý trên khắp thế giới. Docker images chứa mọi thứ mà máy tính cần để chạy phần mềm
- Trong ví dụ này, chúng ta sẽ download 1 image cho NGINX từ Docker Hub. Hãy nhớ rằng Docker Hub là sổ đăng ký công khai do Docker Inc. cung cấp. Image NGINX là thứ mà Docker Inc. gọi là kho lưu trữ đáng tin cậy. Nói chung, người hoặc tổ chức phát hành phần mềm sẽ kiểm soát các `trusted repository` cho phần mềm đó. Chạy lệnh sau sẽ download, cài đặt và khởi động 1 containar chạy NGINX
```
docker run --detach --name web nginx:latest
```
- Khi bạn chạy lệnh này, Docker sẽ cài đặt `nginx:latest` từ repository NGINX được lưu trữ trên Docker Hub (Được đề cập trong chương 3) và chạy phần mềm. Sau khi Docker đã cài đặt và bắt đầu chạy NGINX, một dòng ký tự ngẫu nhiên sẽ xuất hiện trên terminal. Nó sẽ trông giống như thế này:
```
7cb5d2b9a7eab87f07182b5bf58936c9947890995b1b94f412912fa822a9ecb5
```
- Blob ký tự đó là mã định danh duy nhất của container vừa được tạo để chạy NGINX. Mỗi lần bạn chạy `docker run` và tạo 1 container mới, container mới đó sẽ có 1 unique identifier. Người dùng thường ghi lại chuỗi này bằng 1 biến để sử dụng với lệnh khác. Bạn không cần phải làm như vậy cho mục đích của ví dụ này
- Sau khi identifier được hiển thị, có thể có vẻ như không có gì xảy ra