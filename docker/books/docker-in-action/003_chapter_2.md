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
- Sau khi identifier được hiển thị, có thể có vẻ như không có gì xảy ra. Đó là vì bạn đã sử dụng option `--detach` và khởi động chương trình ở chế độ nền. Điều này có nghĩa là chương trình đã bắt đầu nhưng không được attached vào terminal của bạn. Khởi động NGINX theo cách này là hợp lý vì chúng ta sẽ chạy vài chương trình. Server software thường được chạy trong các containers ngầm vì hiếm khi software phụ thuộc vào 1 attached terminal
- Chạy các detached containers là giải pháp hoàn hảo cho các chương trình chạy ngầm ở backgroud. Loại program đó gọi là `daemon`(Chương trình chạy nền trong hệ điều hành thường có chứ *d* ở cuối - vd *httpd*) hoặc `service`. Daemon thường tương tác với các programs khác hoặc con người thông qua network hoặc 1 số kênh truyền thông khác. Khi bạn khởi chạy 1 daemon hoặc program khác trong 1 container mà bạn muốn chạy ở chế độ nền, hãy nhớ sử dụng flag `--detach` hoặc dạng viết tắt là `-d`
- Một deamon khác mà khách hàng của bạn cần trong ví dụ này là 1 `mailer`. Mailer chờ kết nối từ một người gọi & sau đó gửi email (Vd web app gửi yêu cầu đến mailer để gửi email xác nhận cho người dùng). Lệnh sau sẽ cài đặt và chạy 1 mailer phù hợp cho ví dụ này
```
docker run -d \
 --name mailer \
 dockerinaction/ch2_mailer
 ```
- Lệnh này sử dụng dạng rút gọn của flag --detach để bắt đầu 1 container mới có tên là mailer ở chế độ nền. Tại thời điểm này, bạn đã chạy 2 lệnh và cung cấp 2/3 hệ thống mà khách hàng muốn. Component cuối cùng gọi là `agent`, phù hợp với interactive (tương tác) container

### 2.1.2 Running interactive containers
- Text editor mở trên terminal là 1 ví dụ tuyệt vời về chương trình cần có terminal để hoạt động. Nó lấy dữ liệu đầu vào từ người dùng thông qua bàn phím (có thể là chuột) và hiển thị đầu ra trên terminal. Nó có tính tương tác thông qua các luồng đầu vào và đầu ra. Để chạy các interactive programs trong Docker, bạn phải liên kết các phần của terminal với input hoặc output của 1 container. 
- Để bắt đầu làm việc với interactive containers, hãy chạy lệnh sau:
```
docker run --interactive --tty \
 --link web:web \
 --name web_test \
 busybox:1.29 /bin/sh
```
- Lệnh sử dụng 2 flag trên command: `interactive (hoặc -i)` và `-tty (hoặc -t)`. Đầu tiên, option `-interactive` yêu cầu Docker giữ luồng đầu vào chuẩn (stdin) (luồng dữ liệu mà bạn gửi vào chương trình, thường là từ keyboard) mở cho container (Không đóng luồng này, nghĩa là bạn có thể tiếp tục gửi lệnh hoặc dữ liệu vào container) ngay cả khi không có terminal nào được attach (ngay cả khi không có terminal nào kết nối trực tiếp với container, luồng đầu vào vẫn hoạt động). Thứ 2, option `-tty` yêu cầu Docker phân bổ 1 virtual terminal cho container, cho phép bạn truyền tín hiệu đến container. Đây thường là những gì bạn mong muốn từ 1 interactive command-line program. Bạn thường sử dụng cả 2 cách này khi chạy 1 interactive program như shell trong 1 interactive container. 
- Cũng quan trọng như các interactive flags, khi bạn bắt đầu container này, bạn đã chỉ định chương trình chạy bên trong conainer. Trong trường hợp này, bạn đã chạy 1 shell program có tên là `sh`. Bạn có thể chạy bất kỳ program nào bên trong container
- Lệnh trong ví dụ về container tương tác tạo ra 1 container, khởi động shell UNIX và được liên kết với container đang chạy NGINX. Từ shell này, bạn có thể chạy các lệnh xác minh rằng web server của bạn đang chạy đúng cách
```
wget -O - http://web:80/
```
- Sử dụng 1 program có tên là wget để thực hiện request HTTP đến web server(NGINX server mà bạn đã khởi động trước đó trong 1 container) và sau đó hiển thị nội dung của trang web trên terminal của bạn. Trong số các dòng khác, sẽ có 1 thông báo như "Welcome to NGINX!". Nếu bạn thấy thông báo đó thì mọi thứ đang hoạt động bình thường và bạn có thể tiếp tục và tắt interactive container bằng cách nhập exit. Thao tác này sẽ chấm dứt chương trình shell và dừng container. 
- Có thể tạo 1 interactive container, bắt đầu thủ công 1 quy trình bên trong container đó, sau đó tách biệt terminal của bạn. Bạn có thể thực hiện bằng cách giữ phím Ctrl (hoặc Control) và nhầm phím P rồi nhấn Q. Tính năng này chỉ hoạt động khi bạn sử dụng option `-tty`.
- Để hoàn thiện công việc cho khách hàng của bạn, bạn cần phải bắt đầu 1 agent (1 chương trình nhỏ - tác nhân thực hiện nhiệm vụ cụ thể, ở đây là giám sát). Đây là 1 agent giám sát sẽ kiểm tra web server như bạn đã làm trong ví dụ trước và gửi tin nhắn bằng mailer nếu web server dừng. Lệnh này sẽ khởi động các agent trong 1 interactive container bằng cách sử dụng các dạng flags ngắn
```
docker run -it \
 --name agent \
 --link web:insideweb \
 --link mailer:insidemailer \
 dockerinaction/ch2_agent
 ```
- Khi chạy, container sẽ kiểm tra web container mỗi giây và in ra thông báo như sau:
```
System up.
```
- Bây giờ, bạn đã thấy chức năng của nó, hãy detach terminal của bạn ra khỏi container. Cụ thể khi bạn khởi động container và nó bắt đầu ghi System, hãy giữ Ctrl (hoặc control) rồi nhấn P và Q. Sau khi thực hiện xong, bạn sẽ được trả về shell cho host computer của mình. Không dừng chương trình, nếu không màn hình sẽ dừng kiểm tra web server
- Mặc dù bạn thường sử dụng các container detached hoặc deamon cho phần mềm mà bạn triển khai tới các server trên mạng của mình, nhưng các interactive container hữu ích để chạy phần mềm trên desktop của bạn hoặc làm việc thủ công trên server. Tại thời điểm này, bạn đã khởi động cả 3 ứng dụng trong container mà khách hàng của bạn cần. Trước khi bạn có thể tự tin khẳng định đã hoàn thành, bạn nên kiểm tra hệ thống

### 2.1.3 Listing, stopping, restarting, and viewing output of containers
- Đầu tiên, bạn nên làm là kiểm tra setup hiện tại của mình là kiểm tra xem container nào đang chạy bằng cách sử dụng lệnh `docker ps`
- Chạy lệnh sẽ hiển thị thông tin sau về từng container đang chạy
  - ID container
  - Image được sử dụng
  - Command thực hiện trong container
  - Thời gian kể từ khi container được tạo ra
  - Thời gian container đã chạy
  - Các networks port được container tiếp xúc
  - Container name
- Tại thời điểm này, bạn sẽ có 3 container đang chạy với các tên: web, mailer và agent. Nếu có bất kỳ điều gì bị thiếu nhưng bạn đã làm theo ví dụ cho đến nay, có thể nó đã bị dừng nhầm. Ba lệnh tiếp theo sẽ restart lại từng container bằng cách sử dụng container name. Chọn những mục thích hợp để restart lại các container bị thiếu trong danh sách các container đang chạy
```
docker restart web
docker restart mailer
docker restart agent
```
- Bây giờ, cả 3 container đều đang chạy, bạn cần kiểm tra xem hệ thống có đang hoạt động chính xác không. Cách tốt nhất để thực hiện điều đó là kiểm tra logs của từng container. Bắt đầu với web container
```
docker logs web
```
- Lệnh này sẽ hiển thị 1 bản ghi dài với nhiều dòng chứa chuỗi con này
```
"GET / HTTP/1.0" 200
```
- Điều này có nghĩa là web server đang chạy và agent đang kiểm tra trang web. Mỗi lần agent kiểm tra trang web, một trong những dòng này sẽ được ghi vào log. Lệnh docker logs có thể hữu ích cho những trường hợp này nhưng không nên phụ thuộc hoàn toàn vào nó vì có rủi ro. Bất cứ điều gì mà chương trình ghi vào luồng đầu ra stdout hoặc stderr sẽ được ghi lại trong log. Vấn đề với pattern này là log không bao giờ xoay hoặc cắt bớt theo mặc định, do đó, dữ liệu sẽ được ghi vào log cho 1 container sẽ vẫn tồn tại và tăng lên miễn là container đó tồn tại. Việc lưu trữ log lâu dài như vậy có thể gây rắc rối cho quá trình chạy dài hạn. Một cách tốt hơn để xử lý log bằng cách dùng volumes và sẽ thảo luận trong chương 4. 
- Bạn có thể biết rằng agent đang giám sát web server bằng cách kiểm tra log chỉ dành cho web. Để hoàn thiện, bạn cũng nên kiểm tra log output cho mailer & agent
```
docker logs mailer
docker logs agent
```
- Log của mailer sẽ trông như thế này
```
CH2 Example Mailer has started.
```
- Log của agent phải chứa 1 số dòng giống như dòng bạn đã xem khi bạn khởi động container
```
System up.
```
  - Lệnh docker logs có 1 flag -follow hoặc -f, sẽ hiển thị các bản ghi & sau đó tiếp tục theo dõi & cập nhật màn hình hiển thị với các thay đổi đối với bản ghi khi chúng xảy ra. Khi hoàn tất, hãy nhấn Ctrl-C (Hoặc command C) để ngắt logs command
- Bây giờ, bạn đã xác thực rằng các container đang chạy và các agent có thể truy cập máy chủ web, bạn nên kiểm tra xem các agent có nhận thấy khi container web dừng không. Khi điều đó xảy ra, agent sẽ trigger 1 cuộc gọi đến *mailer* và sự kiện sẽ được ghi lại trong log cho cả agent & mailer. Lệnh docker stop yêu cầu chương trình có PID 1 trong container dừng lại. Sử dụng nó trong các lệnh sau để kiểm tra system:
```
docker stop web
docker logs mailer
```
- Hãy tìm ở cuối mailer log có nội dung như sau
```
Sending email: To: admin@work Message: The service is down!
```
- Dòng đó có nghĩa là agent đã phát hiện thành công rằng NGINX server trong container có tên web đã dừng. Chúc mừng! Khách hàng rất vui & bạn đã xây dựng được hệ thống thực sự đầu tiên của mình với container & Docker
- Học các tính năng cơ bản của Docker là 1 chuyện, nhưng hiểu lý do tại sao chúng lại hữu ích và cách sử dụng chúng để tuỳ chỉnh cô lập (isolation - Mỗi container chạy độc lập, không ảnh hưởng đến nhau - như hệ điều hành riêng) lại là 1 nhiệm vụ hoàn toàn khác

## 2.2 Solved problems and the PID namespace
- Mỗi program đang chạy hoặc quy trình trên máy Linux đều có 1 số duy nhất gọi là identifier (PID).  PID namespace là tập hợp các số duy nhất xác định các quy trình. Linux cung cấp các công cụ để tạo nhiều namespace tên PID. Mỗi namespace có 1 bộ đầy đủ các PID có thể có. Điều này có nghĩa là PID sẽ chứa PID 1,2,3,... của riêng nó.
- Hầu hết các program sẽ không cần truy cập vào các tiếng trình đang chạy khác hoặc có thể liệt kê các tiến trình đang chạy khác trên hệ thống. Và do đó Docker sẽ tạo ra 1 namespace PID mới cho mỗi container theo mặc định. PID namespace của container cô lập các quy trình trong container đó ra khỏi các quy trình trong các container khác. 
- Theo quan điểm của 1 quy trình trong 1 container có namespace riêng, PID 1 (Process ID số 1 - quá trình đầu tiên & quan trọng nhất trong bất kỳ hệ thống Linux nào) có thể là 1 quá trình thuộc hệ thống khởi động (init system) như `runit` hoặc `supervisor`, thay vì process của host. Trong 1 container khác, PID 1 có thể tham chiếu đến 1 shell command như bash. Chạy lệnh sau để xem nó hoạt động
  - Trên máy thật, PID 1 thường là `systemd` hoặc `init` (quản lý tất cả các process khác)
```
docker run -d --name namespaceA \
 busybox:1.29 /bin/sh -c "sleep 30000"
docker run -d --name namespaceB \
 busybox:1.29 /bin/sh -c "nc -l 0.0.0.0 -p 80"

docker exec namespaceA ps // 1
docker exec namespaceB ps // 2
```
- Command 1 sẽ tạo ra danh sách các quy trình tương tự nhau
```
PID USER TIME COMMAND
 1 root 0:00 sleep 30000
 8 root 0:00 ps
```
- Command 2 sẽ tạo ra 1 danh sách quy trình hơi khác
```
PID USER TIME COMMAND
1 root 0:00 nc -l 0.0.0.0 -p 80
9 root 0:00 ps
```
- Trong ví dụ này, bạn sử dụng lệnh docker exec để chạy các tiến trình bổ sung trong 1 container đang chạy. Trong trường hợp này, lệnh bạn sử dụng được gọi là ps, lệnh này sẽ hiển thị tất cả các tiến trình đang chạy và PID của chúng. Từ kết quả đầu ra, bạn có thể thấy rõ ràng rằng mỗi container đều có 1 process với PID 1
- Nếu không có namespace PID, các process chạy bên trong 1 container sẽ chia sẻ cùng 1 namespace ID như các process trên các container trên máy khác hoặc trên server. Một process trong 1 container sẽ có thể xác định những process nào đang chạy trên server. Tệ hơn nữa, các quy trình trong 1 container có thể kiểm soát các quy trình trong 1 container khác. Một quy trình không thể tham chiếu đến bất kỳ quy trình nào bên ngoài namespace của nó sẽ bị hạn chế khả năng thực hiện các cuộc tấn công có mục tiêu
- Giống như hầu hết các tính năng cô lập của Docker, bạn có thể tuỳ chọn tạo các container mà không có namespace PID của riêng chúng. Điều này rất quan trọng nếu bạn đang sử dụng một chương trình để thực hiện tác vụ quản trị hệ thống yêu cầu liệt kê quy trình từ bên trong 1 container. Bạn có thể tự mình thử điều này bằng cách đặt flag -pid trên docker create hoặc docker run và đặt value thành host. Hãy tự mình thử với 1 container chạy BusyBox Linux và lệnh ps Linux
```
docker run --pid host busybox:1.29 ps
```
- Bởi vì tất cả các container đều có namespace PID riêng, chúng không thể thấy thông tin hữu ích khi kiểm tra PID của mình và phụ thuộc nhiều hơn vào cấu hình tĩnh (Khi dùng riêng nghĩa là không có --pid host thì chúng phải phụ thuộc vào cách cấu hình của chính mình - Như PID 1 là *bash* hoặc *nginx*. Với --pid host container phụ thuộc vào host nhiều hơn - vì thấy PID của host làm mất đi tính cô lập). Giả sử 1 container chạy 2 process: 1 server và 1 process monitor. Màn hình đó có thể phụ thuộc chặt chẽ vào PID dự kiến của server và sử dụng nó để monitor (giám sát) & kiểm soát server. Đây là 1 ví dụ về sự độc lập môi trường
- Hãy xem xét ví dụ web-monitoring trước đó. Giả sử bạn không sử dụng Docker và chỉ chạy NGINX trực tiếp trên máy tính của bạn. Bây giờ, giả sử bạn quên rằng bạn đã bắt đầu NGINX cho 1 dự án khác. Khi bạn khởi động lại NGINX, quy trình thứ 2 sẽ không thể truy cập vào được các resource cần thiết vì process đầu tiên đã có chúng. Đây là ví dụ xung đột phần mềm cơ bản. Bạn có thể thấy nó hoạt động bằng cách thử chạy 2 bản sao NGINX trong cùng 1 container
```
docker run -d --name webConflict nginx:latest
docker logs webConflict
docker exec webConflict nginx -g 'daemon off;'
```
- Last command sẽ hiển thị kết quả như thế này
```
2015/03/29 22:04:35 [emerg] 10#0: bind() to 0.0.0.0:80 failed (98:
Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
...
```
- Process thứ 2 không được khởi động đúng cách và báo cáo rằng địa chỉ cần thiết đã được sử dụng. Được gọi là `port conflict`, đây là sự cố phổ biến trong các hệ thống thực tế trong đó có nhiều quy trình đang chạy trên cùng 1 máy tính hoặc nhiều người cùng đóng góp vào cùng 1 môi trường. Đây là 1 ví dụ tuyệt vời về vấn đề conflict mà Docker đơn giản hoá và giải quyết. Chạy từng cái trong 1 container khác nhau, như thế này:
```
docker run -d --name webA nginx:latest // Bắt đầu phiên bản NGINX đầu tiên

docker logs webA  // Xác minh nó hoạt động, phải trống

docker run -d --name webB nginx:latest // Bắt đầu phiên bản thứ 2

docker logs webB  // Xác minh nó hoạt động, phải trống
```
- Tính độc lập về môi trường, cung cấp sự tự do để cấu hình phần mềm phụ thuộc vào các resource hệ thống khan hiếm mà không cần quan tâm đến các phần mềm cùng vị trí khác có các yêu cầu xung đột. Sau đây là 1 số vấn đề conflict phổ biến
  - 2 chương trình muốn liên kết với cùng 1 network port
  - 2 chương trình sử dụng cùng 1 tên file tạm thời và file locks đang ngăn chặn điều đó
  - 2 chương trình muốn sử dụng các phiên bản khác nhau của 1 thư viện được cài đặt global
  - 2 processes muốn sử dụng cùng 1 PID file
  - Chương trình thứ 2 bạn cài đặt đã sửa đổi biến môi trường mà một chương trình khác sử dụng. Bây giờ chương trình đầu tiên bị hỏng
  - Nhiều process đang chạy cạnh tranh về memory hoặc CPU time
- Tất cả các conflict này phát sinh khi 1 hoặc nhiều chương trình có sự phụ thuộc chung nhưng không thể đồng ý chia sẻ hoặc có nhu cầu khác nhau. Giống như ví dụ port conflict trước đó, Docker giải quyết xung đột phần mềm bằng các công cụ như Linux namespaces, resource limits, filesystem roots và các thành phần network ảo hoá (virtualized network components). Tất cả các công cụ này được sử dụng để cô lập phần mềm bên trong 1 container Docker

## 2.3 Eliminating metaconflicts: Building a website farm
- Trong phần trước, bạn đã thấy Docker giúp bạn tránh xung đột phần mềm với quy trình cô lập như thế nào. Nhưng nếu bạn không cẩn thận, bạn có thể kết thúc bằng việc xây dựng các hệ thống tạo ra metaconflicts hoặc xung đột giữa các container trong Docker layer
- Hãy xem xét 1 ví dụ khác: Một khác hàng đã yêu cầu bạn xây dựng 1 hệ thống mà bạn có thể lưu trữ một số lượng trang web khác nhau cho khách hàng của họ. Họ cũng muốn sử dụng cùng 1 công nghệ giám sát mà bạn đã xây dựng trước đó trong chương này. Mở rộng hệ thống bạn đã xây dựng trước đó sẽ là cách đơn giản nhất để hoàn thành công việc này mà không cần tuỳ chỉnh cấu hình cho NGINX. Trong ví dụ này, bạn sẽ xây dựng 1 hệ thống với 1 số container chạy máy chủ web và 1 số trình theo dõi giám sát cho mỗi web server. Hệ thống sẽ giống như kiến trúc được mô tả trong hình 2.2
![2.2-web server](./images/2.2-web-server-monitor.png)
- Bản năng đầu tiên của bạn có thể là chỉ cần bắt đầu nhiều vùng chứa web hơn. Nhưng điều đó không đơn giản như vẻ bề ngoài của nó. Việc xác định các container trở nên phức tạp khi số lượng container tăng lên

### 2.3.1 Flexible container identification
- Cách tốt nhất để tìm hiểu lý do tại sao việc chỉ tạo thêm các bản sao của NGINX container mà bạn đã sử dụng trong ví dụ trước là 1 ý tưởng tồi
```
docker run -d --name webid nginx // Tạo 1 container có tên là `webid`
docker run -d --name webid nginx // Tạo 1 container khác có tên là webid
```
- Lệnh thứ 2 sẽ không thành công do conflict
```
FATA[0000] Error response from daemon: Conflict. The name "webid" is
already in use by container 2b5958ba6a00. You have to delete (or rename)
that container to be able to reuse that name.
```
- Sử dụng tên container cố định như web rất hữu ích cho việc thử nghiệm và document, nhưng trong 1 system có nhiều container, việc sử dụng tên cố định như vậy có thể gây xung đột. Theo mặc định, Docker gán 1 tên duy nhất (thân thiện với con người) cho mỗi vùng chứa mà nó tạo ra. Flag `--name` ghi đè lên process đó bằng 1 giá trị đã biết. Nếu có tình huống phát sinh mà tên của 1 conainer cần thay đổi, bạn luôn có thể đổi tên container bằng lệnh `docker rename`
```
docker rename webid webid-old  // Đổi tên container hiện tại thành webid-old
docker run -d --name webid nginx  // Tạo 1 container khác có tên là webid
```
- Đổi tên container có thể giúp giảm bớt xung đột đặt tên 1 lần nhưng không giúp ích nhiều trong việc tránh vấn đề này ngay từ đầu. Ngoài tên, docker còn gán 1 indentifier duy nhất đã đề cập trong ví dụ đầu tiên. Đây là những con số 1024 bit được mã hoá theo hệ thập lục phân và trông giống như thế này:
```
7cb5d2b9a7eab87f07182b5bf58936c9947890995b1b94f412912fa822a9ecb5
```
- Khi các container được khởi động ở chế độ detached, identifier của chúng sẽ được in ra terminal. Bạn có thể sử dụng identifer này thay cho tên container với bất kỳ lệnh nào cần xác định 1 container cụ thể. Ví dụ, bạn có thể sử dụng ID trước đó với lệnh exec hoặc stop
```
docker exec \
7cb5d2b9a7eab87f07182b5bf58936c9947890995b1b94f412912fa822a9ecb5 \
echo hello
docker stop \
7cb5d2b9a7eab87f07182b5bf58936c9947890995b1b94f412912fa822a9ecb5
```
- Xác suất cao về tính năng duy nhất của các ID được tạo ra có nghĩa là không có khả năng xảy ra conflict với ID này. Ở mức độ thấp hơn, cũng không có khả năng xảy ra va chạm giữa 12 ký tự đầu tiên của ID này trên cùng 1 máy tính. Vì trong hầu hết các interface Docker, bạn sẽ thấy ID container bị cắt bớt thành 12 ký tự đầu tiên. Điều này làm cho ID được tạo ra thân thiện hơn với người dùng. Bạn có thể sử dụng chúng ở bất cứ nơi nào cần có container identifier. 2 lệnh trước có thể được viết như thế này:
```
docker exec 7cb5d2b9a7ea ps
docker stop 7cb5d2b9a7ea
```
- Không có ID nào trong số này đặc biệt phù hợp để con người sử dụng. Nhưng chúng hoạt động tốt với các scripts và các kỹ thuật tự động hoá. Docker có 1 số phương tiện để lấy ID của 1 container để có thể tự động hoá. Trong trường hợp này, ID số đầy đủ hoặc bị cắt bớt sẽ được sử dụng
- Cách đầu tiên để lấy ID của 1 container là chỉ cần bắt đầu hoặc tạo 1 container mới và gán kết quả của lệnh cho 1 biến shell
- Như bạn đã thấy trước đó, khi 1 container mới được khởi động ở chế độ detached, ID của container sẽ được ghi vào terminal (stdout). Bạn không thể sử dụng điều này với các interactive container nếu đây là cách duy nhất để có được ID container tại thời điểm này. May mắn thay, bạn có thể sử dụng lệnh khác để tạo container mà không cần khởi động nó. Lệnh `docker create` tương tự như `docker run`, điểm khác biệt chính là container được tạo ở trạng thái đã dừng
```
docker create nginx
```
- Kết quả sẽ là 1 dòng như thế này
```
b26a631e536d3caae348e9fd36e7661254a11511eb2274fb55f9f7c788721b0d
```
- Nếu bạn đang sử dụng Linux command shell như sh hoặc bash, bạn có thể gán kết quả đó cho 1 biến shell và sử dụng lại sau
```
CID=$(docker create nginx:latest)  // Điều này sẽ có hiệu lực trên các shell tuân thủ POSIX
echo $CID
```
- Shell variable tạo ra cơ hội mới cho conflict, nhưng phạm vi conflict đó bị giới hạn trong terminal session hoặc môi trường xử lý hiện tại mà tập lệnh được khởi chạy. Những xung đột đó có thể dễ dàng tránh được vì 1 mục đích sử dụng hoặc chương trình đang quản lý môi trường đó. Vấn đề với cách tiếp cận này là nó sẽ không giúp ích nếu nhiều người dùng hoặc các quy trình tự động cần chia sẻ thông tin đó. Trong trường hợp đó, bạn có thể sử dụng container ID (CID) file
