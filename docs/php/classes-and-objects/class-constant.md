# Class Constants - Hằng số lớp: "Luật lệ bất biến"
- Mỗi class đều có những “luật lệ bất biến”, đó chính là hằng số class. Mội khi đã được ban hành, giá trị của chúng sẽ không thể thay đổi. Mặc định, hằng số sẽ được “công khai” (public) cho mọi công dân (class con, object) truy cập
- Lưu ý:
    - Class con có thể “ban hành lại” (redefine) hằng số class cha. Tuy nhiên, từ PHP 8.1.0, hằng số được khai bá là final sẽ trở thành bất khả xâm phạm ngay cả với class con
    - Giao diện (interface) cũng co thể có hằng số. Hãy tham khảo ý kiến của tài liệu để biết thêm chi tiết
    - Bạn có thể “gọi hồn” class bằng một biến. Tuy nhiên, biến này không được phép “mang danh” các từ khoá như `self`, `parent` và `static`
    - Hằng số class chỉ được “cấp phát” một lần duy nhất cho mỗi class, chứ không phải cho mỗi object
- Vd 1: Định nghĩa và sử dụng hằng số
    
    ```php
    <?php
    class MyClass
    {
        const CONSTANT = 'Giá trị hằng số';
    
        function showConstant() {
            echo  self::CONSTANT . "\n";
        }
    }
    
    echo MyClass::CONSTANT . "\n";
    
    $classname = "MyClass";
    echo $classname::CONSTANT . "\n";
    
    $class = new MyClass();
    $class->showConstant();
    
    echo $class::CONSTANT."\n";
    ?>
    ```
    
- Hằng số đặc biệt `::class` cho phép bạn giải mã tên class đầy đủ (fully qualified class name) ngay trong quá trình biên dịch, rất hữu ích cho các class có namespace
- Vd 2: `::class` với namespace
    
    ```php
    <?php
    namespace foo {
        class bar {
        }
    
        echo bar::class; // foo\bar
    }
    ?>
    ```
    
- Vd 3: Biểu thức hằng số class
    
    ```php
    const ONE = 1;
    class foo {
        const TWO = ONE * 2;
        const THREE = ONE + self::TWO;
        const SENTENCE = 'Giá trị của THREE là '.self::THREE;
    }
    ?>
    ```
    
- Vd 4: Phạm vi hiển thị của hằng số (Từ PHP 7.1.0)
    
    ```php
    <?php
    class Foo {
        public const BAR = 'bar';
        private const BAZ = 'baz';
    }
    echo Foo::BAR, PHP_EOL;
    echo Foo::BAZ, PHP_EOL;
    ?>
    ```
    
    - Kết quả:
    
    ```php
    bar
    
    Fatal error: Uncaught Error: Cannot access private const Foo::BAZ in …
    ```
    
- Từ PHP 7.1.0 bạn có thể sử dụng modifier hiển thị (visility modifiers) để bảo mật hằng số class, giống như với property và method
