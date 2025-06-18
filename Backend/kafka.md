# Overview

## Hệ thống hoạt động không có Kafka
- Hãy tưởng tượng bạn có 1 cửa hàng X gồm các bộ phận: Nhận đơn hàng, kho, thanh toán & gửi email thông báo. (Mỗi bộ phận sẽ là 1 Service trong ứng dụng)
- Ban đầu, cửa hàng nhỏ, mọi thứ chỉ đơn giản là: Khách đặt hàng -> Bộ phận đơn hàng gọi cho kho `Cập nhật kho đi`, gọi cho thanh toán "Tính tiền" rồi gọi cho email `Gửi email đi`. Vẫn ổn áp vì chỉ có vài khách
- Nhưng bắt đầu có vấn đề khi đến **Black Friday**, lượng đơn bùng nổ:
    - Bộ phận thanh toán bị lag vì ngân hàng chậm chẳng hạn dẫn đến việc bộ phân đơn hàng phải chờ, khách thì chỉ thấy "Loading" xoay như chong chóng trên màn hình :v
    - Bộ phận kho thì lỗi 10 phút -> Đơn hàng tắc nghẽn 2h -> Mất khách
- Vấn đề là gì?
    - Các bộ phận "nói chuyện" trực tiếp với nhau (synchronous) nên 1 ông chậm là dẫn đến cả hệ thống chậm
    - Phải chờ đợi nhau -> Hệ thống tắc nghẽn
    - 1 bộ phận hỏng là hệ thống cũng đi đời luôn

## Kafka là gì?
- Kafka giống như 1 bưu điện ở giữa cửa hàng X. Thay vì các bộ phận phải gọi trực tiếp cho nhau, họ gửi "thư" (gọi là **event**) qua bưu điện Kafka. Các bộ phận khác đến lấy thư khi sẵn sàng, không phải chờ nhau
- Cách hoạt động:
    - Bộ phận đơn hàng (gọi là **producer**) gửi thư đến Kafka: "Khách vừa đặt đơn này, mọi người quẩy đi"
    - Kafka sẽ lưu vào "hộp thư" (gọi là **topic**), ví dụ hộp thư "orders" cho đơn hàng
    - Các bộ phận khác như kho, email, thanh toán (gọi là **consumer**) đến lấy thư từ hộp "orders" và làm việc của họ: Cập nhật kho, gửi email, tạo hoá đơn
- Lợi ích:
    - Không ai phải chờ ai -> Hệ thống nhanh hơn
    - Nếu bộ phận thanh toán chậm, đơn hàng vẫn được xử lý bình thường, không bị kẹt
    - Kafka giống như bưu điện mở 24/7, nhận và giao thư siêu nhanh, kể cả khi có hàng triệu khách

## Kafka có thay thế được DB không
- Chúng ta có thể thắc mắc "Kafka lưu thông tin đơn hàng, vậy nó có giống với DB không. **Khônggg**
- **Kafka làm gì?**
    - Nó giống như 1 cuốn sổ ghi lại mọi việc xảy ra (Như khách đặt đơn hàng này, kho update đơn hàng này). Những ghi chép (event) này được lưu tạm thời để các bộ phận khác dùng
- **DB làm gì?**
    - Nó giống như kho lưu trữ chính thức, nơi bạn lưu trữ thông tin lâu dài như danh sách sản phẩm, số lượng tồn kho,...

## Real-time with Stream API
- Kafka không chỉ gửi thư mà còn phân tích thông tin ngay lập tức, như 1 thư ký thông minh. Đây là lúc Stream API xuất hiện
- **Stream API** làm gì?
    - Nó liên tục đọc "thư" (event) từ Kafka và làm các phép tính ngay lập tức (Như đếm số lượng đơn hàng mỗi phút để update bảng doanh số)
- **Khác với consumer thông thường**
    - Consumer thông thường giống nhân viên Email, đọc từng thư và gửi email xác nhận
    - Stream API giống người phân tích, xem cả loạt thư và tính toán: "Nay bán được 1k đơn, cập nhật bảng doanh số thôi"
- Ví dụ trong cửa hàng X, Stream API đọc tất cả các đơn hàng để cập nhật doanh số trên website, để bạn có thể thấy doanh số trông như thế nào
- Hoặc trong các ứng dụng như Grab, Stream API theo dõi vị trí tài xế liên tục và cập nhật bản đồ cho khách

## Partition
- Khi cửa hàng X có hàng triệu khách, bưu điện Kafka phải xử lý cả triệu "thư" mỗi giây. Làm sao để không bị quá tải? Kafka chia hộp thư (topic) thành nhiều **partition** (giống như các quầy trong thư viện)
### Partition là gì?
- Thay vì 1 hộp thư "orders" duy nhất, Kafka chia thành nhiều quầy: Quầy cho đơn hàng ở Hà Nội, quầy cho đơn hàng ở Sì gòng, quầy cho đơn hàng ở Đà Nẵng. Mỗi quầy xử lý 1 phần công việc nên sẽ nhanh hơn
- Ví dụ như ở trong bưu điện nếu chỉ có 1 quầy duy nhất cho tất cả thư thì mọi người sẽ xếp hàng dài
    - Kafka chia thành nhiều quầy (partition), mỗi quầy xử lý 1 nhóm thư. Các bộ phận khác như kho, email đến quầy phù hợp để lấy thư nhanh hơn
- Bạn - người thiết kế hệ thống sẽ quyết định chia như thế nào (giống như việc chọn cách sắp xếp trong bưu điện)

## Consumer Group
- Tưởng tượng bạn có 1 bộ phận kho phải xử lý cả triệu "thư" từ Kafka. Một nhân viên kho không thể nào đọc hết được
- Kafka tạo **consumer groups**: Thay vì 1 nhân viên kho, bạn có cả 1 team (5 người cùng làm). Mỗi người lấy thư từ 1 partition -> xử lý nhanh hơn
### Cách hoạt động
- Kafka tự chia công việc: 1 bé lấy thư từ Hà Nội, 2 bé lấy thư Sì gòng,...
- Nếu có 1 bé nghỉ, Kafka đưa thư của bé đó cho người khác trong team
- Mỗi team có "mã số" (group ID) để Kafka biết họ cùng làm việc

## Kafka Broker
- Là "chi nhánh bưu điện" của Kafka, nơi lưu trữ tất cả thư (sự kiện) và xử lý việc gửi/giao thư
- Mỗi chi nhánh có máy tính lưu trữ trên đĩa cứng, đảm bảo thư không bị mất. Nếu có 1 chi nhánh bị hỏng, chi nhánh khác có bản sao để tiếp tục công việc

## So sánh Kafka với Message Broker tiêu chuẩn
- Các công cụ khác (như RabbitMQ) cũng giống như bưu điện nhưng khác ở chỗ
    - **Message Broker thông thường**: Giao xong thư là xoá luôn, giống như việc xem TV - Nếu bỏ lỡ chương trình là không xem lại được
    - **Kafka**: Giữ thư lâu dài, có thể xem lại đơn cũ để phân tích. Hoặc giống như việc xem Netflix, có thể xem lại phim bất cứ khi nào

## Zookeeper và KRaft
- Kafka cần "người quản lý" để theo dõi các chi nhánh bưu điện (broker) hoạt động thế nào, ai là "trưởng chi nhánh" để điều phối công việc
- **Zookeeper**: Trước đây Kafka sử dụng 1 tool riêng gọi là Zookeeper, giống như thuê 1 công ty bên ngoài để quản lý bưu điện. Zookeeper theo dõi chi nhánh nào còn hoạt động, chia việc ra sao
- **KRaft**: Bây giờ, từ bản 3.0, Kafka tự quản lý luôn, không cần Zookeeper nữa. Giống như bưu điện tự thuê quản lý trong nội bộ, đơn giản và tiết kiệm hơn

>Source: [Youtube](https://www.youtube.com/watch?v=QkdkLdMBuL0&ab_channel=TechWorldwithNana)