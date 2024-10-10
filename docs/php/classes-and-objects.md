# Classes and Objects

- PHP đi kèm với một mô hình object model. Một số tính năng của nó gồm
    - **Visibility (Nhìn thấy hay không)**: Như chơi trốn tìm, cho phép bạn quyết định property và method nào được lộ diện ra bên ngoài
    - **Abstract and final classes and methods (Class và method trừu tượng cuối cùng)**: Giống như bản thiết kế sơ bộ (abstract) và bản hoàn thiện (final), không thể sửa đổi thêm
    - **Addtional magic methods (Phương thức ma thuật bổ sung)**: Những method “Bí ẩn” giúp bạn tuỳ biến cách thức hoạt động của object
    - **Interfaces (Giao diện)**: Như một “hợp đồng” mà các class phải tuân thủ, đảm bảo tính nhất quán trong code
    - **Cloning (Nhân bản)**: Giống như “Nhân bản vô tính”, tạo ra một bản sao của object
- PHP xử ly các object giống như cách nó xử lý các tham chiếu (references) hay “tay nắm cửa” (handles). Nghĩa là mỗi biến sẽ chứa một “tay nắm cửa” trỏ đến object, thay vì là một bản sao chép toàn bộ object. Hãy xem thêm về “bi kíp” này tạo `Object and References (Đối tượng tham chiếu)`

# The basic

## class

- Hãy tưởng tượng class như một bản thiết kế (blueprint) để tạo ra các object
- Để “vẽ” bản thiết kế này, ta dùng từ khoá `class`, tiếp theo là tên class do bạn đặt, rồi đến cặp `{}` bảo quanh các properties và method của class
- Tên class
    - Bắt đầu bằng chữ cái hoặc dấu `_`
    - Tiếp theo là chữ cái, số, hoặc dấu gạch dưới
    - Không được trùng với các từ khoá cấm của PHP
    - VD” `hero123`, `_siunhan`, `nguoi_doi`,…
- Bên trong class có gì?
    - **Constants (hằng số)**: Giống như “kim chỉ nam”, giá trị không đổi
    - **Properties (thuộc tính)**: Đặc điểm của object, như sức mạnh, tốc độ
    - **Methods (phương thức)**: Hành động của object như bay, chạy
    
    ```php
    <?php
    class SimpleClass
    {
        // Khai báo thuộc tính
        public $var = 'Giá trị mặc định';
    
        // Khai báo phương thức
        public function displayVar() {
            echo $this->var;
        }
    }
    ?>
    ```
    
- **$this -**
    - Khi một method được gọi từ một object, `$this` sẽ xuất hiện. $this chính là đại diện cho object đang gọi method đó
- Cảnh báo
    - Từ 8.0.0, gọi method không phải static một cách lén lút (static) sẽ bị lỗi
    - Trước đó, PHP chỉ nhắc nhở (deprecation notice) và $this sẽ “mất tích”

```php
<?php
class A
{
    function foo()
    {
        if (isset($this)) {
            echo '$this đã xuất hiện (';
            echo get_class($this);
            echo ")\n";
        } else {
            echo "\$this đã "biến mất".\n";
        }
    }
}

class B
{
    function bar()
    {
        A::foo();
    }
}

$a = new A();
$a->foo();

A::foo();

$b = new B();
$b->bar();

B::bar();
?>
```

- Kết quả trong PHP 7
    
    ```php
    $this đã xuất hiện (A)
    
    Deprecated: Non-static method A::foo() should not be called statically in %s  on line 27
    $this đã "biến mất".
    
    Deprecated: Non-static method A::foo() should not be called statically in %s  on line 20
    $this đã "biến mất".
    
    Deprecated: Non-static method B::bar() should not be called statically in %s  on line 32
    
    Deprecated: Non-static method A::foo() should not be called statically in %s  on line 20
    $this đã "biến mất".
    ```
    
- Kết quả trong PHP 8
    
    ```php
    $this đã xuất hiện (A)
    
    Fatal error: Uncaught Error: Non-static method A::foo() cannot be called statically in %s :27
    Stack trace:
    #0 {main}
      thrown in %s  on line 27
    ```
    

### **Readonly classes**

- Từ PHP 8.2.0, class được trang bị thêm “readonly”, biến chúng thành những “pháo đài bất khả xâm phạm”. Khi class được bảo vệ bởi `readonly`
    - Mọi properties khai bá trong class đều trở thành bất khả xâm phạm (readonly), không ai có thể thay đổi giá trị của chúng
    - Việc tạo thêm property động (dynamic properties) là điều “không tưởng”
    - Ngay cả khi property static cũng bị “cấm cửa”
    
    ```php
    <?php
    readonly class Foo { // Lớp "An Toàn Tuyệt Đối"
        // ...
    }
    
    // Fatal error: Cannot apply #[AllowDynamicProperties] to readonly class Foo
    ?>
    ```
    

### new

- Để biến class thành object thực sự, bạn cần đến từ khoá `new`. Object sẽ được tạo ra như có magic, trừ khi constructor của class phát hiện lỗi và ném ra exception
- **Note:**
    - Hãy “vẽ” bản thiết kế (định nghĩa class) trước khi khởi tạo object, giống như bạn cần có công thức trước khi nấu ăn vậy
    - Nếu một biến chứa chuỗi là tên của một class được sử dụng với new, một object mới của class đó sẽ được tạo ra. Nếu class nằm trong một namespace, bạn cần sử dụng tên đầy đủ cho nó
    - Nếu “kiến trúc sư” không cần thêm tham số nào, bạn có thể rút gọn bằng cách bỏ qua `()` sau tên class
    
    ```php
    <?php
    $instance = new SimpleClass(); // "Triệu hồi" đối tượng từ lớp SimpleClass
    
    // Hoặc "biến hóa" với biến:
    $className = 'SimpleClass';
    $instance = new $className(); // Tương đương với new SimpleClass()
    ?>
    ```
    
- Từ 8.0.0, `new` còn bá hơn khi hỗ trợ các biểu thức bất kỳ. Điều này cho phép bạn “triệu hồi” object một cách linh hoạt hơn
- Vd 4: Triệu hồi object bằng biểu thức bất kỳ
    
    ```php
    
    class ClassA extends \stdClass {}
    class ClassB extends \stdClass {}
    class ClassC extends ClassB {}
    class ClassD extends ClassA {}
    
    function getSomeClass(): string
    {
        return 'ClassA';
    }
    
    var_dump(new (getSomeClass()));
    var_dump(new ('Class' . 'B'));
    var_dump(new ('Class' . 'C'));
    var_dump(new (ClassD::class));
    ?>
    ```
    
    - Kết quả
    
    ```php
    object(ClassA)#1 (0) {
    }
    object(ClassB)#1 (0) {
    }
    object(ClassC)#1 (0) {
    }
    object(ClassD)#1 (0) {
    }
    ```
    
- Trong ngữ cảnh của class, bạn có thể tạo một object mới bằng `new self` và `new parent`
- Khi gán một object đã tồn tại cho một biến mới, biến mới này sẽ “ nắm tay” object gốc và “cùng chung một con đường”. Điều này cũng đúng khi bạn truyền tham số cho các hàm. Muốn tạo ra một “bản sao” độc lập, bạn cần dùng đến `clone`
- VD 5: Gán object
    
    ```php
    <?php
    
    $instance = new SimpleClass();
    
    $assigned   =  $instance;
    $reference  =& $instance;
    
    $instance->var = '$assigned sẽ có giá trị này';
    
    $instance = null; // $instance và $reference cùng "bay màu"
    
    var_dump($instance);
    var_dump($reference);
    var_dump($assigned);
    ?>
    ```
    
    - Kết quả
    
    ```php
    NULL
    NULL
    object(SimpleClass)#1 (1) {
       ["var"]=>
         string(30) "$assigned sẽ có giá trị này"
    }
    ```
    
- Bạn có thể “triệu hồi” object bằng nhiều cách ảo diệu khác nhau
    
    ```php
    <?php
    
    class Test
    {
        public static function getNew()
        {
            return new static();
        }
    }
    
    class Child extends Test {}
    
    $obj1 = new Test(); // "Triệu hồi" bằng tên lớp
    $obj2 = new $obj1(); // "Triệu hồi" qua biến chứa đối tượng
    var_dump($obj1 !== $obj2);
    
    $obj3 = Test::getNew(); // "Triệu hồi" bằng phương thức lớp
    var_dump($obj3 instanceof Test);
    
    $obj4 = Child::getNew(); // "Triệu hồi" qua phương thức lớp con
    var_dump($obj4 instanceof Child);
    
    ?>
    ```
    
    - Kết quả
    
    ```php
    bool(true)
    bool(true)
    bool(true)
    ```
    
- Bạn có thể truy cập thành viên của object mới được tạo trong một biểu thức
    
    ```php
    2023
    ```
    
    - Lưu ý: Trước PHP 7.1, các tham số sẽ không được đánh giá nếu không có hàm tạo được định nghĩa

### Property and method

- 2 thằng này giống như “anh em” sống chung “một mái nhà” nhưng ở “phòng riêng” (namespaces). Điều này co nghĩa là bạn có thể có một property và một method cùng tên mà không sợ “choảng nhau”. Các truy cập của chúng cũng giống nhau, nhưng hành động được thực hiện (truy cập property hay gọi method) sẽ phụ thuộc vào ngữ cảnh
- Vd 8: truy cập property và gọi method
    
    ```php
    <?php
    class Foo
    {
        public $bar = 'property';
        
        public function bar() {
            return 'method';
        }
    }
    
    $obj = new Foo();
    echo $obj->bar, PHP_EOL, $obj->bar(), PHP_EOL;
    ?>
    ```
    
    - Kết quả
    
    ```php
    property
    method
    ```
    
- Vì “sống chung nhà” nhưng “khác phòng”, bạn không thể gọi trực tiếp một hàm ẩn danh được gán cho property. Thay vào đó, bạn cần “mời” property đó vào một biến trước. Hoặc bạn có thể gọi trực tiếp bằng cách “đóng gói” nó trong ngoặc đơn
- Vd 9: Gọi hàm ẩn danh được lưu trữ trong property
    
    ```php
    <?php
    class Foo
    {
        public $bar;
        
        public function __construct() {
            $this->bar = function() {
                return 42;
            };
        }
    }
    
    $obj = new Foo();
    
    echo ($obj->bar)(), PHP_EOL;
    ?>
    ```
    
    - Kết quả
    
    ```php
    42
    ```
    

### extends

- Một class có thể “kế thừa” hằng số, method và property từ class khác bằng cách sử dụng từ khoá `extends` trong khai báo class. Tuy nhiên, một class chỉ có thể “kế thừa” từ một class cha duy nhất, không thể “tham lam” muốn có nhiều “gia tài” cùng lúc
- Lớp con có thể “ghi đè” (override) các hằng số, method và property được kế thừa bằng cách khai báo lại chúng với cùng tên đã được định nghĩa trong class cha. Tuy nhiên, nếu class cha đã “khoá chặt” method hoặc hằng số bằng từ khoá `final`, lớp con sẽ không thể “động chạm” đến chúng
- Để truy cập method hoặc property tĩnh đã bị “ghi đè”, bạn có thể sử dụng `parent::`
- Lưu ý: từ PHP 8.1.0, hằng số có thể khai báo là `final`
- VD 10: Kế thừa đơn giản
    
    ```php
    <?php
    class ExtendClass extends SimpleClass
    {
        // Ghi đè phương thức của lớp cha
        function displayVar()
        {
            echo "Lớp mở rộng\n";
            parent::displayVar();
        }
    }
    
    $extended = new ExtendClass();
    $extended->displayVar();
    ?>
    ```
    
    - Kết quả
    
    ```php
    Lớp mở rộng
    Giá trị mặc định
    ```
    

### **Quy tắc tương thích chữ ký: "Luật bất thành văn" khi ghi đè**

- Khi ghi đè một method, chữ ký của nó phải tương thích với method cha. Nếu không PHP sẽ ném ra lỗi nghiêm trọng. Trước PHP 8.0.0, bạn sẽ chỉ nhận được 1 cảnh báo nhẹ nhàng (E_WARNING)
- Chữ ký được coi là tương thích nếu nó tuân thủ các quy tắc về variance, biến tham số bắt buộc thành tuỳ chọn, chỉ thêm tham số tuỳ chọn mới và không được phép hạn chế phạm vi hiển thị (visiblity). Nguyên tắc này được gọi là nguyên tắc thay thế Liskov (Liskov Substitution Principle), hay LSP. Hàm tạo và method private được miễn trừ khỏi quy tắc này
- Vd 11: Method con tương thích
    
    ```php
    <?php
    
    class Base
    {
        public function foo(int $a) {
            echo "Hợp lệ\n";
        }
    }
    
    class Extend1 extends Base
    {
        function foo(int $a = 5)
        {
            parent::foo($a);
        }
    }
    
    class Extend2 extends Base
    {
        function foo(int $a, $b = 5)
        {
            parent::foo($a);
        }
    }
    
    $extended1 = new Extend1();
    $extended1->foo();
    $extended2 = new Extend2();
    $extended2->foo(1);
    ?>
    ```
    
    - Kết quả
    
    ```php
    Hợp lệ
    Hợp lệ
    ```
    
- Các ví dụ sau đây cho thấy method con xoá tham số hoặc biến tham số tuỳ chọn thành bắt buộc sẽ không tương thích với method cha
- VD 12: Lỗi nghiêm trọng khi method con xoá tham số
    
    ```php
    <?php
    
    class Base
    {
        public function foo(int $a = 5) {
            echo "Hợp lệ\n";
        }
    }
    
    class Extend extends Base
    {
        function foo()
        {
            parent::foo(1);
        }
    }
    ?>
    ```
    
    - Kết quả trong PHP 8
    
    ```php
    Fatal error: Declaration of Extend::foo() must be compatible with Base::foo(int $a = 5) in /in/evtlq on line 13
    ```
    
- Vd 13: Lỗi nghiêm trọng khi method con biến tham số tuỳ chọn thành bắt buộc
    
    ```php
    <?php
    
    class Base
    {
        public function foo(int $a = 5) {
            echo "Hợp lệ\n";
        }
    }
    
    class Extend extends Base
    {
        function foo(int $a)
        {
            parent::foo($a);
        }
    }
    ?>
    ```
    
    - Kết quả trong PHP 8
    
    ```php
    Fatal error: Declaration of Extend::foo(int $a) must be compatible with Base::foo(int $a = 5) in /in/qJXVC on line 13
    ```
    
- Cảnh báo: Đổi tên tham số của method trong class con không phải là lỗi không tương thích chữ ký. Tuy nhiên, bạn nên tránh làm điều này vì nó có thể dẫn đến lỗi trong thời gian chạy nếu sử dụng tham số có tên
- Vd 14: Lỗi khi sử dụng tham số có tên và tham số đã được đổi tên trong class con
    
    ```php
    <?php
    
    class A {
        public function test($foo, $bar) {}
    }
    
    class B extends A {
        public function test($a, $b) {}
    }
    
    $obj = new B;
    
    // Truyền tham số theo A::test()
    $obj->test(foo: "foo", bar: "bar"); // LỖI!
    ?>
    ```
    
    - Kết quả
    
    ```php
    Fatal error: Uncaught Error: Unknown named parameter $foo in /in/XaaeN:14
    Stack trace:
    #0 {main}
      thrown in /in/XaaeN on line 14
    ```
    

### `::class` - Điệp viên 007 trong class

- `class` keyword còn có thể được sử dụng để giải mã tên class. Để lấy tên đầy đủ của class `ClassName`, bạn có thể sử dụng `ClassName::class`. Tính năng này đặc biệt hữu ích với các class có namespace
- Vd 15: Giải mã tên class
    
    ```php
    <?php
    namespace NS {
        class ClassName {
        }
        
        echo ClassName::class;
    }
    ?>
    ```
    
    - Kết quả
    
    ```php
    NS\ClassName
    ```
    
- Lưu ý: Việc “giải mã” tên class bằng `::class` diễn ra trong quá trình biên dịch. Điều này có nghĩa là tại thời điểm chuỗi tên class được tạo, quá trình tự động tải (autoloading) chưa diễn ra. Do đó, tên class sẽ được mở rộng ngay cả khi class đó không tồn tại. Trong trường hợp này, sẽ không có lỗi nào được đưa ra
- Vd 16: Giải mã tên class không tồn tại
    
    ```php
    <?php
    print Does\Not\Exist::class;
    ?>
    ```
    
    - Kết quả
    
    ```php
    Does\Not\Exist
    ```
    
- Từ PHP 8.0.0, `::class` cũng có thể được sử dụng trên các object. Quá trình giải mã này diễn tra trong thời gian chạy, không phải thời gian biên dịch. Hiệu ứng của nó giống như việc gọi `get_class()` trên object
- Vd 17: Giải mã trên class của object
    
    ```php
    <?php
    namespace NS {
        class ClassName {
        }
    }
    $c = new ClassName();
    print $c::class;
    ?>
    ```
    
    - Kết quả
    
    ```php
    NS\ClassName
    ```
    

### Method và property “an toàn” với null: Miễn nhiêm với null

- Từ PHP8.0.0 bạn có thể truy cập property và method một cách an toàn hơn với toán tử “nullsafe”: `?->`. Toán tử này hoạt động tương tự như cách truy cập thông thường, nhưng nếu object là null, nó sẽ trả về null thay vì ném ra lỗi. Nếu truy cập là một phần của chuỗi, phần còn lại sẽ bị bỏ qua
- Hiệu ứng này giống như việc bạn bọc mỗi lần truy cập trong một kiểm tra `is_null()`, nhưng gọn gàng hơn nhiều
    
    ```php
    <?php
    
    // As of PHP 8.0.0, this line:
    $result = $repository?->getUser(5)?->name;
    
    // Is equivalent to the following code block:
    if (is_null($repository)) {
        $result = null;
    } else {
        $user = $repository->getUser(5);
        if (is_null($user)) {
            $result = null;
        } else {
            $result = $user->name;
        }
    }
    ?>
    ```
