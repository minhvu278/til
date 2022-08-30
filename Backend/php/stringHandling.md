# 1 số nguyên tắc khi xử lý chuỗi 
- Nếu sử dụng `""` để in ra chuỗi kèm với biến thì không cần phải nối chuỗi 
    ```php 
    $name = "Vu Do";
    echo "Ten cua anh dai la $name"
    ```
- Nếu sử dụng `""` để in ra chuỗi mà trong chuỗi có dấu `"` thì ta phải thêm `\` vào trước 
    ```php 
    echo "Ten cua anh dai la \" Vu Do \"";
    ```
    - Tương tự với `'`

## Các hàm xử lý chuỗi thông dụng 
- **addcslashes($str, $char_list)**
    - Có tác dụng chèn `\` vào trước các kí tự chuỗi trong `$str` với các kí tự được liệt kê ở `$char_list`
    - `Lưu ý:` Có phân biệt hoa thường
    ```php 
    echo addcslashes("dominhvu", 'v');
    // dominh\vu
    ```

- **addslashes($str)**
    - Thêm kí tự `\` vào trước các kí tự `', ", \` nếu có 
    ```php 
    echo addslashes("do'minh'vu")
    // do\'minh\'vu
    ```
- **bind2hex($str)**
    - Hàm này dùng để chuyển đổi chuỗi về dạng ASCII HEX của từng kí tự trong chỗi $str 
    ```php
    echo bind2hex("dominhvu")
    // 646f6d696e687675
    ```
- **chop($string, $charList)**
    - Có tác dụng xóa ký tự, hoặc từ cuối cùng của chuỗi nếu nó = $charlist
    ```php
    echo chop("Do Minh Vu", "Vu");
    // Do Minh
    ```

- **crc32($string)**
    - Hàm này dùng để chuyển 1 chuỗi thành 1 số nguyên
    ```php
    echo crc32("Do Minh Vu");
    // 671319781
    ```
- **explode($separator, $string, $limit)**
    - Có tác dụng tách chuỗi `$string` thành nhiều chuỗi khác nhau với điều kiện `$separator` và giới hạn `$limit`
    