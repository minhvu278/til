# Khái niệm
- Java là ngôn ngữ thuần hướng đối tượng 
- Chạy bằng máy ảo Java, muốn thực thi phải biên dịch ra mã máy 

## JVM, JRE, JDK 
- JVM: Là môi trường dùng để chạy ứng dụng, giúp java có thể chạy trên nhiều nền tảng khác nhau (Coi như là người phiên dịch)
- JRE:
//TODO: Note sau 
jsp servlet

## Viết chương trình chạy java  
- Tạo file trong thư mục src 
    ```
    public class demo {
        public static void main(String[] args) {
            System.out.println("Hello bae");
        }
    }
    ```

## Biến trong java
- 1 số quy tắc đặt tên biến 
    - Không có khoảng trắng và kí tự đặc biệt 
    - Không được bắt đầu bằng số
    - Không được trùng nhau 
    - Không được trùng các từ khóa trong ngôn ngữ
    - Đặt theo kiểu camelCase 
- Khai báo kiểu dữ liệu rồi mới đến tên biến 
    ```
    public class demo {
        public static void main(String[] args) {

            string name; -- Khai báo biến name

            name = 'Vu Do' -- Gán giá trị

            System.out.print("Ten:"); --     Print sẽ không xuống dòng như println 
            System.out.println(name); -- In ra 
        }
    }
    ```

## Hằng 
- Là 1 biến mà giá trị không thể thay đổi trong suốt chương trình
- Dùng từ khóa final để khai báo hằng 
    ```
    final string name;
    ```

## Ép kiểu
- Chuyển từ kiểu dữ liệu này -> kiểu dữ liệu khác
- Có 2 loại ép kiểu : Ngầm định (implicit) và tường minh (explicit)
    - Ngầm định : Chuyển từ kiểu dữ liệu nhỏ -> lớn thì không cần làm gì cả 
    ```
    VD: Chuyển từ kiểu int -> long 
    public static void main(String[] args) {
            int a = 5
            long b = a -- in ra 5
        }
    ```

    - Tường minh : Chuyển từ kiểu dữ liệu lớn về nhỏ 
    ```
    VD: Chuyển từ kiểu int -> long 
    public static void main(String[] args) {
            long a = 5
            int b = (int)a -- in ra 5
    }
    ```

## Vòng lặp while 
- Lặp 
    ```
    public static void main(String[] args) {
            int i = 0;
            while (i < 10) {
                System.out.println(i);
            }
    }
    ```

## Mảng 
- Cú pháp khai báo
    <Kiểu dữ liệu > [] <Tên mảng>
    ```
    int[] a;
    ```
- Cấp phát bộ nhớ để tạo mảng
    <Tên mảng> = new <kiểu dữ liệu> [Kích cỡ mảng]
    ```
    a = new int[3]; 
    a[0] = 2;
    a[1] = 5;
    a[2] = 8;
    ```

- Mảng 2 chiều 
    ```
    int[][] a = {{1,2,3}, {4,5,6}, {7,8,9}}
    for (int i = 0; i < 3, i++) {
        for (int j = 0; j < 3; j++){
            System.out.println(a[i][j]+""));
        }
    }
    ```

## Foreach 
- Duyệt từng phần tử trong mảng cho đến hết mảng
- Cú pháp
    for <kiểu dữ liệu> <tên biến chạy> : <tên mảng>{

    }

    ```
    public static void main(String[] args) {
            int[] array = {1,2,4};

            for(int a:array) {
                System.out.println(a)
            }
    }

## Break & continue 
- Break : Dừng vòng lặp chứa nó đang chạy
    - Đúng điều kiện sẽ dừng lại luôn
- Continue : Bỏ qua 1 vòng lặp và thực hiện vòng lặp tiếp theo 
    - Bỏ qua vòng lặp chứa continue & tiếp tục thực hiện các vòng lặp tiếp theo 

## Switch case 
- Cú pháp
    switch (Biến cần kiểm tra) {
        case <giá trị>:
            <trường hợp>
            break
        default : 
            <Khi không có case nào thỏa mãn thì vào default>
    }

    - Gặp case đúng thì nó sẽ break luôn chứ không thực hiện các case sau


## Những khái niệm cơ bản của lập trình hướng đối tượng 
- Object (Đối tượng)
    - Các vật thể như: COn người, xe máy, nhà cửa, ... được gọi là đối tượng 
    - Đối tượng gồm có 2 thông tin là: Thuộc tính và phương thức 
        - Thuộc tính: Là thông tin của đối tượng (Thông tin, chiều cao,...)
        - Phương thức: Là những hành động mà đối tượng đó có thể thực hiện (Ăn, ngủ, chơi,...)

- Class 
    - Là định nghĩa của đối tượng, xây dựng lớp để tạo ra những đối tượng khác nhau 
    VD: 
        Xe máy, xe đạp, xe oto đều thuộc class là xe 

    ```
    VD: In ra tên tuổi chiều cao 
    - Tạo ra 2 class là HelloWorld và ConNguoi

    public class HelloWorld {
        public static void main(String[] args) {
            Person a = new Person(); - Person() là class gọi ở file khác
            a.name = "Vu";
            a.age = 21;
            a.height = 1.6f

            System.out.println(a.name)
            System.out.println(a.age)
            System.out.println(a.height)
        }
    }
    --
    
    public class Persion{
        String name;
        int age;
        float height;
    }

    -- Có thể dùng mảng và vòng lặp
    public class HelloWorld {
        public static void main(String[] args) {
            Persion[] a = new Person[2] - Khoi tao person gom 2 phan tu

            for(int i = 0; i < a.length; i++){
                a[i] = new Persion();
                a[i].name = "Vu " + i;
                a[i].age = i;
                a[i].height = 1.6f
            }

            for(int i = 0; i < a.length; i++){
                System.out.println(a[i].name)
                System.out.println(a[i].age)
                System.out.println(a[i].height)
            }
        }
    }

## Class
- Hàm có void thì không cần return, còn không có thì phải return 
    ```
    public class Person {
        public String name;
        public int age;

        public void eat(String foodName) {
            System.out.println(name + "is eating" + foodName);
        }

        public int getAge() {
            return age
        }
    }
    ```
- This 
    ```
    public class Person {
        public String name;
        public int age;

        public Person(String name, int age) {
            this.name = name; -- Từ khóa this ở đây hiểu như là Person.name (Person của class Person)
            this.age = age;
        }

        public void eat(String foodName) {
            System.out.println(name + "is eating" + foodName);
        }

        public int getAge() {
            return age
        }
    }

    -- Bên class gọi chỉ cần
    public class HelloWorld {
        public static void main (String[] args) {
            Person a = new Person("Vu", 23)

            a.eat("Rice");
            int age = a.getAge();
            System.out.println("He is" + age);
        }
    }

- Package: Coi như là 1 folder 
    ```
    package mypack; -- Ví dụ tên folder là mypack  
    ```

- File nào muốn sử dụng thì cần import vào 
    ```
    import mypack.Person
    ```

## Phạm vi truy cập của biến 
- Private : Chỉ truy cập được trong nội bộ của 
- Default : Mặc định không ghi gì sẽ ở dạng default, phạm vi truy cập nằm trong nội bộ package
- Protected: Phạm vi cả trong và ngoài package nhưng phải thông qua tính kế thừa 
- Public: Có thể truy cập ở bất cứ đâu

## Static 
- Có thể gọi đến mà không cần khởi tạo đối tượng (Bình thường thì sẽ phải new gì gì đó)
- Chỉ có static mới có thể truy cập trực tiếp thông qua tên class 

## This 
- Ánh xạ đối tượng khi cần thực hiện 
- Có thể gọi được phương thức của lớp hiện tại 
    ``` 
    public class Person{
        public String name;

        public Person(String name) {
            this.name = name;
            this.getInfo(); -- Có thể gọi được phương thức getInfo
        }

        public void getInfo(){
            System.out.println("Name" + this.name)
        }
    }
    ```

## Kế thừa 
- Kế thừa lại lớp cha qua extend
- Từ khóa super mục đích là để truy cập vào các phương thức của lớp cha

## Getter & setter 
- Thường sử dụng cho private & public
- Setter: Set gía trị 
    ```
    VD: Set tuổi trong khoảng từ 0 -> 100

    public void setAge(int age){
        if(age >= 0 && age <= 100);
            this.age = age; -- Nếu điều kiện đúng thì mới cho set age 
    }

    public int getAge(){
        return this.age;
    }
    ```

## Overriding & Overloading 
- Overriding: Thăng con ghi đè thằng cha 
    - Nếu muốn thằng con k ghi đè được thằng cha thì thêm từ khóa final vào trước kiểu trả về của thằng cha 

- Overloading: Nhiều phương thức trong 1 lớp có chung tên nhưng khác tham số truyền vào
    ```
    VD: Với setter cho thuộc tính age, có thể người dùng truyền tham số age kiểu int, byte, long. Ta phải Overloading nhiều phương thức cho thuộc tính age để đảm bảo

    public void setAge(int age){
        if(age >= 0 && age <= 100);
            this.age = age; 
    }

    public void setAge(byte age){
        if(age >= 0 && age <= 100);
            this.age = age; 
    }

    public void setAge(long age){
        if(age >= 0 && age <= 100);
            this.age = age; 
    }
    ```

## Trừu tượng 
- VD: Tạo tính năng gửi tin nhắn, ta chỉ cần hiểu người dùng viết tin nhắn rồi nhấn gửi đi 
- Như vậy tính trừu tượng che giấu thông tin thực hiện từ người dùng , họ chỉ biết tính năng được cung cấp (Chỉ biết thông tin đối tượng thay vì sử dụng nó như nào)
- Có thể hiểu nôm na là trừu tượng là sẽ hình dung ra tính năng ấy sẽ hoạt động như nào rồi tạo ra khung sườn(Chưa code)

## Trừu trượng trong java
- Là lớp được khai báo mà không thể tạo ra đối tượng từ lớp đó. Ta sẽ tạo lớp con kế thừa lớp trừu tượng 
- Để tạo lớp trừu tượng ta dùng từ khóa abstract trước từ khóa class 
    ```
    public abstract class Person {

    }
    ```
    - Khi đã đặt là abstract thì sẽ không thể tạo instance cho class đó nữa 
    - Chỉ có những lớp kế thừa mới có thể sử dung được

- Phương thức trừu tượng 
    - Muốn sử dụng được thì phải định nghĩa lại ở trong phương thức kế thừa 
    ```
    public abstract Object demo();

    -- Override
    public Object demo(){
        Student other = new Student(this.name, this.age)
        return other;
    }

## Interface 
- Đặc điểm : 
    - Không thể khởi tạo nên không có phương thức khởi tạo 
    - Tất cả các phương thức trong interface luôn ở dạng public abstract mà k cần khai báo 
    - Các thuộc tính trong interface luôn ở dạng public static final mà k cần khai báo, yêu cầu có giá trị 
    - Chỉ có thể extends 1 class duy nhất nhưng có thể implement bao nhiêu interface cũng được

    ```
    VD: Tạo ra interface IStudy dành riêng cho class student 

    interface IStudy { -- Nên đặt chữ I đằng trước để nhận biết là interface
        void study();
    }

    -- Cho class Student kế thừa
    public class Student extends Person implements IStudy{ -- Vừa kế thừa Person vừa implement IStudy 

    }
    ```
- Nếu thằng cha implement 1 interface nào đó thì thằng con cung phải override lại cả 

## Hàm main trong java 
- Ý nghĩa của từng cú pháp trong phương thức main 
    - public : Phải để quyền truy cập ở dạng public để JRE ở bên ngoài có thể truy cập được 
    - static: Khi JRE bắt đầu chưa có đối tượng nào được khởi tạo. Vì vậy ta để phương thức ở dạng static để JVM có thể load class vào bộ nhớ và có thể gọi phương thức 
    - void: Phương thức main bắt buộc là void

## Try catch 
- Try catch có nhiệm vụ bắt lỗi mà thực tế có thể xảy ra để xử lý sao cho trương trình thân thiện với người dùng hơn 
- Cú pháp 
    ```
    try {
        // những khối lệnh phát sinh lỗi 
    } catch(Exception e) { // Tham số e là tên lỗi muốn xử lý 
        // Chương trình thực hiện khi gặp lỗi trên 
    }

## 4 tính chất của hướng đối tượng 
- Tính đóng gói
- Tính trừu tượng
- Tính kế thừa 
- Tính đa hình

- Ý nghĩa của mỗi tính chất
    - Tính đóng gói 
        - Tính chất này đảm bảo sự bảo mật toàn vẹn của đối tượng trong java
        - Nhằm bảo vệ đối tượng không bị truy cập từ code bên ngoài vào
        - Việc cho phép truy cập các giá trị của đối tượng tùy theo sự đồng ý của người viết ra đối tượng đó 

    - Tính trừu trượng
        - Khi code của mình cho người khác sử dụng mà k muốn người khác sử dụng sai cái mình mong muốn 
        
    - Tính kế thừa
        - Cho phép cải tiến chương trình bằng cách kế thừa lại lớp cũ và phát triển những tính năng mới 
        - Lớp con kế thừa lớp cha có thể sử dụng được các thuộc tính và phương thức của lớp cha mà không cần định nghĩa lại

    - Tính đa hình 
        - Luôn tồn tại song song với tính kế thừa 
        - Tính đa hình là kết quả tất yếu khi ta phát triển khả năng kế thừa và nâng cấp chương trình 


## Note
- Để nhập được input trong java thì phải gọi đến class Scanner 
- System out : In ra màn hình
- System in : Nhập vào
- Gõ chuỗi kí tự : scanner.nextLine();
- Tạo đường dẫn tới file nào đó sử dụng class Path
    ```
    Path path = Path.of("Data.txt")
    ```

    - Nếu k có Path.of ta có thể sử dụng Paths.get()

    - Load file
    ```
    Files.readAllLines(path);
    ```

    - Gọi sẽ trả dữ liệu vào 1 object có kiểu là list string 
    ```
    List<String> data_list = Files.readAllLines(path);
    ```

    - Chuyển kiểu 
    ```
    String [] data = idol_data.split(";")
    ```

- constrains() : Trả về true hoặc false 


## Annotation
- @PostContructor : Giống như hàm dựng, vừa vào sẽ chạy luôn


## String 

### Đối tượng string
- 