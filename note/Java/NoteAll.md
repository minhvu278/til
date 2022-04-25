## Java là gì 
- Là ngôn ngữ kế thừa trực tiếp từ C/C++ và là ngôn ngữ lập trình hướng đối tượng 

## Các kiểu dữ liệu trong Java
- Có 8 kiểu
    - byte
    - short
    - int 
    - long
    - float
    - double
    - boolean
    - char 
 ## Biến và hằng số 
 - Biến : Dùng để lưu trữ dữ liệu mà chương trình có thể tương tác được
    - Có 3 loại: 
        - Biến cục bộ(Local variable) : Là biến được khởi tạo bên trong các phương thức, và được hủy khi phương thức bị hủy 
        - Biến toàn cục (Instance variable): Biến nằm bên trong 1 lớp và bên ngoài mọi phương thức 
        - Biến tĩnh (Static variable): Được khai báo bên trong 1 class với từ khóa `static`, phía bên ngoài các phương thức, constructor và block 
    
- Hằng: Là giá trị không bao giờ thay đổi trong suốt quá trình chạy (Giá trị bất biến trong chương trình)
    - Để khai báo thì ta sử dụng từ khóa `static final`
        ```
        public static final int HOUR_OF_DAY = 24;
        ```

## Chuỗi (String)
- Được coi là 1 dữ liệu dạng đối tượng 
- Có 2 cách để khai báo 
    - C1: 
        ```
        String tenChuoi = "giá_trị_khởi_tạo";
        ```
    - C2: Sử dụng từ khóa new 
        ```
        String chuoi = new String("Welcome to Java!");
        ```
- 1 số hàm xử lý chuỗi 
    - Xác định độ dài 
        ```
        int length = tên_chuỗi.length();
        ```
    - Nối 2 chuỗi : Có thể dùng dấu + hoặc hàm concat() : 
        ```
            String chuoi1 = "Happy ", chuoi2 = "new year!";
        
            /* 
            * nối chuỗi
            */
            String chuoi3 = chuoi1.concat(chuoi2);
            System.out.println(chuoi3); 
        ````
    - So sánh 2 chuỗi sử dụng `compareTo()` : 
        ```
        int result = string1.compareTo(String string2);
        ```

## Collection
- Collection ra đời để khắc phục những hạn chế khi sử dụng mảng 
- Là 1 tập hợp các lớp dùng để lưu trữ danh sách và có khả năng tự co dãn khi danh sách đó thay đổi 
- Không cần khai báo trước số lượng phần tử. Chính vì thế nên khắc phục được hạn chế về kích thước trong mảng 
- Collection framework là 1 tập hợp các class và interface dùng để hỗ trợ việc thao tác trên tập các đối tượng 

## Interface Collection, Class Collection 
- Interface collection 
    - Gồm các interface chính 
        - List Interface: Các phần tử trong này được sắp xếp theo thứ tự và có thể có giá trị giống nhau 
        - Set: Các phần tử trong set là duy nhất và không được giống nhau 
        - SortedSet: Là 1 dạng riêng của Set Interface, trong đó giá trị mặc định của các phần tử được sắp xếp tăng dần 
        - Map: Giá trị của mỗi phần tử trong Map gồm key và value và mỗi key là duy nhất 
        - SortedMap: Là dạng riêng của Map Interface, trong đó giá trị key được sắp xếp tăng dần 

- Class collection
    - Có 6 loại chính 
        - LinkedList: Lưu trữ phần tử dưới dạng danh sách. Các phần tử trong LinkedList được sắp xếp theo thứ tự và có thể giống nhau 
        - ArrayList : Lưu trữ phần tử dưới dạng mảng. Thứ tự dựa vào thứ tự thêm vào và giá trị có thể trùng nhau 
        - HashSet: Thứ tự không dựa theo thứ tự lúc thêm vào và giá trị phần tử là duy nhất 
        - TreeSet: Mặc định được xếp tăng dần và giá trị phần tử là duy nhất
        - HashMap: Giá tri mỗi phần tử bao gồm key và value. HashMap cho phép truy xuất dữ liệu thông qua key 
        - TreeMap: Giá trị cũng gồm key và value. Giá trị được sắp xếp tăng dần 

## Iterator(lặp)
- Là 1 interface cũng cấp 1 số các phương thức dùng để duyệt lặp các phần tử của bất kì tập hợp nào 
- Đối với collection thì ta sử dụng `Iterator` để duyệt qua các phần tử của 1 collection 

## OOP 
- Là 1 kỹ thuật tạo ra các đối tượng trong code
- Tất cả các logic yêu cầu thực tế đều được xây dựng xoay quanh các đối tượng 
- Access modifier 
    - public :  Có thể truy cập ở mọi nơi 
    - protected: Truy cập trong lớp khai báo lớp con của nó và các lớp cùng gói với nó 
    - default: Truy cập từ trong lớp khai báo và các lớp cùng gói với lớp khai báo 
    - private: Chỉ truy cập bên trong lớp 

- Tính đóng gói (Encapsulation)
    - Bảo mật và che giấu thông tin 
    - Các thuộc tính của đối tượng được khai báo là private 
    - Cũng cấp phưowng thức getter/setter để truy cập và sửa đổi dữ liệu 

- Tính kế thừa: 
    - Cho phép lớp con kế thừa các thuộc tính và phương thức của lớp chả
    - Lớp con cũng có thể thêm các thuộc tính và phương thức của riêng nó 
    - Từ khóa super 
        - Sử dụng để phân biệt các thành phần có cùng tên giữa lớp cha và lớp con 
        - Sử dụng để gọi hàm tạo của lớp cha từ con 
    
- Tính đa hình 
    - Có khả năng giúp tái sử dụng lại code và có thể thay đổi cách ứng xử một cách linh hoạt tùy theo loại đối tượng 
    - Ví dụ như là sinh viên đến trường nghe giảng còn về nhà rửa bát,...
    - Để thể hiện được tính đa hình cần bảo đảm 2 điều kiện 
        - Các lớp phải có quan hệ kế thừa với 1 lớp cha nào đó 
        - Tính đa hình chỉ được thể hiện khi đã ghi đè lên phương thức của lớp cha 

    - VD 
        ```
        public class Shape {
            public void show() {
                System.out.println("Đây là phương thức show() của lớp Shape");
            }
        }
        ```
        ```
        public class Rectangle extends Shape {
            public void show() {
                System.out.println("Đây là phương thức show() của lớp Rectangle");
            }
        }
        ```
        ```
        public class Square extends Shape {
            public void show() {
                System.out.println("Đây là phương thức show() của lớp Square");
            }
        }
        ```
        ```
        public class Main {

        public static void main(String[] args) {
            Shape shape = new Shape();
            shape.show();   // hiển thị dòng "Đây là phương thức show() của lớp Shape"
                // bản chất của shape là Shape, nhưng vì khai báo Rectangle nên chúng ta chỉ nhìn thấy những gì mà Rectangle có
                // vì vậy sẽ chạy những hàm của Rectangle
                shape = new Rectangle();
                shape.show();   // hiển thị dòng "Đây là phương thức show() của lớp Rectangle"
                // tương tự lúc này shape sẽ đóng vai trò là 1 Square
                shape = new Square();
                shape.show();   // hiển thị dòng "Đây là phương thức show() của lớp Square"
            }
        
        }
        ```
    - Đúng ra là mỗi 1 lớp ta phải tạo ra 1 đối tượng tương ứng để gọi hàm `show()` nhưng đối với tính đa hình thì không cần, `shape` sẽ đóng vai trò là lớp con tương ứng

- Tính trừu tượng 
    - Không thể hiện cụ thể mà chỉ nêu tên vấn đề 
    - Loại bỏ các tính chất phức tạp và chỉ đưa các thuộc tính và phương thức cần thiết 
    - Phương thức trừu tượng 
        - Không có thân phương thức nằm trong `{}`
        - Và để định nghĩa thì ta thêm `abstract` trước tên phương thức 
            ```
            public abstract khaiBaoPhuongThucTruuTuong();
            ```
            - Để sử dụng được phương thức trừu tượng này thì ta cần phải ghi đè nó trong lớp con kế thừa nó 
    - Lớp trừu tượng (Abstract Class)
        - Không thể khởi tạo đối tượng từ nó 
        - Các lớp con kế thừa phải có các thuộc tính & phương thức của nó thông qua việc ghi đè 

## Static 
- Chủ yếu dùng để quản lý bộ nhớ
- Đặc điểm chung của các thành phần khai báo là static 
    - Được cấp phát bộ nhớ 1 lần duy nhất ngay khi biên dịch chương trình 
    - Có thể dùng chung cho mọi đối tượng 
    - Truy xuất trực tiếp từ tên lớp mà không cần khởi tạo đối tượng của lớp đó 
    - Được hủy khi kết thúc chương trình 
- Biến/thuộc tính tĩnh (Static variable)
    - Là biến dùng cho mọi đối tượng thuộc lớp 
    - Cũng tương tự như hằng số nhưng linh hoạt hơn là ta có thể thay đổi giá trị khi cần thiết

## Nested Class 
- Được chia làm 2 loại 
    - Static nested classes: Là class được khai báo dạng `static` bên trong 1 class khác 
    - Non-static nested classes: Gồm 3 thứ 
        - Inner class: Khai báo 1 class không phải dạng static bên trong 1 class khác 
        - Local classes: Khai báo 1 class bên trong 1 method khác 
        - Anonymous Classes: Là class giống Inner class và Local Classes. Nó được khai báo bên trong class hoặc method mà không có tên cụ thể 

## Exception (Ngoại lệ)
- Là 1 vấn đề phát sinh trong quá trình thực thi chương trình 
- Khi xử lý ngoại lệ, luồng xử lý bị gián đoạn, chương trình, ứng dụng dừng bất thường. Được gọi là 1 đối tượng được ném tại runtime
- Được chia làm 3 loại 
    - Checked Exceptions(Ngoại lệ được kiểm tra)
    - Unchecked Exceptions (Ngoại lệ không được kiểm tra)
    - Error (Lỗi)

- Khác nhau giữa checked và unchecked exception 
    - Checked: 
        - Là ngoại lệ được kiểm tra và thông báo bởi trình biên dịch 
        - Xảy ra tại thời điểm biên dịch 
        - Là những Exception mà lập trình viên không lường trước được 

## Phân biệt authentication & authoriazation 
- Authentication : Kiểm tra khi đăng nhập vào có tồn tại không (Xác thực)
- Authoriazation(Phân quyền): Vai trò nào thì redirect đến trang đó 
    
## Dependency Injection 
- Là 1 dạng design pattern được thiết kế với mục đích nhằm ngăn chặn sự phụ thuộc giữa các class