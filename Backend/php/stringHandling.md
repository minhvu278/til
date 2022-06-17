# 1 số nguyên tắc khi xử lý chuỗi 
- Nếu chuỗi được đặt trong dấu nháy kép `""` thì các kí tự  `"` bên trong chuỗi phải thêm `\` đằng trước  
    ```
    echo "Nam nói\"Cậu ấy đang ăn tối\" ";
    ```

- Nếu chuỗi nằm trong dấu nháy kép thì trong chuỗi ta có thể truyền biến vào mà không cần dùng đến phép nối chuỗi 
    ```php
    $str = "đang ăn tối";
    echo "Nam nói\"Cậu ấy $str\" "; 
    ```

- Nếu chuỗi được đặt trong dấu nháy đơn `''` thì các kí tự trong dấu `'` bên trong chuỗi phải thêm dấu gạch chéo đằng trước nó.
    ```
    echo 'Freetuts's a website learning online';
    ```
    