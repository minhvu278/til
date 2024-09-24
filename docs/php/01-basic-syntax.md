# Basic syntax
## PHP tags

- Khi PHP phân tích một file, nó sẽ tìm kiếm các thẻ mở và đóng, đó là `<?php và ?>`, chúng cho PHP biết bắt đầu và dừng việc thông dịch code giữa chúng. Việc phân tích cú pháp theo cách này cho phép PHP được nhúng vào tất cả các document khác nhau, vì mọi thứ bên ngoài cặp thẻ mở và đong sẽ bị trình phân tích cú pháp PHP bỏ qua
- PHP bao gồm `echo`  ngắn `<?=`, đây là một cách viết tắt của `<?php echo` dài dòng hơn
    
    ```jsx
    <?php echo 'nếu bạn muốn phục vụ mã PHP trong tài liệu XHTML hoặc XML, hãy sử dụng các thẻ này'; ?>
    Bạn có thể sử dụng thẻ echo ngắn để <?= 'in chuỗi này' ?>.
    Nó tương đương với <?php echo 'in chuỗi này' ?>.
    <? echo 'mã này nằm trong các thẻ ngắn, nhưng sẽ chỉ hoạt động '. 'nếu short_open_tag được bật'; ?>
    ```
    
- Các thẻ ngắn được bật theo mặc định nhưng có thể bị tắt thông qua chỉ thị file cấu hình `php.ini` là `short_open_tag`, hoặc bị tắt theo mặc định nếu PHP được xây dựng với cấu hình `--disable-short-tags`
- Lưu ý: Vì các thẻ ngắn có thể bị tắt, nên chỉ sử dụng các thẻ thông thường (`<?php. ?>` và `<?=  ?>` )
- Nếu một file chỉ chứa code PHP, tốt nhất là bỏ qua thẻ đóng PHP ở cuối tệp. Điều này ngăn chặn khoảng trắng hoặc dòng mới vô tình được thêm vào sau thẻ đóng PHP, điều này có thể gây ra những hiệu ứng không mong muốn vì PHP sẽ bắt đầu đệm đầu ra khi lập trình viên không có ý định gửi bất kỳ đầu ra nào tại thời điểm đó trong file code
    
    ```jsx
    <?php
    echo "Hello world";
    
    // ... more code
    
    echo "Last statement";
    
    // the script ends here with no PHP closing tag
    ```
    

## **Escaping from HTML**

- Mọi thứ bên ngoài cặp thẻ mở và đóng sẽ bị trình phân tích cú pháp PHP bỏ qua, điều này cho phép các tệp PHP co nội dung hỗn hợp. Điều này cho phép PHP được nhúng vào các tài liệu HTML. Ví dụ để tạo các template
    
    ```jsx
    <p>This is going to be ignored by PHP and displayed by the browser.</p>
    <?php echo 'While this is going to be parsed.'; ?>
    <p>This will also be ignored by PHP and displayed by the browser.</p>
    ```
    
- Điều này hoạt động như mong đợi, bởi vì khi trình thông dịch PHP gặp thẻ đóng `?>`, nó chỉ đơn giản là bắt đầu xuất ra bất cứ thứ gì nó tìm thấy (ngoại trừ dòng mới ngay sau đó - xem phần tách lệnh) cho đến khi nó gặp thẻ mở khác trừ khi ở giữa một câu lệnh điều kiện, trong trường hợp đó trình thông dịch sẽ xác định kết quả của điều kiện trước khi đưa ra quyết định bỏ qua cái gì.
- Sử dụng cấu trúc với điều kiện
    
    ```jsx
    <?php if ($expression == true): ?>
      This will show if the expression is true.
    <?php else: ?>
      Otherwise this will show.
    <?php endif; ?>
    ```
    
- Trong ví dụ này, PHP sẽ bỏ qua các block mà điều kiện không được đáp ứng, ngay cả khi chung nằm ngoài các thẻ mở đóng PHP; PHP bỏ qua chúng theo điều kiện vì trình thông dịch PHP sẽ nhảy qua các khối chứa trong một điều kiện không được đáp ứng
- Đề xuất ra các block text lớn, việc thoát khỏi chế độ phân tích cú pháp PHP thường hiệu quả hơn so với việc gửi tất cả văn bản thông qua echo hoặc print
- Lưu ý: Nếu PH được nhúng trong XML hoặc XHTML, thì phải sử dụng PHP thông thường <?php ?> để duy trì tuân thủ các tiêu chuẩn
