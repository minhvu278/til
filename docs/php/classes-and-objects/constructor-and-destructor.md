# **Constructors and Destructors - Hàm tạo và hàm hủy: "Sinh ra từ đâu, trở về từ đó"**

# **Hàm tạo (Constructor): "Nặn" đối tượng**

- Trong PHP, mọi object đều được tạo ra từ 1 khuôn mẫu - class. Và hàm tạo chính là người thợ đảm nhiệm trọng trách này
- Khi một object được tạo ra, hàm tạo sẽ được gọi để “khởi tạo” các property, giống như việc bạn “trang trí” cho ngôi nhà của mình trước khi dọn vào ở
- Lưu ý
    - Hàm tạo của class cha sẽ không được tự động gọi nếu class con tự định nghĩa hàm tạo riêng
    - Để “triệu hồi” hàm tạo của lớp cha, bạn cần explicitly gọi `parent::__construct()` bên trong hàm tạo của class con
    - Nếu class con lười biếng không định nghĩa hàm tạo, nó có thể kế thừa từ class cha, giống như các method thông thường (trừ khi hàm tạo của class cha được khai báo là private)
- Vd 1: Hàm tạo trong kế thừa
    
    ```php
    <?php
    class BaseClass {
        function __construct() {
            print "Trong hàm tạo của BaseClass\n";
        }
    }
    
    class SubClass extends BaseClass {
        function __construct() {
            parent::__construct(); // "Triệu hồi" hàm tạo của lớp cha
            print "Trong hàm tạo của SubClass\n";
        }
    }
    
    class OtherSubClass extends BaseClass {
        // "Kế thừa" hàm tạo của BaseClass
    }
    
    // In BaseClass constructor
    $obj = new BaseClass();
    
    // In BaseClass constructor
    // In SubClass constructor
    $obj = new SubClass();
    
    // In BaseClass constructor
    $obj = new OtherSubClass();
    ?>
    ```
    
- Không giống như các method khác, hàm tạo `__construct()` được miễn trừ khỏi các quy tắc tương thích chữ ký khi kế thừa
- Hàm tạo là method “bình thường” được gọi trong quá trình khởi tạo object. Do đó, chúng có thể tự do khai báo số lượng tham số tuỳ ý, là bắt buộc hay tuỳ chọn, có kiểu dữ liệu hay không và có giá trị mặc định hay không
- Vd 2: Sử dụng tham số trong hàm tạo
    
    ```php
    <?php
    class Point {
        protected int $x;
        protected int $y;
    
        public function __construct(int $x, int $y = 0) {
            $this->x = $x;
            $this->y = $y;
        }
    }
    
    // Truyền cả hai tham số.
    $p1 = new Point(4, 5);
    // Chỉ truyền tham số bắt buộc. $y sẽ nhận giá trị mặc định là 0.
    $p2 = new Point(4);
    // Sử dụng tham số có tên (từ PHP 8.0):
    $p3 = new Point(y: 5, x: 4);
    ?>
    ```
    
- Nếu class không có hàm tạo, hoặc hàm tạo không có tham số bắt buộc, bạn có thể “lược bỏ” cặp ngoặc đơn

## **Old-style constructors**

- Trước PHP 8.0.0, với các class trong global namespace, method có tên trùng với tên class sẽ được ưu ái xem như hàm tạo kiểu cũ. Tuy nhiên cú pháp này đã lỗi thời và sẽ nhắc nhở bạn bằng lỗi `E_DEPRECATED` khi sử dụng. Nếu bạn cố chấp định nghĩa cả `__constructor()` và method trùng tên, `__constructor()` sẽ được ưu tiên gọi
- Với các class có namespace, hoặc bất kỳ class nào từ PHP 8.0.0, method trùng tên sẽ không còn ý nghĩa đặc biệt nữa
- Hãy bắt kịp xu hướng và luôn sử dụng `__constructor()` trong code mới

## **Nâng cấp hàm tạo (Constructor Promotion): "Rút gọn" mã nguồn**

- Từ PHP 8.0.0, bạn có thể “nâng cấp” tham số của hàm tạo để “gắn kết” trực tiếp với property của object. Điều này giúp bạn rút gọn code khi tham số hàm tạo thường được gán cho property mà không cần xử lý gì thêm
- Vd 3: Nâng cấp property trong hàm tạo
    
    ```php
    <?php
    class Point {
        public function __construct(protected int $x, protected int $y = 0) {
        }
    }
    ```
    
- Khi tham số hàm tạo bao gồm modifier, PHP sẽ hiểu ý bạn và xem nó vừa là property object vừa là tham số hàm tạo, và tự động gán giá trị cho property đó
- Lưu ý:
    - Bạn có thể sử dụng modifier (như `readonly`) để “nâng cấp” property, nhưng modifier hiển thị (public, protected, private) là phổ biến nhất
    - Bạn không thể “gắn mác” `callable` cho property của object. Do đó, tham số được “nâng cấp” cũng không được phép mang kiểu `callable`
    - Mọi quy tắc đặt tên cho property và tham số đều được áp dụng cho tham số được “nâng cấp”
    - Thuộc tính (attribute) được đặt trên tham số “nâng cấp” sẽ được “sao chép” cho các property và tham số. Tuy nhiên, giá trị mặc định sẽ chỉ được sao chép cho tham số

### **new trong bộ khởi tạo (initializers): "Linh hoạt" hơn**

- Từ PHP 8.1.0, bạn có thể sử dụng `new` để tạo object trong các trường hợp sau
    - Giá trị mặc định của tham số
    - Biến tĩnh (static variable)
    - Hằng số toàn cục (global constant)
    - Tham số của property (attribute)
    - Hàm define()
- Lưu ý: Bạn không được phép sử dụng tên class động (dynamic), tên class không phải chuỗi (non-string), class ẩn danh (anonymous class), giải nén tham số (agrument unpacking) và biểu thức không được hỗ trợ
- Vd 4: Sử dụng `new` trong bộ khởi tạo
    
    ```php
    
    // Hợp lệ:
    static $x = new Foo;
    
    const C = new Foo;
     
    function test($param = new Foo) {}
     
    #[AnAttribute(new Foo)]
    class Test {
        public function __construct(
            public $prop = new Foo,
        ) {}
    }
    
    // Không hợp lệ (lỗi biên dịch):
    function test(
        $a = new (CLASS_NAME_CONSTANT)(), // dynamic class name
        $b = new class {}, // anonymous class
        $c = new A(...[]), // argument unpacking
        $d = new B($abc), // unsupported constant expression
    ) {}
    ?>
    ```
    

### **Phương thức tạo tĩnh (Static Creation Methods): "Nhiều cách" để "nặn" đối tượng**

- PHP chỉ cho phép một hàm tạo duy nhất cho mỗi class. Tuy nhiên, bạn có thể sử dụng method tĩnh như một “lớp vỏ bọc” (wrapper) cho hàm tạo để tạo để tạo ra các object theo nhiều cách khác nhau
    
    ```php
    class Product {
    
        private ?int $id;
        private ?string $name;
    
        private function __construct(?int $id = null, ?string $name = null) {
            $this->id = $id;
            $this->name = $name;
        }
    
        public static function fromBasicData(int $id, string $name): static {
            $new = new static($id, $name);
            return $new;
        }
    
        public static function fromJson(string $json): static {
            $data = json_decode($json, true);
            return new static($data['id'], $data['name']);
        }
    
        public static function fromXml(string $xml): static {
            // Xử lý logic tùy chỉnh tại đây.
            $data = convert_xml_to_array($xml);
            $new = new static();
            $new->id = $data['id'];
            $new->name = $data['name'];
            return $new;
        }
    }
    
    $p1 = Product::fromBasicData(5, 'Widget');
    $p2 = Product::fromJson($some_json_string);
    $p3 = Product::fromXml($some_xml_string);
    ```
    
- Bạn có thể khai báo hàm tạo là `private` hoặc `protected` để giấu nó khỏi thế giới bên ngoài. Khi đó, chỉ method tĩnh mới có thể triệu hồi “hàm tạo”
- Trong ví dụ trên
    - `fromBasicData()`: nhận các tham số cần thiết, sau đó tạo object bằng cách gọi hàm tạo và trả về kết quả
    - `fromJson()`: Nhận một chuỗi JSON tự xử lý và chuyển đổi nó sang định dạng mà hàm tạo mong muốn, sau đó trả về object mới
    - `fromXml()` : Nhận một chuỗi XML, tự xử lý, sau đó tạo một object “trống”. Hàm tạo vẫn được gọi, nhưng vì tất cả các tham số đều là tuỳ chọn, method này sẽ bỏ qua chúng. Sau đó, nó gán giá trị trực tiếp cho các chuỗi property của object trước khi trả về kết quả
- Trong cả 3 trường hợp, từ khoá `static` được dịch thành tên của class hiện tại, trong trường hợp này là `Product`

## **Hàm hủy (Destructor): "Trả về cát bụi"**

- Cũng giống như con người, object trong PHP cũng có “sinh lão bệnh tử”. Và hàm huỷ sẽ được gọi khi object “trở về cát bụi” - không còn được tham chiếu đến nữa, hoặc trong quá trình “dọn dẹp” (shutdown sequence) của chương trình
- Vd 6: Hàm huỷ
    
    ```php
    
    class MyDestructableClass 
    {
        function __construct() {
            print "Trong hàm tạo\n";
        }
    
        function __destruct() {
            print "Đang hủy " . __CLASS__ . "\n";
        }
    }
    
    $obj = new MyDestructableClass();
    ?>
    ```
    
- Tương tự như hàm tạo:
    - Hàm huỷ của class cha sẽ không được tự động gọi
    - Bạn cần explicitly gọi `parent::_destruct()` trong hàm huỷ của lớp con để “kế thừa” nghi thức từ lớp cha
    - Lớp con có thể kế thừa hàm huỷ của lớp cha nếu nó không tự định nghĩa hàm huỷ riêng
- Hàm huỷ sẽ được gọi ngay cả khi bạn “ép buộc” chương trình dừng lại bằng `exit()`
- Lưu ý:
    - Khi hàm huỷ được gọi trong quá trình “dọn dẹp” của chương trình, HTTP header đã được gửi đi
    - Thư mục làm việc trong giai đoạn này có thể khác với một số SAPIs (ví dụ: Apache)
    - Ném ra lỗi (exception) từ hàm huỷ (trong quá trình “dọn dẹp”) sẽ gây ra lỗi nghiêm trọng
