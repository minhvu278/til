# Part 1 : Fundamentals (Các nguyên tắc cơ bản)
- Cung cấp các nguyên tắc cơ bản mới trong Java8
- Hiểu được biểu thức lambda là gì
- Viết mã đầy đủ, dễ dàng thích ứng với các yêu cầu thay đổi 
- Chap 1: Tóm tắt những thay đổi của Java 
- Chap 2: 
- Chap 3: Giải thích đầy đủ, đầy đủ ví dụ về biểu thức lambda và tham chiếu phương thức 

## Chap 1: Java 8, 9 ,10 ,11
- Nội dung chương 
    - Lý do java thay đổi 
    - Thay đổi nền tảng máy tính 
    - Áp lực để Java phát triển 
    - Giới thiệu các tính năng thay đổi của java 8 và 9

- Kể từ khi phát hành Java Development Kit (JDK 1.0) vào năm 1996, Java đã được 1 số lượng lớn theo dõi và được sử dụng trong nhiều dự án lớn và nhỏ
- Big story: 
    - Java 8 thay đổi theo nhiều cách sâu sắc nhất trong tất cả các phiên bản 
    - Thay đổi cho phép bạn viết chương trình dễ dàng hơn 
    - Thay vì viết code dài dòng
        ```
        Collections.sort(inventory, new Comparator<Apple>() {
            public int compare(Apple a1, Apple a2){
            return a1.getWeight().compareTo(a2.getWeight());
            }
        });
        ```
    - Thì ta có thể viết 
        ```
        inventory.sort(comparing(Apple::getWeight));
        ```
- Từ những thay đổi trên, 1 số thứ nhất quán được Java ghi lại 
    - Luồng API
    - Kỹ thuật chuyển mã đến các phương thức 
    - Các phương thức mặc định của interface 

- Java 8 cung cấp 1 API mới hỗ trợ nhiều hoạt động song song để xử lý dữ liệu giống với truy vấn dữ liệu và có thể thể hiện những gì ta muốn theo cách cao cấp hơn 

- Lý do java còn thay đổi 
    - Ngôn ngữ mới xuất hiện thay cho ngôn ngữ cũ, trừ khi chúng thay đổi 
    - Tuy C, C++ vẫn được sử dụng phổ biến cho bởi vì thời gian chạy ngắn mặc dù thiếu an toàn nhưng sẽ dẫn đến thiếu an toàn, xảy ra nhiều lỗi và tạo ra các lỗ hổng về bảo mật. Vì thế nên Java & C# thay thế cho C và C++ 
- Ngôn ngữ Java trong hệ sinh thái 
    - Java có 1 khởi đầu tốt, bắt đầu bằng hướng đối tượng và các thư viện hữu ích 
- Lý do java trở thành ngôn ngữ lập trình chung
    - Hướng đối tượng đã trở thành hot vào năm 1990 nhờ 2 lý do: 
        - Tính đóng gói của nó ít vấn đề hơn đối với C 
        - Dễ nắm bắt mô hình lập trình WIMP từ win 95 đổ lên 

- Java 8 cung cấp nhiều công cụ và khái niệm giúp giải quyết vấn đề mới hoặc hiện tại nhanh hơn 

### Xử lý luồng 
- Khái niệm đầu tiên là xử lý luồng 
- 1 chương trinh có thể đọc từng mục của 1 luồng vào và tương tự như vậy ghi các mục vào luồng đầu ra 
- Luồng đầu ra của 1 chương trình cũng có thể là luồng đầu vào của 1 chương trình khác 


## Function 
-  Java 8 bổ sung các hàm dưới dạng giá trị mới tạo điệu kiện cho việc sử dụng các luồng 
- Các giá trị có thể đưọc thao tác bằng chương trình Java 
    - Đầu tiên là có các giá trị nguyên thủy
    - Thứ 2 là giá trị có thể là đối tượng 
- Cách duy nhất để có 1 trong những thứ này là sử dụng từ khóa `new`

### Phương thức và lambda 
- Tính năng đầu tiên là tham chiếu phương thức 
    - Giả sử muốn lọc all các tệp ẩn trong 1 thư mục, ta cần viết 1 phương thức, với 1 tệp nó sẽ cho biết có bị ẩn hay không. Có 1 phương thức hỗ trợ là `isHidden()` - Có thể xem là 1 hàm lấy về 1 File và trả về giá trị boolean.
    - Tuy nhiên để sử dụng nó thì ta cần phải bọc thành 1 đối tượng `FileFilter` mà sau đó phải chuyển vào phương thức `File.listFiles` 
        ```
        File[] hiddenFiles = new File(".").listFiles(new FileFilter() {
            public boolean accept(File file) {
            return file.isHidden();
            }
        });
        ```
    - Khá phức tạp mặc dù đó chỉ là 3 dòng quan trọng. Ta đã có sẵn phương thức `isHidden` mà ta có thể sử dụng. Vậy tại sao lại phải gói gọn trong class `FileFilter` dài dòng và sau đó khởi tạo nó. Đó là bởi vì những gì mà ta phải làm trước Java 8
    - Bây giờ ta có thể viết đoạn code đó như sau 
        ```
        File[] hiddenFiles = new File(".").listFiles(File::isHidden);
        ```
    - Ta đã có sẵn `isHidden` vì thế ta có thể chuyển vào thẳng vào phương thức `listFiles` bằng cách sử dụng tham chiếu phương thức trong Java 8 `::`

### Lambdas: Anoymous fuction
- 
 