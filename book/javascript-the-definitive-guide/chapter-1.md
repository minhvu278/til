# Chapter 1. Introduction to JavaScript
- Js là ngôn ngữ lập trình “thống trị” thế giới web. Hầu hết các website đều sử dụng Js và tất cả các browser hiện đại - trên PC, tablet, mobile - đều tích hợp sẵn Javascript interperters (trình thông dịch Js), biến Js trở thành ngôn ngữ lập trình được triển khai rộng rãi nhất trong lịch sử
- Trong thập kỷ qua, Node.js đã cho phép lập trình Js “thoát khỏi” trình duyệt web và sự thành công vang dội của Node đồng nghĩa với việc Js giờ đây cũng là ngôn ngữ lập trình được sử dụng nhiều nhất trong giới lập trình viên. Cho dù bạn là “lính mới” hay đã là “cao thủ” Js, cuốn sách này sẽ giúp bạn “nâng tầm” kỹ năng của mình
- Nếu bạn đã quen thuộc với các ngôn ngữ lập trình khác, bạn có thể thấy Js là một ngôn ngữ lập trình `high-level` (cấp cao), `dynamic` (động), `interpreted` (thông dịch) phù hợp với cả phong cách lập trình `object-oriented` (hướng đối tượng) và `functional` (hàm). Các biến trong Js là `untyped` (không kiểu). Cú pháp của nó dựa trên Java nhưng nhìn chung là không liên quan. Js kế thừa các `first-class functions` (hàm hạng nhất) từ Scheme và `prototype-based inheritance` (kế thừa dựa trên prototype) từ ngôn ngữ ít được biết đến là Self. Nhưng bạn không cần phải biết bất kỳ ngôn ngữ nào trong số đó, hoặc quen thuộc với các thuật ngữ này, để sử dụng cuốn sách này và học Js
- Cái tên “Javascritpt” có vẻ “sai sai”. Ngoại trừ sự giống nhau về mặt cú pháp, Js hoàn toàn khác với Java. Và Js đã vượt xa nguồn gô là 1 `scripting-language` (ngôn ngữ kịch bản) để trở thành một ngôn ngữ `general-purpose` (đa năng) mạnh mẽ và hiệu quả, phù hợp cho các dự án kỹ thuật mềm “khủng” với `codebases` (cơ sở mã) đồ sộ
    
    ### JAVASCRIPT: NAMES, VERSIONS, AND MODES
    
    - Js được tạo ra bởi Netscape vào những ngày đầu của web, và về mặt kỹ thuật, “Js” là nhãn hiệu được cấp phép từ Sun Microsystems (nay là Oracle) được sử dụng để mô tả việc triển khai ngôn ngữ của Netscape (nay là Mozilla). Netscape đã gửi ngôn ngữ này để chuẩn hoá cho ECMA - hiệp hội các nhà sản xuất máy tính châu Âu - và do các vấn đề về nhãn hiệu, phiên bản chuẩn hoá của ngôn ngữ này đã bị “mắc kẹt” với cái tên “ECMAScript” nghe có vẻ ‘kỳ cục”. Trên thực tế, mọi người vẫn gọi ngôn ngữ này là Js. Cuốn sách này sử dụng tên “ECMAScript” và viết tắt “ES” để chỉ tiêu chuẩn ngôn ngữ và các phiên bản tiêu chuẩn đó
    - Trong phần lớn những năm 2010, phiên bản 5 của tiêu chuẩn ECMAScript (ES5) đã được tất cả các trình duyệt web hỗ trợ. Cuốn sách này coi ES5 là nên tảng tương thích và không còn thảo luận về các phiên bản trước đó của ngôn ngữ. ES6 được phát hành vào năm 2015 và đã bổ sung tính năng mới quan trọng - bao gồm cú pháp `class` và `module` - đã thay đổi Js từ 1 ngôn ngữ kịch bản thành 1 ngôn ngữ đa năng nghiêm túc, phù hợp kỹ thuật phần mềm quy mô lớn. Kể từ ES6, ECMAScript đã chuyển sang chu kỳ phát hành hằng năm và các phiên bản của ngôn ngữ - ES2016, ES2018, ES2019 và ES2020 - giờ đây đã được xác định theo năm phát hành
    - Khi Js phát triển, các nhà thiết kế ngôn ngữ đã từng cô gắng sửa chữa những sai sót trong các phiên bản đầu (trước ES5). Để duy trì khả năng tương thích ngược, không thể xoá các tính năng cũ, dù chúng có lỗi đến đâu. Nhưng trong ES5 trở lên, các chương trình có thể chọn tham gia `stric mode` (chế độ nghiêm ngặt) của Js, trong đó một số lỗi ngôn ngữ ban đầu đã được sửa chữa. Cơ chế để chọn tham gia là chỉ thị `use strict` được mô tả trong $5.6.3. Phần đó cũng tóm tắt các sự khác biệt giữa Js cũ và Js strict. Trong ES6 trở lên, việc sử dụng các tính năng ngôn ngữ mới thường được ngầm định gọi chế độ nghiêm ngặt. Ví dụ: nếu bạn sử dụng từ khoá class của ES6 hoặc tạo module ES6, thì tất cả các mã trong class hoặc module sẽ tự động ở strict mode và các tính năng cũ, bị lỗi sẽ không khả dụng trong các ngữ cảnh đó. Cuốn sách này sẽ đề cập đến các tính năng cũ của Js nhưng lưu ý rằng chúng sẽ không khả dụng trong strict mode
- Để hữu ích, mọi ngôn ngữ phải có `platform` (nền tảng) hoặc `standard library` (thư viện chuẩn) để thực hiện những việc như `input` (nhập) và `output` (xuất) cơ bản. Ngôn ngữ Js cốt lõi định nghĩa API tối thiểu để làm việc với number, text, arrays, sets, maps,… nhưng không bao gồm bất kỳ chức năng input output nào. Input và output (cũng như các tính năng phức tạp hơn, chẳng hạn như networking, storage and graphics) là trách nhiệm của “host enviroment” (môi trường lưu trữ) mà Js được nhúng vào
- `Host environment` ban đầu của Js là trình duyệt web và đây vẫn là môi trường thực thi phổ biến nhất cho mã Js. Môi trường trình duyệt web cho phép mã Js lấy input từ chuột và bàn phím của người dùng và bằng cách thực hiện các `HTTP` request. Và nó cho phép mã Js hiển thị `output` cho người dùng bằng HTML và CSS
- Kể từ năm 2010, một `host enviroment` khác đã co sẵn cho mã Js. Thay vì hạn chế Js làm việc với các API do trình duyệt web cung cấp, `Node` cung cấp cho Js quyền truy cập vào toàn bộ hệ điều hành, cho phép các chương trình Js đọc và ghi file, gửi và xác nhận dữ liệu qua network và thực hiện và phục vụ các HTTP request. Node là một lựa chọn phổ biến để triể khai máy chủ web và cũng là một công cụ thuận tiện để viết các `utility scripts` (tập lệnh tiện ích) đơn giản như 1 giải pháp thay thế cho `shell scripts`
- Phần lớn cuốn sách này tập chung vào bản thân ngôn ngữ Js. Chương 11 ghi lại `standard library` của Js, chương 15 giới thiệu `host enviroment` của trình duyệt web và chương 16 giới thiệu `host enviroment` của Node
- Cuốn sách này bao gồm các nguyên tắc cơ bản ở cấp độ thấp trước, sau đó xây dựng dựa trên những nguyên tắc đó đến các khái niệm trừu tượng cấp cao hơn và nâng cao hơn. Các chương được dự định để đọc theo thứ tự. Nhưng việc học 1 ngôn ngữ lập trình mới không bao giờ là một quá trình tuyến tính và việc mô tả một ngôn ngữ cũng không phải là tuyến tính: Mỗi tính năng ngôn ngữ đều liên quan đến các tính năng khác, và cuốn sách này chứa đầy các tham chiếu chéo - đôi khi là lùi và đôi khi là tiến - đến nội dung liên quan. Chương giới thiệu này sẽ lướt qua ngôn ngữ 1 cách nhanh chóng, giới thiệu các tính năng chính giúp bạn dễ hiểu hơn về cách xử lý chuyên sâu trong các chương tiếp theo. Nếu bạn đã là 1 lập trình viên Js đang hành nghề, bạn có thể bỏ qua chương này. (Mặc dù bạn có thể thích đọc, ví dụ 1-1 ở cuối chương trước khi tiếp tục.)
## 1.1 Exploring JavaScript

- Khi học 1 ngôn ngữ lập trình mới, điều quan trọng là phải thử nghiệm các ví dụ trong sách, sau đó sửa chúng và thử lại xem bạn đã “ngấm” ngôn ngữ đến đâu. Để làm được điều đó, bạn cần 1 `Javascript interperter` (trình thông dịch Js)
- Cách dễ nhất để “nghịch” vài dòng code Js là mở devtool lên trong trình duyệt của bạn bằng cách nhấn F12 và chọn tab console. Sau đó bạn có thể gõ code và xem kết quả ngay lập tức.
- Một cách khác để “chơi thử” Js là tải xuống Node từ [https://nodejs.org](https://nodejs.org/). Sau khi node được cài đặt trên hệ thống của bạn, bạn chỉ cần mở cửa sổ và gõ node để bắt đầu 1 phiên `interactive` Js (tương tác Js) như sau
    
    ```jsx
    $ node
    Welcome to Node.js v12.13.0.
    Type ".help" for more information.
    > .help
    .break Sometimes you get stuck, this gets you out
    .clear Alias for .break
    .editor Enter editor mode
    .exit Exit the repl
    .help Print this help message
    .load Load JS from a file into the REPL session
    .save Save all evaluated commands in this REPL session to
    a file
    Press ^C to abort current expression, ^D to exit the repl
    > let x = 2, y = 3;
    undefined
    > x + y
    5
    > (x === 2) && (y === 3)
    true
    > (x > 3) || (y < 3)
    false
    ```
    

## **1.2 Hello World**

- Khi bạn đã sẵn sàng thử nghiệm với các đoạn code dài hơn, môi trường tương tác từng dòng có lẽ không phù hợp và bạn có thể thích viết code trong text editor hơn. Từ đó bạn có thể copy và paste vào console của Js hoặc vào 1 phiên Node. Hoặc bạn có thể lưu code của mình vào 1 file và sau đó chạy file đó bằng node
    
    ```jsx
    node snippet.js
    ```
    
- Nếu bạn sử dụng Node theo cách `non-interactive` (không tương tác) như thế này, nó sẽ không tự động in ra giá trị của tất cả các code bạn chạy, vì vậy bạn sẽ phải tự làm điều đó. Bạn có thể sử dụng hàm `console.log()` để hiển thị text và các giá trị Js khác trong terminal hoặc console của chrome

## 1.3 A Tour of JavaScript

- Phần này giới thiệu nhanh ngôn ngữ JS thông qua các ví dụ code. Sau chương mở đầu này, chúng ta sẽ “nhảy” vào Js ở cấp độ “siêu cơ bản”: Chương 2 giải thích những thứ như comments, dấu chấm phẩy và bộ ký tự Unicode. Chương 3 bắt đầu thú vị hơn: Nó giải thích variables của Js và các values bạn co thể gán cho variable đó
- Dưới đây là 1 số code mẫu để minh hoạ những điểm nổi bật của 2 chương đó
    
    ```jsx
    // Bất cứ thứ gì sau dấu gạch chéo kép là comment (ghi chú) bằng tiếng Anh.
    // Đọc kỹ comments: chúng giải thích code JavaScript.
    // Variable là tên tượng trưng cho một value.
    // Variables được khai báo bằng từ khóa let:
    let x; // Khai báo một variable tên là x.
    // Values có thể được gán cho variables bằng dấu =
    x = 0; // Bây giờ variable x có value là 0
    x // => 0: Một variable được đánh giá bằng value của nó.
    // JavaScript hỗ trợ một số loại values
    x = 1; // Numbers (số).
    x = 0.01; // Numbers có thể là số nguyên hoặc số thực.
    x = "hello world"; // Strings (chuỗi) văn bản trong dấu ngoặc kép.
    x = 'JavaScript'; // Dấu ngoặc đơn cũng phân định strings.
    x = true; // Boolean value (giá trị đúng/sai).
    x = false; // Boolean value còn lại.
    x = null; // Null là một special value (giá trị đặc biệt) có nghĩa là "không có value."
    x = undefined; // Undefined là một special value khác giống như null.
    ```
    
- Hai loại rất quan trọng khác mà các chương trình Js có thể thao tác là objects và arrays. Đây là chủ đề của chương 6 và 7, nhưng chúng rất quan trọng nên bạn sẽ thấy chúng nhiều lần trước khi đến các chương đó
    
    ```jsx
    // Kiểu dữ liệu quan trọng nhất của JavaScript là object.
    // Object là tập hợp các cặp name/value (tên/giá trị), hoặc ánh xạ từ string tới value.
    let book = { // Objects được bao bọc trong dấu ngoặc nhọn.
    topic: "JavaScript", // Property (thuộc tính) "topic" có value là "JavaScript."
    edition: 7 // Property "edition" có value là 7
    }; // Dấu ngoặc nhọn đánh dấu kết thúc của object.
    // Truy cập properties của object bằng . hoặc []:
    book.topic // => "JavaScript"
    book["edition"] // => 7: một cách khác để truy cập values của property.
    book.author = "Flanagan"; // Tạo properties mới bằng phép gán.
    book.contents = {}; // {} là một empty object (đối tượng trống) không có properties.
    // Truy cập properties có điều kiện bằng ?. (ES2020):
    book.contents?.ch01?.sect1 // => undefined: book.contents không có property ch01.
    // JavaScript cũng hỗ trợ arrays (danh sách được đánh số) của values:
    let primes = [2, 3, 5, 7]; // Mảng 4 values, được phân định bằng [ và ].
    primes[0] // => 2: element (phần tử) đầu tiên (index 0) của mảng.
    primes.length // => 4: số lượng elements trong mảng.
    primes[primes.length-1] // => 7: element cuối cùng của mảng.
    primes[4] = 9; // Thêm một element mới bằng phép gán.
    primes[4] = 11; // Hoặc thay đổi một element hiện có bằng phép gán.
    let empty = []; // [] là một empty array không có elements.
    empty.length // => 0
    // Arrays và objects có thể chứa các arrays và objects khác:
    let points = [ // Mảng có 2 elements.
    {x: 0, y: 0}, // Mỗi element là một object.
    {x: 1, y: 1}
    ];
    let data = { // Object có 2 properties
    trial1: [[1,2], [3,4]], // Value của mỗi property là một mảng.
    trial2: [[2,3], [4,5]] // Các elements của mảng là các mảng.
    };
    ```
    
    ### COMMENT SYNTAX IN CODE EXAMPLES
    
    - Bạn có thể nhận thấy trong code trước đó rằng 1 số comments bắt đầu bằng mũi tên (⇒). Những cái này hiển thị `value` được tạo ra bởi code trước comment và là nỗ lực của tôi để mô phỏng môi trường Js tương tác như console của trình duyệt web trong một cuốn sách in
    - Những comment `// =>` đó cũng đóng vai trì như 1 `assertion` (khẳng định), và tôi đã viết 1 công cụ để kiểm tra code và xác minh rằng nó tạo ra value được chỉ định trong comment. Tôi hy vọng điều này sẽ giúp tôi giảm lỗi trong sách
    - Có 2 kiểu `comment/assertion` liên quan. Nếu bạn thấy một comment ở dạng `// a = 42` , co nghĩa là sau khi code trước comment chạy, biến a sẽ có value là 42. Nếu bạn thấy 1 comment ở dạng `// !` , có nghĩa là code trên dòng trước comment sẽ ném ra 1 exception (và phần còn lại của comment sau dấu chấm than thường giải thích loại exception nào được ném ra)
    - Bạn sẽ thấy những comment này được sử dụng trong cuốn sách
- Cú pháp được minh hoạ ở đây để liệt kê các `elements` của mảng trong dấu ngoặc vuông hoặc ánh xạ `property name` (tên thuộc tính) của `object` với `property value` bên trong dấu ngoặc nhọn được gọi là `initializer expression` (biểu thức khởi tạo) và nó chỉ là một trong những chủ đề của chương 4. `Expression` (biểu thức) là một cụm từ Js có thể được đánh giá để tạo ra 1 `value` . Ví dụ việc sử dụng dấu . hoặc dấu [] để tham chiếu đến value của property của object hoặc element của mảng là một expresion
- Một trong những cách phổ biến nhất để tạo expressions trong Js là sử dụng operators
    
    ```jsx
    // Toán tử tác động lên values (toán hạng) để tạo ra value mới.
    // Toán tử số học là một số toán tử đơn giản nhất:
    3 + 2 // => 5: cộng
    3 - 2 // => 1: trừ
    3 * 2 // => 6: nhân
    3 / 2 // => 1.5: chia
    points[1].x - points[0].x // => 1: toán hạng phức tạp hơn cũng hoạt động
    "3" + "2" // => "32": + cộng số, nối chuỗi
    // JavaScript định nghĩa một số toán tử số học viết tắt
    let count = 0; // Định nghĩa một biến
    count++; // Tăng biến
    count--; // Giảm biến
    count += 2; // Cộng 2: giống như count = count + 2;
    count *= 3; // Nhân với 3: giống như count = count * 3;
    count // => 6: tên biến cũng là expressions.
    // Toán tử so sánh kiểm tra xem hai values có bằng nhau,
    // không bằng nhau, nhỏ hơn, lớn hơn, v.v. Chúng đánh giá thành true hoặc false.
    let x = 2, y = 3; // Dấu = này là phép gán, không phải kiểm tra bằng nhau
    x === y // => false: bằng nhau
    x !== y // => true: không bằng nhau
    x < y // => true: nhỏ hơn
    x <= y // => true: nhỏ hơn hoặc bằng
    x > y // => false: lớn hơn
    x >= y // => false: lớn hơn hoặc bằng
    "two" === "three" // => false: hai chuỗi khác nhau
    "two" > "three" // => true: "tw" lớn hơn "th" theo thứ tự bảng chữ cái
    false === (x > y) // => true: false bằng false
    // Toán tử logic kết hợp hoặc đảo ngược values boolean
    (x === 2) && (y === 3) // => true: cả hai phép so sánh đều đúng. && là AND
    (x > 3) || (y < 3) // => false: không có phép so sánh nào đúng. || là OR
    !(x === y) // => true: ! đảo ngược value boolean
    ```
    
- Nếu `expressions` của Js giống như các cụm từ, thì `statements` (câu lệnh) của Js giống như 1 câu đầy đủ. `Statements` là chủ đề của chương 5. Nói 1 cách đại khái, `expression` là thứ tính toán một value nhưng không làm bất cứ điều gì: Nó không làm thay đổi trạng thái chương trình theo bất kỳ cách nào. Mặt khác, `statements` không có `value` nhưng chung làm thay đổi state. Bạn đã thấy cách khai báo biến và `statements` gán ở trên. Loại `statement` rộng lớn khác là `control structure` (cấu trúc điều khiển), chẳng hạn như `conditionals` (điều kiện) và `loops` . Bạn sẽ thấy các ví dụ bên dưới sau khi chúng  ta tìm hiểu về `functions`
- `Function` là một block code Js được đặt tên và tham số hoá mà bạn định nghĩa một lần sau đó có thể gọi đi gọi lại nhiều lần. `Functions` không được đề cập chính thức cho đến chương 8, nhưng giống như `objects` và `arrays` bạn sẽ thấy chung nhiều lần trước khi đến chương đó. Dưới đây là 1 số ví dụ đơn giản
    
    ```jsx
    // Functions là các khối code JavaScript được tham số hóa mà chúng ta có thể gọi.
    function plus1(x) { // Định nghĩa function có tên "plus1" với tham số "x"
    return x + 1; // Trả về value lớn hơn 1 so với value được truyền vào
    } // Functions được bao bọc trong dấu ngoặc nhọn
    plus1(y) // => 4: y là 3, vì vậy lời gọi này trả về 3+1
    let square = function(x) { // Functions là values và có thể được gán cho biến
    return x * x; // Tính value của function
    }; // Dấu chấm phẩy đánh dấu kết thúc của phép gán.
    square(plus1(y)) // => 16: gọi hai functions trong một expression
    ```
    
- Trong ES6 trở lên, có 1 cú pháp viết tắt để định nghĩa `functions` . Cú pháp ngắn gọn này sử dụng `=>` để phân tách danh sách đối số khỏi phần thân function, vì vậy function được định nghĩa theo cách này được gọi là `arrow functions` . Nó thường được sử dụng nhất khi bạn muốn truyền 1 function chưa đặt tên làm đối số cho function khác. Code trước đó trông như thế này khi được viết lại để sử dụng arrow functions
    
    ```jsx
    const plus1 = x => x + 1; // Đầu vào x ánh xạ tới đầu ra x + 1
    const square = x => x * x; // Đầu vào x ánh xạ tới đầu ra x * x
    plus1(y) // => 4: lời gọi function giống nhau
    square(plus1(y)) // => 16
    ```
    
- Khi chúng ta sử dụng `function` với `object` chúng ta có `method` (phương thức)
    
    ```jsx
    // Khi functions được gán cho properties của object, chúng ta gọi
    // chúng là "methods". Tất cả JavaScript objects (bao gồm cả arrays) đều có methods:
    let a = []; // Tạo một mảng trống
    a.push(1,2,3); // Method push() thêm elements vào mảng
    a.reverse(); // Một method khác: đảo ngược thứ tự của elements
    // Chúng ta cũng có thể định nghĩa methods của riêng mình. Từ khóa "this" tham chiếu đến object
    // mà method được định nghĩa trên đó: trong trường hợp này là mảng points từ trước đó.
    points.dist = function() { // Định nghĩa method để tính khoảng cách giữa các điểm
    let p1 = this[0]; // Element đầu tiên của mảng mà chúng ta đang gọi
    let p2 = this[1]; // Element thứ hai của object "this"
    let a = p2.x-p1.x; // Hiệu số tọa độ x
    let b = p2.y-p1.y; // Hiệu số tọa độ y
    return Math.sqrt(a*a + // Định lý Pitago
    b*b); // Math.sqrt() tính căn bậc hai
    };
    points.dist() // => Math.sqrt(2): khoảng cách giữa 2 điểm của chúng ta
    ```
    
- Bây giờ như đã hứa, đây là một số functions mà phần thân của chúng thể hiện các `statements control structure`  phổ biến của Js
    
    ```jsx
    // JavaScript statements bao gồm conditionals và loops sử dụng cú pháp
    // của C, C++, Java và các ngôn ngữ khác.
    function abs(x) { // Function để tính giá trị tuyệt đối.
    if (x >= 0) { // Câu lệnh if...
    return x; // thực thi code này nếu phép so sánh là true.
    } // Đây là kết thúc của mệnh đề if.
    else { // Mệnh đề else tùy chọn
    executes its code if
    return -x; // phép so sánh là false.
    } // Dấu ngoặc nhọn tùy chọn khi có 1 statement cho mỗi mệnh đề.
    } // Lưu ý statements return được lồng bên trong if/else.
    abs(-10) === abs(10) // => true
    function sum(array) { // Tính tổng các elements của mảng
    let sum = 0; // Bắt đầu với tổng ban đầu là 0.
    for(let x of array) { // Lặp qua mảng, gán mỗi element cho x.
    sum += x; // Thêm value của element vào tổng.
    } // Đây là kết thúc của vòng lặp.
    return sum; // Trả về tổng.
    }
    sum(primes) // => 28: tổng của 5 số nguyên tố đầu tiên 2+3+5+7+11
    function factorial(n) { // Function để tính giai thừa
    let product = 1; // Bắt đầu với tích là 1
    while(n > 1) { // Lặp lại statements trong {} trong khi biểu thức trong () là true
    product *= n; // Viết tắt cho product = product * n;
    n--; // Viết tắt cho n = n - 1
    } // Kết thúc vòng lặp
    return product; // Trả về tích
    }
    factorial(4) // => 24: 1*4*3*2
    function factorial2(n) { // Một phiên bản khác sử dụng vòng lặp khác
    let i, product = 1; // Bắt đầu với 1
    for(i=2; i <= n; i++) // Tự động tăng i từ 2 lên đến n
    product *= i; // Làm điều này mỗi lần. {} không cần thiết cho vòng lặp 1 dòng
    return product; // Trả về giai thừa
    }
    factorial2(5) // => 120: 1*2*3*4*5
    ```
    
- Js hỗ trợ phong cách lập trình oop, nhưng nó khác đáng kể so với ngôn ngữ lập trình hướng đối tượng cổ điển. Chương 9 trình bày chi tiết về OOP trong Js với nhiều ví dụ. Dưới đây là 1 ví dụ đơn giản minh hoạ cách định nghĩa class Js để biểu diễn các điểm hình học 2D. Các objects là instances (thể hiện) của class này có 1 method duy nhất, có tên là `distance()` , tính toán khoảng cách của điểm từ gốc
    
    ```jsx
    class Point { // Theo quy ước, tên class được viết hoa.
    constructor(x, y) { // Constructor function để khởi tạo instances mới.
    this.x = x; // Từ khóa this là object mới đang được khởi tạo.
    this.y = y; // Lưu đối số function dưới dạng properties của object.
    } // Không cần return trong constructor functions.
    distance() { // Method để tính khoảng cách từ gốc đến điểm.
    return Math.sqrt( // Trả về căn bậc hai của x² + y².
    this.x * this.x + // this tham chiếu đến Point object mà
    this.y * this.y // method distance được gọi trên đó.
    );
    }
    }
    // Sử dụng constructor function Point() với "new" để tạo Point objects
    let p = new Point(1, 1); // Điểm hình học (1,1).
    // Bây giờ sử dụng method của Point object p
    p.distance() // => Math.SQRT2
    ```
    
- Chuyến thăm quan giới thiệu về cú pháp và khả năng cơ bản của Js kết thúc tại đây, nhưng cuốn sách vẫn tiếp tục với các chương độc lập bao gồm các tính năng bổ sung của ngôn ngữ
- Chương 10 - Modules
    - Hiển thị cách code Js trong 1 file hoặc script có thể sử dụng các functions và classes của Js được định nghĩa trong các tệp hoặc script khác
- Chương 11 - The Javascript Standard Library (Thư viện chuẩn Js)
    - Bao gồm các functions và classes tích hợp sẵn có sẵn cho tất cả các chương trình Js. Điều này bao gồm các cấu trúc dữ liệu quan trọng như `maps` `sets` `class` `regular`, `functions` ,…
- Chương 12  - Iterators and Generators (Trình lặp và trình tạo)
    - Giải thích cách thức hoạt động của for/of và cách bạn có thể làm cho classes của riêng mình có thể lặp với `for/of` . Nó cũng bao gồm các `generator functions` (hàm tạo) và câu lệnh `yield`
- Chương 13 - Asynchrnous Js (Js không đồng bộ)
    - Chương này là 1 khám phá chuyên sâu về lập trình không đồng bộ trong Js, bao gồm `callbacks` và `events` , API dựa trên `Promise` và các từ khoá `async` và `await` . Mặc dù ngôn ngữ Js côt lõi không phải là đồng bộ, nhưng API không đồng bộ là mặc định trong cả trình duyệt web và Node, chương này sẽ giải thích các kỹ thuật để làm việc với các API đó
- Chương 14 - Metaprogramming ( Siêu lập trình)
    - Giới thiệu 1 sô tính năng nâng cao của Js co thể được quan tâm bởi dev viết thư viện code cho các dev Js khác sử dụng
- Chương 15 - Js in Web Browser (Js trong trình duyệt web)
    - Giới thiệu `host enviroment` (môi trường lưu trữ) của trình duyệt web, giải thích các trình duyệt web thực thi code Js và bao gồm các API quan trọng nhất trong số rất nhiều API được định nghĩa bởi trình duyệt web. Đây là chương dài nhất trong cuốn sách
- Chương 16 - Server-Side Js with Node (Js phía server với Node)
    - Giới thiệu `host enviroment` Node bao gồm mô hình lập trình cơ bản và các cấu trúc dữ liệu và API quan trọng cần hiểu
- Chương 17 - Js Tools and Extenstions (Công cụ và Tiện ích mở rộng Js)
    - Bao gồm các công cụ và tiện tích mở rộng ngôn ngữ đáng để biết vì chúng được sử dụng rộng rãi và có thể giúp bạn trở thành một dev hiệu quả hơn

## 1.4 Example: Character Frequency Histograms

- Chương này kết thúc với một chương trình Js ngắn nhưng không tầm thường. Ví dụ bên dưới là một chương trình Node đọc văn bản từ standard input, tính toán biể đồ tần suất ký tự từ văn bản đó và sau đó in ra biể đồ. Bạn có thể gọi chương trình như thế này để phân tích tần suất ký tự của chính code nguồn của nó
    
    ```jsx
    $ node charfreq.js < charfreq.js
    T: ########### 11.22%
    E: ########## 10.15%
    R: ####### 6.68%
    S: ###### 6.44%
    A: ###### 6.16%
    N: ###### 5.81%
    O: ##### 5.45%
    I: ##### 4.54%
    H: #### 4.07%
    C: ### 3.36%
    L: ### 3.20%
    U: ### 3.08%
    /: ### 2.88%
    ```
    
- Ví dụ này sử dụng một số tính năng nâng cao của Js và nhằm mục đích chứng minh các chương trình Js trong thế giới thực có thể trông như thế nào. Bạn không nên mong đợi hiểu hết code này ngay bây giờ, nhưng hãy yên tâm rằng tất cả chúng sẽ được giải thích trong các chương tiếp theo
    
    ```jsx
    /**
    * Chương trình Node này đọc văn bản từ đầu vào tiêu chuẩn, tính toán tần suất
    * của mỗi chữ cái trong văn bản đó và hiển thị biểu đồ của
    * các ký tự được sử dụng thường xuyên nhất. Nó yêu cầu Node 12 trở lên để chạy.
    *
    * Trong môi trường kiểu Unix, bạn có thể gọi chương trình như thế này:
    * node charfreq.js < corpus.txt
    */
    // Class này mở rộng Map để method get() trả về giá trị được chỉ định
    // thay vì null khi key không có trong map
    class DefaultMap extends Map {
    constructor(defaultValue) {
    super(); // Gọi constructor của superclass
    this.defaultValue = defaultValue; // Ghi nhớ default value
    }
    get(key) {
    if (this.has(key)) { // Nếu key đã có trong map
    return super.get(key); // trả về value của nó từ superclass.
    }
    else {
    return this.defaultValue; // Nếu không, trả về default value
    }
    }
    }
    // Class này tính toán và hiển thị biểu đồ tần suất chữ cái
    class Histogram {
    constructor() {
    this.letterCounts = new DefaultMap(0); // Map từ chữ cái đến số lượng
    this.totalLetters = 0; // Tổng số chữ cái
    }
    // Function này cập nhật biểu đồ với các chữ cái của văn bản.
    add(text) {
    // Xóa khoảng trắng khỏi văn bản và chuyển đổi thành chữ hoa
    text = text.replace(/\s/g, "").toUpperCase();
    // Bây giờ lặp qua các ký tự của văn bản
    for(let character of text) {
    let count = this.letterCounts.get(character); // Lấy số lượng cũ
    this.letterCounts.set(character, count+1); // Tăng nó lên
    this.totalLetters++;
    }
    }
    // Chuyển đổi biểu đồ thành string hiển thị đồ họa ASCII
    toString() {
    // Chuyển đổi Map thành mảng các mảng [key,value]
    let entries = [...this.letterCounts];
    // Sắp xếp mảng theo số lượng, sau đó theo thứ tự bảng chữ cái
    entries.sort((a,b) => { // Function để xác định thứ tự sắp xếp.
    if (a[1] === b[1]) { // Nếu số lượng bằng nhau
    return a[0] < b[0] ? -1 : 1; // sắp xếp theo thứ tự bảng chữ cái.
    } else { // Nếu số lượng khác nhau
    return b[1] - a[1]; // sắp xếp theo số lượng lớn nhất.
    }
    });
    // Chuyển đổi số lượng thành tỷ lệ phần trăm
    for(let entry of entries) {
    entry[1] = entry[1] / this.totalLetters*100;
    }
    // Loại bỏ bất kỳ mục nhập nào nhỏ hơn 1%
    entries = entries.filter(entry => entry[1] >= 1);
    // Bây giờ chuyển đổi mỗi mục nhập thành một dòng văn bản
    let lines = entries.map(
    ([l,n]) => `${l}: ${"#".repeat(Math.round(n))} ${n.toFixed(2)}%`
    );
    // Và trả về các dòng được nối, được phân tách bằng ký tự xuống dòng.
    return lines.join("\n");
    }
    }
    // Async function (trả về Promise) này tạo một Histogram object,
    // đọc không đồng bộ các đoạn văn bản từ đầu vào tiêu chuẩn và thêm các đoạn đó vào
    // biểu đồ. Khi nó đến cuối luồng, nó trả về biểu đồ này
    async function histogramFromStdin() {
    process.stdin.setEncoding("utf-8"); // Đọc string Unicode, không phải byte
    let histogram = new Histogram();
    for await (let chunk of process.stdin) {
    histogram.add(chunk);
    }
    return histogram;
    }
    // Dòng code cuối cùng này là phần thân chính của chương trình.
    // Nó tạo một Histogram object từ đầu vào tiêu chuẩn, sau đó in biểu đồ.
    histogramFromStdin().then(histogram => {
    console.log(histogram.toString()); });
    ```
    
- Ví dụ này sử dụng nhiều tính năng của Js như `classes, maps, arrays, arrow functions, async functions, promises và template literals` . Nó cũng sử dụng các `methods` của `standrad library` như `replace()`, `toUpperCase()`, `sort()`, `filter()`,…
- Mặc dù ví dụ này hơi khó hiểu lúc đầu, nhưng nó cung cấp 1 cái nhìn tổng quan tôt về code Js trong thế giới thực có thể trông như thế nào. Khi bạn tìm hiểu sâu hơn về các tính năng của Js trong các chương tiếp theo, bạn sẽ có thể hiểu rõ hơn về code này và viết các chương trình của riêng mình

## 1.5 Summary

- Cuốn sách này giải thích Js từ cơ bản đến nâng cao. Điều này có nghĩa là chúng ta bắt đầu với các chi tiết `low-level` (cấp thấp) như `comments` , `identifiers`, `variables` và `type` ; sau đó xây dựng lên `expressions`, `statement` , `objects`  và `functions` ; và sau đó bao gồm các khái niệm trừu tượng `high-level` của ngôn ngữ như `classes` và `modules` . Tôi rất coi trọng từ “hoàn chỉnh” trong tiêu đề của cuốn sách này, và các chương sắp tới sẽ giải thích ngôn ngữ ở mức độ chi tiết mà lúc đầu co thể khiến bạn hơi “ngợp”. Tuy nhiên, để thực sự thành thao Js, bạn cần phải hiểu rõ các chi tiết và tôi hy vọng rằng bạn sẽ dành thời gian để đọc cuốn sách này từ đầu đến cuối
- Nhưng xin đừng cảm thấy rằng bạn phải cần làm điều đó ngay trong lần đọc đầu tiên. Nếu bạn thấy mình đang “sa lầy” trong 1 phần nào đó, chỉ cần bỏ qua phần tiếp theo. Bạn có thể quay lại và “nắm vững” các chi tiết sau khi bạn đã có kiến thức thực tế về ngôn ngữ nói chung
