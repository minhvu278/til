# Statements
- Chương 4 đã mô tả các biểu thức (expressions) như là các cụm từ trong Js. Theo cách so sánh đó, các câu lệnh (statements) là các câu hoặc lệnh trong Js. Cũng giống như các câu tiếng Anh được kết thúc và phân tách bằng dấu chấm, các câu lệnh Js được kết thúc bằng dấu chấm phẩy (2.6)
- Các biểu thức được ước lượng để tạo ra một giá trị, nhưng các câu lệnh được `thực thi` để làm điều gì đó xảy ra
- Một cách để “làm cho điều gì đó xảy ra” là ước lượng một biểu thức có tác dụng phụ (side effects). Các biểu thức có tác dụng phụ, chẳng hạn như phép gán (assignments) và gọi hàm (function invocations), có thể đứng riêng lẻ như một câu lệnh và khi được sử dụng theo cách này được gọi là câu lệnh biểu thức (expression statements). Một loại câu lệnh tương tự là câu lệnh khai báo (declaration statements) dùng để khai báo các biến mới và định nghĩa các hàm mới
- Các chương trình Js không gì khác hơn là một chuỗi các câu lệnh để thực thi. Theo mặc định, trình thông dịch Js thực thi các câu lệnh này lần lượt theo thứ tự chúng được viết. Một các khác để “làm cho điều gì đó xảy ra” là thay đổi thứ tự thực thi mặc định này và Js có một số câu lệnh hoặc cấu trúc điều khiển để làm điề này
    - `Conditionals`: Các câu lệnh như if và switch làm cho trình thông dịch Js thực thi hoặc bỏ qua các câu lệnh khác tuỳ thuộc vào giá trị của một biểu thức
    - `Loops`: Các câu lệnh nhw `while` và `for` thực thi các câu lệnh khác lặp đi lặp lại
    - `Jumps`: Các câu lệnh như break, return và throw khiến trình thông dịch nhảy đến phần khác của chương trình
- Các phần sau đây mô tả các câu lệnh khác nhau trong Js và giải thích cú pháp của chúng. Bảng 5-1 ở cuối chương, tóm tắt cú pháp. Một chương trình Js đơn giản là một chuỗi các câu lệnh, được phân tách bằng dấu chấm phẩy, vì vậy, sau khi bạn đã quen thuộc với các câu lệnh của Js, bạn có thể bắt đầu viết các chương trình Js

## 5.1 **Expression Statements**

- Các loại câu lệnh đơn giản nhất trong Js là các biểu thức có tác dụng phụ. Loại câu lệnh này đã được trình bày trong chương 4
- Câu lệnh gán là một loại chính của câu lệnh biểu thức
    
    ```jsx
    greeting = "Hello " + name;
    i *= 3;
    ```
    
- Các toán tử tăng và giảm, `++` và `--`, có liên quan đến câu lệnh gán. Chúng có tác dụng phụ là thay đổi giá trị của biến, giống như thể một phép gán đã được thực hiện
    
    ```jsx
    counter++;
    ```
    
- Toán tử `delete` có tác dụng phụ quan trọng là xoá một object property. Do đó, nó hầu như luôn được sử dụng như một câu lệnh, thay vì là một phần của một biểu thức lớn hơn
    
    ```jsx
    delete o.x;
    ```
    
- Gọi hàm là một loại chính xác của câu lệnh biểu thức
    
    ```jsx
    console.log(debugMessage);
    displaySpinner(); // Một hàm giả định để hiển thị spinner trong ứng dụng web.
    ```
    
- Các câu lệnh gọi hàm này là các biểu thức, nhưng chúng có tác dụng phụ ảnh hưởng đến môi trường chủ (host environment) hoặc trạng thái chương trình và chúng được sử dụng ở đây như các câu lệnh. Nếu một hàm không có bất kỳ tác dụng phụ nào, thì việc gọi nó là vô nghĩa, trừ khi nó là một phần của một biểu thức lớn hơn hoặc một câu lệnh gán. Ví dụ, bạn sẽ không chỉ tính toán cosine và loại bỏ kết quả
    
    ```jsx
    Math.cos(x);
    ```
    
- Nhưng bạn cũng có thể tính toán giá trị và gán nó cho một biến để sử dụng sau
    
    ```jsx
    cx = Math.cos(x);
    ```
