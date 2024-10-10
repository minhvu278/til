# Type
## Introduction

- Mỗi biểu thức trong PHP đều có một trong các kiểu tích hợp sau, tuỳ thuộc vào giá trị của nó
    
    ```php
    null
    bool
    int
    float (số dấu phẩy động)
    string
    array
    object
    callable
    resource
    ```
    
- PHP là một ngôn ngữ gõ động, có nghĩa là theo mặc định không cần phải chỉ định kiểu của một biến, vì điều này sẽ được xác định trong thời gian chạy. Tuy nhiên, có thể gõ tĩnh một số khía cạnh cỉa ngôn ngữ thông qua việc sử dụng khai bá kiểu
- Các kiểu giới hạn loại thao tác có thể được thực hiện trên chúng. Tuy nhiên, nếu một biểu thức/biến được sử dụng trong một thao tác mà kiểu của nó không hỗ trợ, PHP sẽ cố gắng ép kiểu thành một kiểu hỗ trợ thao tác đó. Quá trình này phụ thuộc vào ngữ cảnh mà giá trị được sử dụng. Để biết thêm thông tin, hãy xem phần về Ép kiểu
- Lưu ý: Có thể buộc một biểu thức được đánh giá thành một kiểu nhất định bằng cách sử dụng ép kiểu. Một biến cũng có thể ép kiểu tại chỗ bằng cách sử dụng hàm `settype()` trên nó
- Để kiểm tra giá trị và kiểu của một biểu thức, hãy sử dụng hàm `var_dump()`. Để lấy kiểu của một biểu thức, hãy sử dụng `get_debug_type()`. Tuy nhiên, để kiểm tra xem một biểu thức có thuộc một kiểu nhất định hay không, hãy sử dụng hàm `is_type`
    
    ```php
    <?php
    $a_bool = true;   // một bool
    $a_str  = "foo";  // một chuỗi
    $a_str2 = 'foo';  // một chuỗi
    $an_int = 12;     // một int
    
    echo get_debug_type($a_bool), "\n";
    echo get_debug_type($a_str), "\n";
    
    // Nếu đây là một số nguyên, hãy tăng nó lên bốn
    if (is_int($an_int)) {
        $an_int += 4;
    }
    var_dump($an_int);
    
    // Nếu $a_bool là một chuỗi, hãy in nó ra
    if (is_string($a_bool)) {
        echo "String: $a_bool";
    }
    ?>
    ```
    
- Kết quả
    
    ```php
    bool
    string
    int(16)
    ```
    
- Lưu ý, trước PHP 8.0.0, khi `get_debug_type()` không khả dụng, có thể sử dụng `gettype()` thay thế. Tuy nhiên, nó không sử dụng tên kiểu chuẩn

## **Type System**

- PHP sử dụng một hệ thống kiểu danh nghĩa với một mối quan hệ kiểu con hành vi mạnh mẽ. Mối quan hệ kiểu con được kiểm tra tại thời điểm biên dịch trong khi việc xác minh kiểu được kiểm tra động trong thời gian chạy
- Hệ thống kiểu của PHP hỗ trợ nhiều kiểu nguyên tử có thể được kết hợp với nhau để tạo ra các kiểu phức tạp hơn. Một số kiểu này có thể được viết dưới dạng khai báo kiểu

### **Atomic types**

- Một số atomic types là kiểu tích hợp chặt chẽ với ngôn ngữ và không thể được tái tạo bằng các kiểu do người dùng định nghĩa
- Danh sách base type
- Kiểu tích hợp
    
    ```php
    Kiểu null
    Kiểu vô hướng:
    Kiểu bool
    Kiểu int
    Kiểu float
    Kiểu string
    Kiểu array
    Kiểu object
    Kiểu resource
    Kiểu never
    Kiểu void
    Kiểu lớp tương đối: self, parent và static
    ```
    
- Kiểu giá trị
    
    ```php
    false
    true
    ```
    
- Kiểu do người dùng định nghĩa (thường được gọi là kiểu lớp)
    
    ```php
    Giao diện
    Lớp
    Liệt kê
    Kiểu callable
    ```
    

### Composite types

- Có thể kết hợp nhiều atomic type thành kiểu phức hợp. PHP cho phép kết hợp các kiểu theo cách sau
    - Giao của class-types (interfaces and class name)
    - Union of types
    
    ### Intersection types
    
    - Một intersection types chấp nhận các giá trị thoả mãn nhiều khai báo kiểu class, thay vì chỉ một. Các kiểu riêng lẻ tạo thành intersection type được nối với nhau bằng ký hiệu `&`. Do đó một kiểu giao bao gồm các kiểu T, U và V sẽ được viết là `T&U&V`
    
    ### Union types
    
    - Chấp nhận các giá trị của nhiều kiểu khác nhau, thay vì chỉ một. Các kiểu riêng lẻ tạo thành union type được kết nối với nhau bằng `|`. Do đó một union type bao gồm các kiểu T, U và V sẽ được viết là `T|U|V`. Nếu một trong các kiểu là intersection type, nó cần được đặt trong ngoặc đơn đơn được viết ở dạng DNF: `T|(X&Y)`

### Type alias

- PHP hỗ trợ hai biệt danh kiểu: `mixed` và `iterable` tương ứng với union types của `object|resource|array|string|float|int|bool|null` và `Traversable|array`
- Lưu ý: PHP không hỗ trợ type alias do người dùng định nghĩa

## NULL

- Kiểu dữ liệu null là kiểu đơn vị (unit type) của PHP, nghĩa là nó chỉ có một giá trị duy nhất: null
- Các biến chưa được định nghĩa (undefined) và các biến đã bị huỷ (unset()) sẽ được phân giải thành giá trị null
- Chỉ có một giá trị null, và đó là hằng số không phân biệt hoa thường null
    
    ```jsx
    $var = NULL;       
    ?>
    ```
    

### Ép kiểu sang null

- **Cảnh báo**: Tính năng này đã không được dùng từ phiên bản PHP 7.2.0 và loại bỏ khỏi 8.0.0. Việc phụ thuộc vào tính năng này là không nên
- Ép kiểu 1 biến thành null bằng cách sử dụng (unset) $var sẽ không xoá biến hoặc huỷ giá trị của nó. Nó sẽ chỉ trả về giá trị null
- Xem thêm: `is_null()`, `unset()`

## Booleans

- Kiểu dữ liệu bool chỉ có 2 giá trị được sử dụng để biểu thị giá trị logic. Nó có thể là true hoặc false
- Để xác định một giá trị bool, hãy sử dụng hằng số true hoặc false. Cả 2 đều không phân biệt hoa thường
    
    ```jsx
    $foo = True; // gán giá trị TRUE cho $foo
    ?>
    ```
    
- Thông thường, kết quả của một toán tử trả về giá trị bool được truyền vào một cấu trúc điều khiển
    
    ```jsx
    // == là một toán tử kiểm tra
    // sự bằng nhau và trả về một boolean
    if ($action == "show_version") {
        echo "The version is 1.23";
    }
    
    // điều này không cần thiết...
    if ($show_separators == TRUE) {
        echo "<hr>\n";
    }
    
    // ...bởi vì điều này có thể được sử dụng với ý nghĩa chính xác như vậy:
    if ($show_separators) {
        echo "<hr>\n";
    }
    ?>
    ```
    

### **Converting to boolean**

- Để chuyển đổi 1 giá trị sang bool một cách rõ ràng, hãy sử dụng ép kiểu (bool). Thông thường điều này không cần thiết vì khi một giá trị được sử dụng trong ngữ cảnh logic, nó sẽ tự động hiểu là một giá trị thuộc kiểu bool. Để biết thêm thông tin, hãy xem trang Type Jugging
- Khi chuyển sang bool, các giá trị sau được gọi là false
    
    ```jsx
    boolean false
    
    số nguyên 0 (zero)
    
    số thực 0.0 và -0.0 (zero)
    
    chuỗi rỗng "", và chuỗi "0"
    
    mảng có 0 phần tử
    
    kiểu đơn vị NULL (bao gồm các biến chưa được khởi tạo - unset variables)
    
    Các đối tượng nội bộ (Internal objects) overload hành vi ép kiểu của chúng sang bool. Ví dụ: Các đối tượng SimpleXML được tạo từ các phần tử rỗng không có thuộc tính.
    ```
    
- Mọi giá trị khác được coi là true (bao gồm resource và NAN)
    - Lưu ý: `-1` được coi là true, giống như bất kỳ số khác 0 bằng 0 (dù âm hay dương
    
    ```jsx
    var_dump((bool) "");        // bool(false)
    var_dump((bool) "0");       // bool(false)
    var_dump((bool) 1);         // bool(true)
    var_dump((bool) -2);        // bool(true)
    var_dump((bool) "foo");     // bool(true)
    var_dump((bool) 2.3e5);     // bool(true)
    var_dump((bool) array(12)); // bool(true)
    var_dump((bool) array());   // bool(false)
    var_dump((bool) "false");   // bool(true)
    ?>
    ```
    

## Integer

- Một số nguyên (int) là một số thuộc tập ℤ = {..., -2, -1, 0, 1, 2, ...}.

### Syntax

- Số nguyên có thể được chỉ định bằng ký hiệu thập phân (cơ số 10), thập lục phân (cơ số 16), bát phân (cơ số 8) hoặc nhị phân (cơ số 2). Toán tử phủ định có thể được sử dụng để biểu thị số nguyên âm
- Để sử dụng ký hiệu bát phân, hãy thêm số 0 vào trước số. Kể từ PHP 8.1.0, ký hiệu bát phân cũng có thể được thêm vào trước bằng 0o hoặc 0O. Để sử dụng ký hiệu thập lục phân, hãy thêm 0x trước số. Để sử dụng ký hiệu nhị phân, hãy thêm 0b vào trước số
- Kể từ PHP 7.4.0, các số nguyên có thể chứa `_` giữa các số, để dễ đọc hơn. Các dấu gạch dưới này được trình phân tích cú pháp của PHP loại bỏ
    
    ```jsx
    $a = 1234; // số thập phân
    $a = 0123; // số bát phân (tương đương với 83 thập phân)
    $a = 0o123; // số bát phân (kể từ PHP 8.1.0)
    $a = 0x1A; // số thập lục phân (tương đương với 26 thập phân)
    $a = 0b11111111; // số nhị phân (tương đương với 255 thập phân)
    $a = 1_234_567; // số thập phân (kể từ PHP 7.4.0)
    ?>
    ```
    
- Về mặt hình thức, cấu trúc cho các số nguyên kể từ PHP 8.1.0 (trước đó, tiền tố bát phân 0o hoặc 0O không được cho phép và trước PHP 7.4.0, dấu _ không được cho phép)
    
    ```jsx
    decimal     : [1-9][0-9]*(_[0-9]+)*
                | 0
    
    hexadecimal : 0[xX][0-9a-fA-F]+(_[0-9a-fA-F]+)*
    
    octal       : 0[oO]?[0-7]+(_[0-7]+)*
    
    binary      : 0[bB][01]+(_[01]+)*
    
    integer     : decimal
                | hexadecimal
                | octal
                | binary
    ```
    
- Kích thước của một số nguyên phụ thuộc vào nền tảng, mặc dù giá trị tối đa khoảng 2 tỷ là giá trị thông thường (đó là 32 bit có dấu). Các nền tảng 64 bit thường có giá trị tối đa khoảng 9E18. PHP không hỗ trợ số nguyên không dấu. Kích thước số nguyên có thể được xác định bằng cách sử dụng hằng số `PHP_INT_SIZE`, giá trị tối đa bằng cách sử dụng hằng số `PHP_INT_MAX` và giá trị tối thiểu bằng cách sử dụng hằng sô `PHP_INT_MIN`

### **Integer overflow [](https://www.php.net/manual/en/language.types.integer.php#language.types.integer.overflow)(Tràn số nguyên)**

- Nếu PHP gặp một số vượt quá giới hạn kiểu int, nó sẽ được hiểu là một số dấu chấm động (float). Ngoài ra, một số phép toán dẫn đến một số vượt giới hạn của kiểu int sẽ trả về một số dấu chấm động
    
    ```jsx
    $large_number = 50000000000000000000;
    var_dump($large_number);         // float(5.0E+19)
    
    var_dump(PHP_INT_MAX + 1);       // Hệ thống 32-bit: float(2147483648)
                                     // Hệ thống 64-bit: float(9.2233720368548E+18)
    ?>
    ```
    

### **Integer division (Chia số nguyên)**

- Không có toán tử chia số nguyên trong PHP, để đạt được điều này, hãy sử dụng hàm `intdiv()`. 1/2 mang lại số chấm động 0.5. Giá trị có thể được ép kiểu thành số nguyên để làm tròn về 0 hoặc hàm `round()` cung cấp khả năng kiểm soát tốt hơn việc làm tròn
    
    ```jsx
    var_dump(25/7);         // float(3.5714285714286)
    var_dump((int) (25/7)); // int(3)
    var_dump(round(25/7));  // float(4)
    ?>
    ```
    

### **Converting to integer**

- Để chuyển đổi rõ ràng một giá trị thành số nguyên, hãy sử dụng phép ép kiểu (int) hoặc (integer). Tuy nhiên, trong hầu hết các trường hợp, phép ép kiểu là không cần thiết, vì một giá trị sẽ tự động được chuyển đổi nếu một toán tử, hàm hoặc cấu trúc điều khiển yêu cầu một đối số int. Một giá trị cũng có thể được chuyển đổi thành số nguyên bằng hàm `intval()`
- Nếu một tài nguyên được chuyển đổi thành số nguyên, thì kết quả sẽ là số tài nguyên duy nhất được PHP gán cho tài nguyên trong thời gian chạy
- Xem thêm Type Jugging

### From boolean

- false sẽ mang lại 0 và true sẽ mang lại 1

### **From [floating point numbers](https://www.php.net/manual/en/language.types.float.php)**

- Khi chuyển đổi từ float sang int, số sẽ được làm tròn về 0. Kể từ bản 8.1.0, một thông báo phản đối (deprecation notice) được đưa ra khi chuyển đổi ngầm định một float không nguyên thành int làm mất độ chính xác
    
    ```jsx
    
    function foo($value): int {
      return $value; 
    }
    
    var_dump(foo(8.1)); // "Deprecated: Implicit conversion from float 8.1 to int loses precision" kể từ PHP 8.1.0
    var_dump(foo(8.1)); // 8 trước PHP 8.1.0
    var_dump(foo(8.0)); // 8 trong cả hai trường hợp
    
    var_dump((int) 8.1); // 8 trong cả hai trường hợp
    var_dump(intval(8.1)); // 8 trong cả hai trường hợp
    ?>
    ```
    
- Nếu float vượt quá giới hạn của int (thường là +/- 2.15e+9 = 2^31 trên nền tảng 32-bit và +/- 9.22e+18 = 2^63 trên nền tảng 64-bit), kết quả là undefined, vì float không có đủ độ chính xác để đưa ra kết quả int chính xác. Không có cảnh báo, thậm chí còn không có thông báo nào được đưa ra khi điều này xảy ra
- Lưu ý: NaN và -Inf sẽ luôn bằng không khi ép kiểu thành int
- **Warning**: Không bao giờ ép kiểu một phân số chưa biết thành int, vì đôi khi điều này có thể dẫn đến kết quả không mong muốn
    
    ```jsx
    echo (int) ( (0.1+0.7) * 10 ); // in ra 7!
    ?>
    ```
    

### From string

- Nếu string là số hoặc bắt đầu bằng số thì nó sẽ được phân giải thành giá trị số nguyên tương ứng, nêu không nó sẽ chuyển đổi thành 0

### From null

- null luôn được chuyển đổi thành 0

### **From other types**

- Thận trọng: Hành vi chuyển đổi thành int là không xác định đối với các kiểu khác. Không dựa vào bất kỳ hành vi quan sát nào, vì nó có thể thay đổi mà không cần thông báo

## **Floating point numbers**

- Số dấu chấm động còn được gọi là “floats, double, hoặc số thực” có thể được chỉ định bằng bất kỳ cú pháp nào sau đây
    
    ```jsx
    $a = 1.234; 
    $b = 1.2e3; 
    $c = 7E-10;
    $d = 1_234.567; // kể từ PHP 7.4.0
    ?>
    ```
    
- Chính thức từ PHP 7.4.0 (trước đó `_` không được cho phép)
    
    ```jsx
    LNUM          [0-9]+(_[0-9]+)*
    DNUM          ({LNUM}?"."{LNUM}) | ({LNUM}"."{LNUM}?)
    EXPONENT_DNUM (({LNUM} | {DNUM}) [eE][+-]? {LNUM})
    ```
    
- Kích thước của một dấu chấm động phụ thuộc vào nền tảng, mặc dù giá trị tối đa xấp xỉ 1.8e308 với độ chính xác khoảng 14 chữ số thập phân là một giá trị phổ biến (định dạng IEEE 64 bit).

### Warning

- Độ chính xác của dấu chấm động. Float có độ chính xác hạn chế. Mặc dù nó phụ thuộc vào hệ thống, PHP thường sử dụng định dạng độ chính xác kép IEEE 754, định dạng này sẽ cho sai số tương đối đa do làm tròn theo thứ tự 1.11e-16. Các phép toán số học không cơ bản có thể cho sai số lớn hơn và tất nhiên, việc lan truyền sai số phải được xem xét khi một số phép toán được kết hợp
- Ngoài ra các số hữu tỉ có thể biển diễn chính xác dưới dạng số dấu chấm động cơ số 10, như 0.1 hoặc 0.7, không có biểu diễn chính xác dưới dạng số chấm động ở cơ số 2, được sử dụng nội bộ, bất kể kích thước của phần định trị. Do đó, chúng không được chuyển đổi thành các đối tác nhị phân nội bộ của chúng mà không mất chút độ chính xác . Điều này có thể dẫn đến kết quả khó hiểu. Ví dụ floor((0.1 + 0.7) * 10) thường sẽ trả về 7 thay vì 8 như mong đợi, vì biểu diễn nội bộ sẽ giống như 7.9999999999999991118.…
- Vì vậy đừng bao giờ tin tưởng vào kết quả float đến chữ số cuối cùng và không so sánh trực tiếp các số float về độ bằng nhau. Nếu cần độ chính xác cao hơn, các hàm toán học độ chính xác tuỳ ý và các hàm gmp có sẵn

### **Converting to float**

### From string

- Nếu chuỗi là số hoặc bắt đầu bằng số thì nó sẽ được phân giải thành giá trị số float tương ứng, nếu không nó sẽ chuyển đổi thành 0

### **From other types**

- Đối với các giá trị của các kiểu khác, việc chuyển đổi được thực hiện bằng cách chuyển đổi giá trị thành số nguyên trước rồi sau đó thành float.
- Lưu ý: Vì một số kiểu nhất định có hành vi không xác định khi chuyển đổi thành số nguyên, nên đây cũng là trường hợp khi chuyển đổi thành float

### **Comparing floats**

- Như đã lưu ý trong cảnh báo ở trên, việc kiểm tra các giá trị float bằng nhau là có vấn đề, do cách chúng biểu diễn nội bộ. Tuy nhiên, có những cách để thực hiện so sánh các giá trị float giúp giải quyết những hạn chế này
- Để kiểm tra giá trị float về sự bằng nhau, một giới hạn trên của sai số tương đối do làm tròn được sử dụng. Giá trị này được gọi là epsilon máy, hoặc là đơn vị làm tròn, và là chênh lệch chấp nhận được nhỏ nhất trong các phép tính
- $a và $b bằng nhau do độ chính xác 5 chữ số
    
    ```jsx
    $a = 1.23456789;
    $b = 1.23456780;
    $epsilon = 0.00001;
    
    if(abs($a-$b) < $epsilon) {
        echo "true";
    }
    ?>
    ```
    

### NaN

- Một số phép toán số học có thể dẫn đến một giá trị được biểu thị bằng hằng số NaN. Kết quả này đại diện cho một giá trị không xác định hoặc không thể biểu diễn trong các phép tính float. Bất kỳ so sánh lỏng lẻo hoặc nghiêm ngặt nào của giá trị này với bất kỳ giá trị nào khác, bao gồm cả chính nó, nhưng ngoại từ true, sẽ có kết quả là false
- Vì NaN đại diện cho bất kỳ số lượng giá trị khác nhau nào, NaN không nên được so sánh với các giá trị khác, bao gồm cả chính nó và thay vào đó nên được kiểm tra bằng cách sử dụng `is_nan()`

## String

- String là một chuỗi các ký tự, trong đó 1 ký tự giống như 1 byte. Điều này có nghĩa là PHP hỗ trợ bộ nhớ ký tự 256 ký tự và do đó không hỗ trợ cung cấp Unicode gốc.
- Lưu ý trên bản dựng 32-bit, mội chuỗi có thể lớn hơn 2GB (tối đa 2147483647 byte)

### Syntax

- 1 string có thể được định nghĩa theo 4 cách khác nhau
    - Dấu nháy đơn
    - Dấu nháy kép
    - Cú pháp heredoc
    - Cú pháp nowdoc

### **Single quoted**

- Cách đơn giản nhất để chỉ định 1 string là đặt nó trong dấu nháy đơn (’)
- Để chỉ định một dấu ngoặc đơn theo nghĩa đen, hãy thoát nó bằng dấu gạch chéo ngược (\). Để chỉ định một dấu gạch chéo ngược theo nghĩa đen, hãy nhân đôi nó (\\). Tất cả các trường hợp khác của dấu gạch chéo ngược sẽ được coi là dấu gạch chéo ngược theo nghĩa đen: Điều này có nghĩa là các chuỗi thoát khác mà có thể bạn đã quen, chẳng bạn như \r hoặc \n, sẽ được xuất ra theo nghĩa đen như đã chỉ định thay vì có bất kỳ ý nghĩa đặc biệt nào khác
- Lưu ý: không giống như cú pháp dấu nháy kép và heredoc, các biến và chuỗi thoát cho các ký tự đặc biệt sẽ không được mở rộng khi chúng xuất hiện trong chuỗi dấu nháy đơn
    
    ```jsx
    echo 'this is a simple string';
    
    echo 'You can also have embedded newlines in
    strings this way as it is
    okay to do';
    
    // Xuất ra: Arnold once said: "I'll be back"
    echo 'Arnold once said: "I\'ll be back"';
    
    // Xuất ra: You deleted C:\*.*?
    echo 'You deleted C:\\*.*?';
    
    // Xuất ra: You deleted C:\*.*?
    echo 'You deleted C:\*.*?';
    
    // Xuất ra: This will not expand: \n a newline
    echo 'This will not expand: \n a newline';
    
    // Xuất ra: Variables do not $expand $either
    echo 'Variables do not $expand $either';
    ?>
    ```
    

### **Double quoted**

- Nếu chuỗi được đặt trong dấu nháy kép (”), PHP sẽ diễn giải các chuỗi thoát theo các ký tự đặc biệt
    
    ```jsx
    Chuỗi	Ý nghĩa
    \n	Dòng mới (LF hoặc 0x0A (10) trong ASCII)
    \r	Trở về đầu dòng (CR hoặc 0x0D (13) trong ASCII)
    \t	Tab ngang (HT hoặc 0x09 (9) trong ASCII)
    \v	Tab dọc (VT hoặc 0x0B (11) trong ASCII)
    \e	Thoát (ESC hoặc 0x1B (27) trong ASCII)
    \f	Form feed (FF hoặc 0x0C (12) trong ASCII)
    \	Dấu gạch chéo ngược
    $	Dấu đô la
    "	Dấu nháy kép
    [0-7]{1,3}	Bát phân: chuỗi các ký tự khớp với biểu thức chính quy [0-7]{1,3} là một ký tự ở dạng bát phân (ví dụ: "\101" === "A"), sẽ tự động tràn để vừa với một byte (ví dụ: "\400" === "\000")
    \x[0-9A-Fa-f]{1,2}	Thập lục phân: chuỗi các ký tự khớp với biểu thức chính quy [0-9A-Fa-f]{1,2} là một ký tự ở dạng thập lục phân (ví dụ: "\x41" === "A")
    \u{[0-9A-Fa-f]+}	Unicode: chuỗi các ký tự khớp với biểu thức chính quy [0-9A-Fa-f]+ là một điểm mã Unicode, sẽ được xuất ra chuỗi dưới dạng biểu diễn UTF-8 của điểm mã đó. Dấu ngoặc nhọn là bắt buộc trong chuỗi. Ví dụ: "\u{41}" === "A"
    ```
    
- Cũng như trong chuỗi nháy đơn, việc thoát bất kỳ ký tự nào khác sẽ dẫn đến việc dấu gạch chéo ngược cũng được in ra
- Tính năng quan trọng của chuỗi nháy kép là thực tế là biến sẽ được sử dụng. Xem phân tích cú pháp để biết chi tiết
