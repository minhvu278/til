# Properties - Đặc điểm nhận dạng của object

- Các biến thành viên trong class được gọi là properties. Chúng có thể được gọi bằng những cái tên mỹ miều khác như “trường” (fields)
- Để nhận diện một property, bạn cần ít nhất một “dấu hiệu đặc trưng” (modifier), chẳng hạn như
    - Phạm vi hiển thị (visibility): `public, private, protected` - quy định ai được phép tiếp cận property
    - Từ khoá tĩnh (Static keyword): `static` - biến property thành “tài sản chung” của cả class
    - Từ khoá chỉ đọc (readonly): `readonly` (từ PHP 8.1.0) - biến property thành “bất khả xâm phạm” sau khi khởi tạo
- Sau khi “dấu hiệu đặc chưng” bạn có thể (tuỳ chọn) “gắn mác” kiểu dữ liệu (Type declaration) cho property (trừ readonly), và cuối cùng là khai báo biến như bình thường. Bạn cũng có thể “gán giá trị” ban đầu cho property, nhưng phải là giá trị hằng số
- Lưu ý
    - Cách khai bá property “lỗi thời” bằng từ khoá var đã bị lãng quên. Hãy update bằng cách sử dụng modifier!
    - Nếu bạn quên không ghi phạm vi hiển thị, property sẽ tự động mặc định là public
- Bên trong method của class, bạn có thể truy cập property không tĩnh bằng toán tử `->`: `$this->property_name`, còn property tĩnh được truy cập bằng toán tử `::`: `self::$property_name`
- `$this` lại xuất hiện! Nó đại diện cho object đang gọi method và chỉ “hiện hình” bên trong method của class khi được gọi từ ngữ cảnh của object
- Vd 1: Khai báo property
    
    ```php
    <?php
    class SimpleClass
    {
       public $var1 = 'hello ' . 'world';
       public $var2 = <<<EOD
    hello world
    EOD;
       public $var3 = 1+2;
       // Khai báo thuộc tính không hợp lệ:
       public $var4 = self::myStaticMethod();
       public $var5 = $myVar;
    
       // Khai báo thuộc tính hợp lệ:
       public $var6 = myConstant;
       public $var7 = [true, false];
    
       public $var8 = <<<'EOD'
    hello world
    EOD;
    
       // Không có modifier hiển thị:
       static $var9;
       readonly int $var10;
    }
    ?>
    ```
    
- Lưu ý: Có rất nhiều hàm hỗ trợ xử lý class và object. Hãy tham khảo thêm về Class/Object Functions

### Khai báo kiể dữ liệu: Gắn mác cho property

- Từ PHP 7.4.0, bạn có thể gán mác kiểu dữ liệu cho property (trừ callable)
- Vd 2: Property có kiểu dữ liệu
    
    ```php
    
    class User
    {
        public int $id;
        public ?string $name;
    
        public function __construct(int $id, ?string $name)
        {
            $this->id = $id;
            $this->name = $name;
        }
    }
    
    $user = new User(1234, null);
    
    var_dump($user->id);
    var_dump($user->name);
    
    ?>
    ```
    
    - Kết quả
    
    ```php
    int(1234)
    NULL
    ```
    
- Bạn phải khởi tạo property có kiểu dữ liệu trước khi truy cập, nếu không PHP sẽ ném ra lỗi
- Vd 3: Truy cập property
    
    ```php
    
    class Shape
    {
        public int $numberOfSides;
        public string $name;
    
        public function setNumberOfSides(int $numberOfSides): void
        {
            $this->numberOfSides = $numberOfSides;
        }
    
        public function setName(string $name): void
        {
            $this->name = $name;
        }
    
        public function getNumberOfSides(): int
        {
            return $this->numberOfSides;
        }
    
        public function getName(): string
        {
            return $this->name;
        }
    }
    
    $triangle = new Shape();
    $triangle->setName("triangle");
    $triangle->setNumberofSides(3);
    var_dump($triangle->getName());
    var_dump($triangle->getNumberOfSides());
    
    $circle = new Shape();
    $circle->setName("circle");
    var_dump($circle->getName());
    var_dump($circle->getNumberOfSides());
    ?>
    ```
    
    - Kết quả
    
    ```php
    string(8) "triangle"
    int(3)
    string(6) "circle"
    
    Fatal error: Uncaught Error: Typed property Shape::$numberOfSides must not be accessed before initialization
    ```
    

### **Thuộc tính chỉ đọc (Readonly Properties): "Bất khả xâm phạm"**

- Từ PHP 8.1.0, property có thể được “bảo vệ” bằng modifier `readonly`. Khi đó, mọi nỗ lực thay đổi giá trị của property sau khi khởi tạo sẽ bị PH ngăn chặn
- Vd 4: Property readonly
    
    ```php
    
    class Test {
       public readonly string $prop;
    
       public function __construct(string $prop) {
           // Khởi tạo hợp lệ.
           $this->prop = $prop;
       }
    }
    
    $test = new Test("foobar");
    // Đọc giá trị - Hợp lệ.
    var_dump($test->prop); // string(6) "foobar"
    
    // Gán lại giá trị - Không hợp lệ, ngay cả khi giá trị giống nhau.
    $test->prop = "foobar";
    // Lỗi: Cannot modify readonly property Test::$prop
    ?>
    ```
    
- Lưu ý:
    - Bạn chỉ có thể sử dụng modifier `readonly` cho property có kiểu dữ liệu. Nếu bạn muốn tạo property `readonly` không có ràng buộc kiểu, hãy sử dụng kiểu `Mixed`
    - Property `readonly static` hiện chưa được “hỗ trợ”
- Vd 5: Khởi tạo property readonly không hợp lệ
    
    ```php
    class Test1 {
        public readonly string $prop;
    }
    
    $test1 = new Test1;
    // Khởi tạo bên ngoài phạm vi private - Không hợp lệ.
    $test1->prop = "foobar";
    // Lỗi: Cannot initialize readonly property Test1::$prop from global scope
    ?>
    ```
    
- Lưu ý: Bạn không được phép gán giá trị mặc định (default value) cho property `readonly`, vì nó sẽ biến thành hằng số - “vô dụng” trong trường hợp này
    
    ```php
    
    class Test {
        // Lỗi nghiêm trọng: Readonly property Test::$prop cannot have default value
        public readonly int $prop = 42;
    }
    ?>
    ```
    
    - Bạn không thể sử dụng `unset()` để xoá bỏ property `readonly` sau khi nó đã được khởi tạo. Tuy nhiên, bạn có thể xoá bỏ nó trước khi khởi tạo, nhưng phải nằm trong phạm vi khai báo
- Ngoài gán giá trị trực tiếp, các hành động sau cũng bị coi là “thay đổi” giá trị và sẽ “gặp hoạ” với lỗi Error
    
    ```php
    
    class Test {
        public function __construct(
            public readonly int $i = 0,
            public readonly array $ary = [],
        ) {}
    }
    
    $test = new Test;
    $test->i += 1;
    $test->i++;
    ++$test->i;
    $test->ary[] = 1;
    $test->ary[0][] = 1;
    $ref =& $test->i;
    $test->i =& $ref;
    byRef($test->i);
    foreach ($test as &$prop);
    ?>
    ```
    
- Tuy nhiên, readonly không có nghĩa là “đóng băng” hoàn toàn. Object (hoặc tài nguyên) được lưu trữ trong property `readonly` vẫn có thể bị “biến đổi” nội dung
    
    ```php
    
    class Test {
        public function __construct(public readonly object $obj) {}
    }
    
    $test = new Test(new stdClass);
    // Biến đổi nội dung - Hợp lệ.
    $test->obj->foo = 1;
    // Gán lại đối tượng - Không hợp lệ.
    $test->obj = new stdClass;
    ?>
    ```
    

### **Thuộc tính động (Dynamic Properties): "Linh hoạt" nhưng "nguy hiểm"**

- Nếu bạn cố tình “gán giá trị” cho một property “không tồn tại” trong object, PHP sẽ tự động tạo ra property đó. Tuy nhiên, property động này chỉ “sống sót” trong phạm vi của object hiện tại
- Cảnh báo:
    - Property động đã bị khai tử từ 8.2.0. Thay vào đó, bạn nên khai báo rõ ràng property. Để xử lý các tên property “không thể đoán trước”, hãy sử dụng method `__get()` và `__set()`. Trong trường hợp bất khả kháng, bạn có thể sử dụng property `#[AllowDynamicProperties]`.
