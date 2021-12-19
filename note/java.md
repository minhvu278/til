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
- Có thể sử dụng trực tiếp mà không cần đến đối tượng
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

- Getter & setter 

