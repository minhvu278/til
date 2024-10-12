# **Autoloading Classes - Tự động tải lớp: "Giải phóng" khỏi mớ include**

- Khi xây dựng những “ứng dụng đồ sộ” với lập trình hướng đối tượng, việc tạo một file PHP cho mỗi class là điều không thể tránh khỏi. Tuy nhiên, “ác mộng” sẽ bắt đầu khi bạn phải viết một “loạt” `include` dài dằng dặc ở đầu mỗi file để sử dụng các class cần thiết
- Đừng lo, `spl_autoload_register()` sẽ “giải phóng” bạn khỏi mớ “include” rườm rà đó! Hàm này cho phép bạn đăng ký một hoặc nhiều “trợ lý” autoloader, giúp tự động tải các class và interface chưa được định nghĩa. Nhờ đó, PHP sẽ có “cơ hội cuối cùng” để tải class trước khi báo lỗi
- Mọi cấu trúc “giống class” (class-like construct) đều có thể được tự động tải theo cách này bao gồm:
    - Lớp (classes)
    - Giao diện (interfaces)
    - Trait
    - Kiểu liệt kê (enumerations)
- Cảnh báo
    - Trước PHP 8.0.0, bạn có thể sử dụng `__autoload()` để tự động tải class và interface. Tuy nhiên hàm này “kém linh hoạt” hơn `spl_autoload_register()` và đã bị khai từ từ PHP 7.2.0 và xoá hoàn toàn trong PHP 8.0.0
    - Bạn có thể gọi `spl_autoload_register()` nhiều lần để đăng ký nhiều trợ lý autoloader. Tuy nhiên, nếu một hàm autoloader “nổi loạn” và ném ra lỗi, quá trình tự động tải sẽ bị “gián đoạn”. Vì vậy, hãy “nhắc nhở” các hàm autoloader của bạn “giữ bình tĩnh” và tránh ném ra lỗi
- Vd 1: Tự động tải class
    - Ví dụ này minh hoạ cách tải các class `MyClass1` và `MyClass2` từ các file `MyClass1.php và MyClass2.php` tương ứng
    
    ```php
    <?php
    spl_autoload_register(function ($class_name) {
        include $class_name . '.php';
    });
    
    $obj  = new MyClass1();
    $obj2 = new MyClass2(); 
    ?>
    ```
    
- Vd 2: Tự động tải interface
    - Ví dụ này minh hoạt cách tải interface `ITest`
    
    ```php
    
    spl_autoload_register(function ($name) {
        var_dump($name);
    });
    
    class Foo implements ITest {
    }
    
    /*
    string(5) "ITest"
    
    Fatal error: Interface 'ITest' not found in ...
    */
    ?>
    ```
    
- Xem thêm
    - unserialize()
    - unserialize_callback_func
    - unserialize_max_depth
    - spl_autoload_register()
    - spl_autoload()
    - __autoload()
