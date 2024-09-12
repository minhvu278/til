# Lexical Structure
- Lexical Structure (cấu trúc từ vựng) của 1 ngôn ngữ lập trình là tập hợp các quy tắc cơ bản quy định cách bạn viết chương trình trong ngôn ngữ đó. Nó là cú pháp ở cấp độ thấp nhất của 1 ngôn ngữ: nó chỉ định tên biến trong như thế nào, các ký tự phân cách cho `comments`, và một câu lệnh chương trình được phân tách với câu lệnh tiếp theo chẳng hạn
- Chương ngắn này ghi lại cấu trúc từ vựng của Js. Nó bao gồm
    - Phân biệt hoa thường, khoảng trắng và dấu xuống dòng
    - Comments
    - Literals (giá trị ký tự)
    - Identifiers (định danh) và reserved words (từ khoá dành riêng)
    - Unicode
    - Dấu chấm phẩy tuỳ chọn

## 2.1 The Text of a JavaScript Program
- Js là một ngôn ngữ phân biệt hoa thường. Điều này có nghĩa là các `keywords` của ngôn ngữ, `variables` , `function names` và `identifiers` khác phải luôn được nhập với viết hoa các chữ cái nhất quán
- Js bỏ qua các `khoảng trắng` xuất hiện giữa các `tokens` (mã thông báo) trong chương trình. Phần lớn, Js cũng bỏ qua các `dấu xuống dòng` (nhưng vẫn có ngoại lệ). Bởi vì bạn có thể sử dụng khoảng trắng và dấu xuống dòng một cách tự do trong chương trình của mình, bạn có thể định dạng và thụt lề chương trình của mình một cách gọn gàng và nhất quán, giúp code dễ đọc và dễ hiểu
- Ngoài ký tự khoảng trắng thông thường (\u0020), Js cũng nhận dạng các tab, các ký tự điều khiển ASCII khác nhau và các ký tự khoảng trắng Unicode khác nhau dưới dạng khoảng trắng. Js nhận dạng dấu xuống dòng, ký tự trả về đầu dòng và chuỗi ký tự trả về đầu dòng/ dấu xuống dòng như ký tự kết thúc dòng

## 2.2 Comments
- Js hỗ trợ 2 kiểu `comments`. Bất kỳ văn bản nào nằm giữa `//` đều được gọi là `comment` và Js sẽ bỏ qua. Bất kỳ văn bản nào nằm giữa ký tự `/*` và `*/` cũng được coi là comment. Những comment này có thể kéo dài nhiều dòng nhưng không được lồng nhau.
    
    ```jsx
    // Đây là comment một dòng.
    /* Đây cũng là một comment */ // và đây là một comment khác.
    /*
    * Đây là comment nhiều dòng. Các ký tự * bổ sung ở đầu
    * mỗi dòng không phải là một phần bắt buộc của cú pháp; chúng chỉ
    * để code trông "ngầu" hơn thôi!
    */
    ```
