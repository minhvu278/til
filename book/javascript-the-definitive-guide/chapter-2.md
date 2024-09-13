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
## 2.3 Literals

- Literals (Giá trị ký tự) là một giá trị khi dữ liệu xuất hiện trực tiếp trong 1 chương trình. Sau đây là tất cả các `literals`
    
    ```jsx
    12 // Số mười hai
    1.2 // Số một phẩy hai
    "hello world" // Chuỗi văn bản
    'Hi' // Một chuỗi khác
    true // Giá trị Boolean true
    false // Giá trị Boolean false
    null // Không có đối tượng
    ```
    
- Chi tiết về `literals` sẽ được xuất hiện trong chương 3

## 2.4 Identifiers and Reserved Words

- `Identifiers` (định danh) đơn giản chỉ là một cái tên. Trong Js, identifiers được sử dụng để đặt tên cho **constants, variables, property, function, classes** và để cung cấp lable cho các vòng lặp nhất định trong code Js. `identifiers` trong Js phải bắt đầu bằng 1 chữ cái, dấu (_) hoặc dấu ($). Các ký tự tiếp theo có thể là chữ cái, chữ số, dấu gạch dưới hoặc dấu $ (Chữ số không được phép làm ký tự đầu tiên để Js có thể dễ dàng phân biệt `identifiers` với số). Đây là các `identifiers` hợp lệ
    
    ```jsx
    i
    my_variable_name
    v13
    _dummy
    $str
    ```
    
- Giống như bất kỳ ngôn ngữ nào, Js dành riêng một số `identifiers` nhất định để sử dụng bởi chính ngôn ngữ. Những **resered word** (từ khoá dành riêng) này không được sử dụng làm `identifiers` thông thường. Chúng được liệt kê trong các phần tiếp theo

### 2.4.1 Reserved Words

- Các từ khoá sau đây là một phần của Js. Nhiều từ trong số này (chẳng hạn như if, while và for) là **reserved keywords** không được sử dụng làm tên của **constants, variables, functions** hoặc **classes** (mặc dù tất cả chúng đều có thể được sử dụng làm tên của **properties** trong **object**). Những từ khác (chẳng hạn như from, of, get và set) được sử dụng trong các ngữ cảnh hạn chế mà không có sự mơ hồ về cú pháp và hoàn toàn hợp pháp như **identifiers**. Tuy nhiên một số từ khoá khác (chẳng hạn như let) không thể được dành riêng hoàn toàn để duy trì khản năng tương thích ngược với các chương trình cũ hơn và do đó có các quy tắc phức tạp chi phối khi nào chúng có thể sử dụng để làm identifiers và khi nào thì không (ví dụ: let có thể được dùng để khai báo làm tên biến nếu được khai báo bằng var ở ngoài class, nhưng không được nếu khai báo bên trong class hoặc bằng const). Cách đơn giản nhất là tránh sử dụng bất kỳ từ nào trong số hàm này làm `identifiers` ngoài trừ **from, set và target**, chúng an toàn để sử dụng và được sử dụng phổ biến như
    
    ```jsx
    as const export get null target void
    async continue extends if of this while
    await debugger false import return throw with
    break default finally in set true yield
    case delete for instanceof static try
    catch do from let super typeof
    class else function new switch var
    ```
    
- Js cũng dành riêng hoặc hạn chế việc sử dụng một số từ khoá hiện không được sử dụng bởi ngôn ngữ nhưng có thể được sử dụng trong các phiên bản trong tương lai
    
    ```jsx
    enum implements interface package private protected public
    ```
    
- Vì lý do lịch sử nên `arguments` và `eval` không được làm `identifiers` trong một số trường hợp và tốt nhất là nên tránh hoàn toàn

## Unicode

- Các chương trình Js được viết bằng bộ ký tự Unicode, và bạn có thể dùng bất kì ký tự nào trong string, comments. Để dễ di chuyển và chỉnh sửa, thông thường chỉ sử dụng các chữ cái và chữ số ASCII trong identifier. Nhưng đây chỉ là một quy ước lập trình và ngôn ngữ cho phép các chữ cái, chữ số và biểu tượng Unicode (nhưng không phải biểu tượng cảm xúc) trong identifiers. Điều này có nghĩa là các lập trình viên có thể sử dụng các ký hiệu toán học và từ ngữ từ các ngôn ngữ không phải tiếng anh làm constant và variable
    
    ```jsx
    const π = 3.14;
    const sí = true;
    ```
    

### 2.5.1 Unicode Escape Sequences

- Một số phần cứng và phần mềm máy tính không thể hiển thị, nhập hoặc xử lý chính xác toàn bộ ký tự Unicode. Để hỗ trợ các dev và hệ thống sử dụng công nghệ cũ hơn, Js định nghĩa các `escape sequences` (chuỗi thoát) cho phép chúng ta viết ký tự unicode chỉ bằng các ký tự ASCII. Các `escape sequences` Unicode này bắt đầu bằng ký tự `\u` và theo sau là chính xác 4 chữ số thập lục phân ( sử dụng các chữ cái viết hoa hoặc viết thường A-F) hoặc từ 1 - 6 chữ số thập lục phân được bao bọc trong dấu ngoặc nhọn. Các `escape sequences` Unicode này có thể xuất hiện trong literals chuỗi Js, literals regex và identifiers(nhưng không phải trong keyword của ngôn ngữ). Ví dụ `escape sequences` Unicode cho ký tự là “é” là `\u009`; đây là 3 cách khác nhau để viết tên biến bao gồm ký tự này
    
    ```jsx
    let café = 1; // Định nghĩa biến bằng ký tự Unicode
    caf\u00e9 // => 1; truy cập biến bằng escape sequence
    caf\u{E9} // => 1; một dạng khác của cùng một escape sequence
    ```
    
- Các phiên bản js ban đầu chỉ hỗ trợ escape sequences 4 chữ số. Phiên bản có dấu ngoặc nhọn đã được giới thiệu trong ES6 để hỗ trợ tốt hơn các điểm mã Unicode yêu cầu nhiều hơn 16 bit, chẳng hạn như biểu tượng cảm xúc
    
    ```jsx
    console.log("\u{1F600}"); // In ra biểu tượng cảm xúc mặt cười
    ```
    
- **Escape sequences** Unicode cũng có thể xuất hiện trong comments, nhưng vì comments bị bỏ qua chúng chỉ được coi là các ký tự ASCII trong ngữ cảnh đó và không được hiểu là Unicode

### 2.5.2 Unicode Normalization

- Nếu bạn sử dụng các ký tự không phải là ASCII trong chương trình Js của mình, bạn phải lưu ý rằng Unicode cho phép nhiều cách mã hoá cùng 1 ký tự. Ví dụ chuỗi “é” có thể được mã hoá dưới 1 ký tự unicode duy nhất `\u00E9` hoặc dưới dạng ASCII “e” thông thường theo sau là dấu trọng âm kết hợp `\u0301`. Hai cách mã hoá này thường giống hệt nhau khi được hiển thị bởi trình soạn thảo văn bản, nhưng chúng có mã hoá nhị phân khác nhau, có nghĩa là chúng được coi là 2 cách khác nhau bới Js, điều này có thể dẫn đến các chương trình rất khó hiểu
    
    ```jsx
    const café = 1; // Hằng số này được đặt tên là "caf\u{e9}"
    const café = 2; // Hằng số này khác: "cafe\u{301}"
    café // => 1: hằng số này có một giá trị
    café // => 2: hằng số không thể phân biệt này có một giá trị khác
    ```
    
- Tiêu chuẩn Unicode định nghĩa cách mã hoá ưa thích cho tất cả các ký tự và chỉ định một quy trình chuẩn hoá để chuyển đổi văn bản thành dạng chuẩn phù hợp để so sánh. Js giả định rằng code nguồn mà nó đang diễn giải đã được chuẩn hoá và không tự thực hiện bất kỳ chuẩn hoá nào. Nếu bạn dự định sử dụng các ký tự Unicode trong chương trình Js của mình, bạn nên đảm bảo rằng trình soạn thảo của bạn hoặc một số công cụ khác thực hiện chuẩn hoá Unicode code nguồn của bạn để ngăn bạn kết thúc với các identifiers khác nhau nhưng không thể phân biệt được bằng mắt thường

## 2.6 Optional Semicolons

- Giống như nhiều ngôn ngữ lập trình, Js sử dụng dấu (;) để phân tách các `statements` (câu lệnh) (Xem chương 5) với nhau. Điều này rất quan trọng để làm rõ ý nghĩa của code: Nếu không có dấu phân cách, phần cuối của statement sẽ có thể giống như phần đầu của statement tiếp theo hoặc ngược lại. Trong Js bạn thường có thể bỏ qua dấu chấm phẩy giữa 2 statements nếu các statement đó được viết trên các dòng riêng biệt
- Nhiều dev Js (và trong cuốn sách này) sử dụng dấu chấm phẩy để đánh dấu rõ ràng phần cuối của `statements` ngay cả khi chúng không bắt buộc. Một kiểu khác là bỏ qua dấu chấm phẩy bất cứ khi nào có thể, chỉ sử dụng chúng trong 1 số trường hợp yêu cầu. Cho dù bạn chọn kiểu nào, có một số chi tiết bạn nên hiểu về dấu chấm phẩy tuỳ chọn trong Js
- Hãy xem đoạn code sau. Vì 2 `statements` xuất hiện trên các dòng riêng biệt, nên có thể bỏ qua dấu chấm phẩy đầu tiên
    
    ```jsx
    a = 3;
    b = 4;
    ```
    
- Tuy nhiên, viết như sau là bắt buộc
    
    ```jsx
    a = 3; b = 4;
    ```
    
- Lưu ý rằng Js không coi mọi dấu xuống dòng là dấu ; nó chỉ coi xuống dòng là dấu ; nếu nó không thể phân tích cú pháp code mà không cần thêm dấu ; ngầm. Chính thức hơn(và với 3 ngoại lệ được mô tả ở phần sau), Js coi dấu xuống dòng là ; nếu ký tự không phải khoảng trắng tiếp theo sẽ không thể được hiểu là phần tiếp theo của `statement` hiện tại
    
    ```jsx
    let a
    a
    =
    3
    console.log(a)
    ```
    
- Js sẽ hiểu đoạn code này như sau
    
    ```jsx
    let a; a = 3; console.log(a);
    ```
    
- Js coi dấu xuống dòng đầu tiên là dấu ; vì nó không thể phân tích cú pháp `let a a` mà không có dấu ; . `a` thứ 2 có thể đứng 1 mình như statement `a;` , nhưng Js không coi dấu xuống dòng thứ 2 là dấu ; vì nó có thể tiếp tục phân tích cú pháp statement dài hơn `a = 3;`
- Các quy tắc kết thúc `statement` này dẫn đến 1 số trường hợp đáng ngạc nhiên. Đoạn code dưới trông giống như 2 statements riêng biệt được phân tách bởi dấu xuống dòng
    
    ```jsx
    let y = x + f
    (a+b).toString()
    ```
    
- Nhưng dấu ngoặc đơn trên dòng code thứ 2 có thể được hiểu là 1 lời gọi hàm `f` từ dòng đầu tiên và Js hiểu code như sau
    
    ```jsx
    let y = x + f(a+b).toString();
    ```
    
- Nhiều khả năng đây không phải là cách hiểu mà tác giả code dự định. Để hoạt động như 2 `statements` riêng biệt, trong trường hợp này, cần có dấu ; rõ ràng
- Nói chung, nếu một statement bắt đầu bằng `(,[,/,+ hoặc -` đều có khả năng bị hiểu lầm là phần tiếp theo của statement trước đó. Statements bắt đầu bằng `/`, + - khá hiếm gặp trong thực tế nhưng statement bắt đầu bằng ( và [ không hề hiếm, ít nhất là trong 1 số kiểu lập trình Js. Một số dev thích đặt dấu chấm phẩy phòng thủ ở đầu bất kỳ statement nào như vậy để nó sẽ tiếp tục hoạt động chính xác ngay cả khi statement trước đó được sửa đổi và dấu ; kết thúc trước đó bị xoá
    
    ```jsx
    let x = 0 // Dấu chấm phẩy bị bỏ qua ở đây
    ;[x,x+1,x+2].forEach(console.log) // Dấu chấm phẩy phòng thủ ; giữ cho statement này tách biệt
    ```
    
- Có 3 ngoại lệ đối với Js chung là Js hiểu dấu xuống dòng là dấu ; khi nó không thể phân tích cú pháp dòng thứ 2 như phần tiếp theo của statement trên dòng đầu tiên. Ngoại lệ đầu tiên liên quan đến `statement` **return, throw, yield, break, continue**(xem chương 5). Các statement này thường được đứng 1 mình, nhưng đôi khi chúng được theo sau bởi một `identifier` hoặc `expression` . Nếu dấu xuống dòng xuất hiện sau bất kỳ ký tự từ nào trong số này (trước bất ký token nào khác), Js sẽ luôn hiểu dấu xuống dòng đó là dấu ;
    
    ```jsx
    return
    true;
    ```
    
- Js sẽ giả định ý của bạn là
    
    ```jsx
    return; true;
    ```
    
- Tuy nhiên ý của bạn là
    
    ```jsx
    return true;
    ```
    
- Điều này có nghĩa là bạn không được chèn dấu xuống dòng giữa `return và break hoặc continue và expression sau từ khoá`. nếu bạn chèn dấu xuống dòng, code của bạn sẽ gặp lỗi không rõ ràng và khó gỡ lỗi
- Ngoại lệ thứ 2 liên quan đến toán từ ++ và —. Những toán tử này có thể là toán tử tiền tố, xuất hiện trước expression hoặc toán tử hậu tố xuất hiện sau expression. Nếu bạn muốn sử dụng 2 toán tử này làm toán tử hậu tố, chúng phải xuất hiện trên cùng một dòng với expression mà chúng áp dụng. Ngoại lệ thứ 3 liên quan đến các functions được định nghĩa bằng cú pháp arrow functions: Bản thân `=>` phải xuất hiện trên cùng một dòng với danh sách tham số
