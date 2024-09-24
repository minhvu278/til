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
