# Objects

- Object là kiểu dữ liệu cơ bản nhất của Js và bạn đã thấy chúng nhiều lần trong các chương trước. Vì object rất quan trọng đối với ngôn ngữ Js, nên điều quan trọng là bạn phải hiểu cách chúng hoạt động một cách chi tiết và chương này cung cấp chi tiết đó. Nó bắt đầu với một cái nhìn tổng quan chính thức về các object, sau đó đi sâu vào các phần thực tế về việc tạo object và truy vấn, thiết lập, xoá, kiểm tra và liệt kê các thuộc tính của object. Các phần tập trung vào thuộc tính này được theo sau bởi các phần giải thích cách mở rộng, tuần tự hoá và định nghĩa các method quan trọng trên các object. Cuối cùng, chương kết thúc với một phần dài về cú pháp object literal mới trong ES6 và các phiên bản gần đây hơn của ngôn ngữ

## **6.1 Introduction to Objects**

- Object là một giá trị phức hợp: nó tổng hợp nhiều giá trị (giá trị nguyên thuỷ hoặc các object khác) và cho phép bạn lưu trữ và truy xuất các giá trị đó theo tên. Một object là một tập hợp các property không có thứ tự, mỗi property có tên và một giá trị. Tên property thường là chuỗi (mặc dù, như chúng ta sẽ thấy trong 6.10.3, tên property có thể là Symbol), vì vậy chúng ta có thể nói rằng các object ánh xạ chuỗi thành các giá trị. Ánh xạ chuỗi-giá trị này có nhiều tên khác nhau - bạn có thể quen thuộc với câu trúc dữ liệu cơ bản dưới tên “hash”, “hashtable”. “dictionary” hoặc “associative”. Tuy nhiên, một object không chỉ là một ánh xạ chuỗi-giá trị đơn giản. Ngoài việc duy trì tập hợp các property riêng của nó, một object Js cũng kế thừa các property của 1 object khác, được gọi là “prototype” của nó. Các property của một object thường là các method được kế thừa và “kế thừa nguyên mẫu” này là một tính năng quan trọng của Js
- Các object Js là động - các object thường có thể được thêm và xoá - nhưng chúng có thể được sử dụng để mô phỏng các object tĩnh và “struct” của các ngôn ngữ được nhập tĩnh. Chúng cũng có thể được sử dụng (bằng cách bỏ qua phần giá trị của ánh xạ chuỗi-giá trị) để biểu thị các tập hợp chuỗi
- Bất kỳ giá trị nào trong Js không phải là chuỗi, số, Symbol hoặc true, false, null hoặc undefined đều là một object. Và mặc dù chuỗi, số và boolean không phải là object, nhưng chúng có thể hoạt động như các object bất biến
- Nhớ lại từ 3.8 rằng các object có thể thay đổi và được thao tác bằng cách tham chiếu hơn là bằng giá trị. Nếu biến `x` tham chiếu đến 1 object và code `let y = x` được thực thi, thì biến `y` chứa một tham chiếu đến cùng một object, không phải là một bản sao của object đó. Bất kỳ sửa đổi nào được thực hiện đối với object thông qua biến `y` cũng hiển thị thông qua biến `x`
- Những điều phổ biến nhất cần làm với các object là tạo chúng và thiết lập, truy vấn, xoá, kiểm tra và liệt kê các property của chúng. Các thao tác cơ bản này được mô tả trong phần mở đầu của chương này. Các phần sau đó đề cập đến các chủ đề nâng cao hơn
- Property có tên và giá trị. Tên property có thể là bất kỳ chuỗi nào, bao gồm cả chuỗi rỗng (hoặc bất kỳ Symbol nào), nhưng không có object nào có thể có 2 property cùng tên. Giá trị có thể là bất kỳ giá trị Js nào hoặc nó có thể là hàm getter hoặc setter (hoặc cả 2). Chúng ta sẽ tìm hiểu về các hàm getter và setter trong 6.10.6
- Đôi khi điều quan trọng là phải có thể phân biệt giữa các property được xác định trực tiếp trên một object và các property được kế thừa từ một object nguyên mẫu. Js sử dụng thậut ngữ `thuộc tính riêng (own property)` để chỉ các property không được kế thừa
- Ngoài tên và giá trị của nó, mỗi property có ba property
    - Property `writable` chỉ định liệu giá trị của property có thể được đặt hay không
    - `enumerable` chỉ định liệu tên property có được trả về bởi vòng lặp for/in hay không
    - `configurable` chỉ định liệu property có thể bị xoá hay không và liệu các property của nó có thể bị thay đổi hay không
- Nhiều object được tích hợp sẵn của Js có các thuộc tính chỉ đọc, không thể liệt kê hoặc không thể định cấu hình. Tuy nhiên, theo mặc định, tất cả các property của object bạn tạo đều có thể ghi, có thể liệt kê và có thể định cấu hình. 14.1 giải thích các kỹ thuật để chỉ định các giá trị property không mặc định cho các object của bạn

## **6.2 Creating Objects**

- Các object có thể được tạo bằng object literal, bằng từ khoá `new` và bằng hàm `Object.create()`. Các phần phụ bên dưới mô tả từng kỹ thuật

### 6.2.1 Object Literal

- Các dễ nhất để tạo một object là bao gồm một object literal trong code Js của bạn. Ở dạng đơn giản nhất, một object literal là một danh sách cặp `name:value` được phân tách bằng dấu phẩy, được đặt trong dấu ngoặc nhọn. Tên property là một định danh Js hoặc một chuỗi ký tự (cho phép chuỗi rỗng). Giá trị property là bất kỳ biểu thức Js nào; giá trị của biểu thức (nó có thể là các giá trị nguyên thuỷ hơạc giá trị đối tượng) trở thành giá trị của property. Dưới đây là một số ví dụ
    
    ```jsx
    let empty = {}; // Một đối tượng không có thuộc tính
    let point = { x: 0, y: 0 }; // Hai thuộc tính số
    let p2 = { x: point.x, y: point.y+1 }; // Giá trị phức tạp hơn
    let book = {
      "main title": "JavaScript", // Các tên thuộc tính này bao gồm khoảng trắng,
      "sub-title": "The Definitive Guide", // và dấu gạch ngang, vì vậy hãy sử dụng chuỗi ký tự.
      for: "all audiences", // for là từ khóa dành riêng, nhưng không có dấu ngoặc kép.
      author: { // Giá trị của thuộc tính này 
                 // là một đối tượng khác.
        firstname: "David", 
        surname: "Flanagan"
      }
    };
    ```
    
- Một dấu phẩy ở cuối sau property cuối cùng trong object literal là hợp lệ và một số kiểu lập trình khuyến khích sử dụng các dấu phẩy ở cuối này để bạn ít có khả năng gây ra lỗi cú pháp nếu bạn thêm thuộc tính mới vào cuối object literal sau này
- Object literal là một biểu thức tạo và khởi tạo một object mới và riêng biệt mỗi khi nó được đánh giá. Giá trị của mỗi property được đánh giá mỗi khi literal được đánh giá. Điều này có nghĩa là một object literal có thể tạo ra nhiều object mới nếu nó xuất hiện trong phần thân của vòng lặp hoặc trong một hàm được gọi lặp đi lặp lại và các giá trị thuộc tính của các object này có thể khác nhau
- Các object literal được hiển thị ở đây sử dụng cú pháp đơn giản đã hợp lệ kể từ các phiên bản Js đầu tiên. Các phiên bản gần đây của ngôn ngữ đã giới thiệu một số tính năng object literal mới, đề cập trong 6.10

### 6.2.2 Creating Objects with new

- Toán tử `new` tạo và khởi tạo một object mới. Từ khoá `new` phải được theo sau bởi một lệnh gọi hàm. Một hàm được sử dụng theo cách này được gọi là hàm tạo (constructor) và phục vụ để khởi tạo một object mới được tạo. Js bao gồm các hàm tạo cho các kiểu tích hợp sẵn của nó
    
    ```jsx
    let o = new Object(); // Tạo một đối tượng trống: giống như {}.
    let a = new Array(); // Tạo một mảng trống: giống như [].
    let d = new Date(); // Tạo một đối tượng Date đại diện cho thời gian hiện tại
    let r = new Map(); // Tạo một đối tượng Map để ánh xạ key/value
    ```
    
- Ngoài ra hàm tạo tích hợp sẵn này, việc bạn tự định nghĩa các hàm tạo của riêng mình để khởi tạo các object mới được tạo là điều phổ biến. Làm như vậy được đề cập trong Chương 9

### **6.2.3 Prototype**

- Trước khi chúng ta có thể đề cập đến kỹ thuật tạo object thứ 3, chúng ta phải tạm dừng lại một chút để giải thích về prototype. Hầu hết mọi object Js đều có một object Js thứ 2 được liên kết với nó. Object thứ 2 này được gọi là prototype và object đầu tiên kế thừa property từ prototype
- Tất cả các object được tạo bởi object literal đều có cùng một object prototype và chúng ta có thể tham chiếu đến đối tượng prototype này trong code Js dưới dạng `Object.prototype`. Các object được tạo bằng cách sử dụng từ khoá `new` và lệnh gọi hàm sử dụng giá trị của thuộc tính `prototype` của hàm tạo làm prototype của chúng. Vì vậy, object được tạo bởi `new Object()` kế thừa từ `Object.proptotype`, giống như object được tạo bởi `{}`. Tương tự, object được tạo bởi `newArray()` sử dụng `Array.prototype` làm prototype của nó và object được tạo bởi `new Date()` sử dụng `Date.prototype`
- Điều này có thể gây nhầm lẫn khi mới học Js. Hãy nhớ: Hầu hết tất cả các object đều có prototype, nhưng chí có một số lượng tương đối nhỏ các object có property `prototype`. Chính là những object có property `prototype` này xác định prototype cho tất cả các object khác
- `Object.prototype` là một trong số ít các object không có prototype: nó không kế thừa bất kỳ property nào. Các object prototype khác là các object bình thường có prototype. Hầu hết các hàm tạo tích hợp sẵn (và hầu hết các hàm tạo do người dùng định nghĩa) đều có prototype kế thừa từ `Object.prototype`. Ví dụ `Date.prototype` kế thừa các property từ `Object.prototype`, vì vậy một object Date được tạo bởi `new Date()` kế thừa các property từ cả `Date.prototype` và `Object.prototype`. Chuỗi các object prototype được liên kết này được gọi là chuỗi prototype (prototype chain).
- Giải thích về cách thức hoạt động của kế thừa có trong 6.3.2. Chương 9 giải thích chi tiết hơn về mối liên hệ giữa prototype và hàm tạo: nó cho thấy cách xác định các object class mới bằng cách viết hàm tạo và đặt property `prototype` của nó thành object prototype sẽ được sử dụng bởi các “thể hiện” được tạo bằng hàm tạo đó. Và chúng ta sẽ học cách truy vấn (và thậm chí thay đổi) prototype của một object trong 14.3

### **6.2.4 Object.create()**

- `Object.create()` tạo một object mới, sử dụng đối số đầu tiên của nó làm prototype của object đó
    
    ```jsx
    let o1 = Object.create({x: 1, y: 2}); // o1 kế thừa các thuộc tính x và y.
    o1.x + o1.y // => 3
    ```
    
- Bạn có thể chuyển `null` để tạo một object mới không có prototype, nhưng nếu bạn làm điều này, object mới được tạo sẽ không kế thừa bất cứ thứ gì, thậm chí kể các method cơ bản như `toString()` (Có nghĩa là cũng sẽ không hoạt động toán tử +)
    
    ```jsx
    let o2 = Object.create(null); // o2 không kế thừa thuộc tính hoặc phương thức nào.
    ```
    
- Nếu bạn muốn tạo 1 object trống thông thường (giống như object được trả về bởi `{}` hoặc `new Object()`), hãy chuyển `Object.prototype`
    
    ```jsx
    let o3 = Object.create(Object.prototype); // o3 giống như {} hoặc new Object().
    ```
    
- Khả năng tạo một object mới với 1 prototype tuỳ ý là một khả năng mạnh mẽ và chúng ta sẽ sử dụng `Object.create()` ở một số nơi trong chương này. (`Object.create()` cũng nhận một đối số thứ 2 tuỳ chọn mô tả các property của object mới. Đối số thứ 2 này là một tính năng nâng cao được đề cập trong 14.1)
- Một cách sử dụng cho `Object.create()` là khi bạn muốn bảo vệ chống lại sự sửa đổi ngoài ý muốn (nhưng không độc hại) đối với 1 object bởi một hàm thư viện mà bạn không kiểm soát được. Thay vì chuyển trực tiếp object cho hàm, bạn có thể chuyển một object kế thừa từ nó. Nếu hàm đọc các thuộc tính của object đó, nó sẽ thấy các giá trị được kết thừa. Tuy nhiên, nếu nó đặt các property, thì những lần ghi đó sẽ không ảnh hưởng đến object ban đầu
- Để hiểu tại sao điều này hoạt động, bạn cần biết cách các thuộc tính được truy vấn và thiết lập trong JavaScript. Đây là chủ đề của phần tiếp theo.

## **6.3 Querying and Setting Properties**

- Để lấy giá tri của một property, hãy sử dụng toán tử (.) hoặc ([]) được mô tả trong 4.4. Vế trái phải là một biểu thức có giá trị là một object. Nếu sử dụng toán tử `.`, về phải phải là một định danh đơn giản đặt tên cho property. Nếu sử dụng dấu ngoặc vuông, giá trị trong dấu ngoặc vuông phải là một biểu thức đánh giá thành một chuỗi chứa tên property mong muốn
    
    ```jsx
    let author = book.author; // Lấy thuộc tính "author" của book.
    let name = author.surname; // Lấy thuộc tính "surname" của author.
    let title = book["main title"]; // Lấy thuộc tính "main title" của book.
    ```
    
- Để tạo hoặc thiết lập một property, hãy sử dụng dấu chấm hoặc dấu ngoặc vuông như khi bạn truy cập property nhưng đặt chúng ở vế trái của biểu thức gán
    
    ```jsx
    book.edition = 7; // Tạo thuộc tính "edition" của book.
    book["main title"] = "ECMAScript"; // Thay đổi thuộc tính "main title".
    ```
    
- Khi sử dụng ký hiệu dấu ngoặc vuông, chúng ta đã nói rằng biểu thức bên trong dấu ngoặc vuông phải được đánh giá thành một chuỗi. Một câu lệnh chính xác hơn là biểu thức phải được đánh giá thành một chuỗi hoặc một giá trị có thể được chuyển đổi thành một chuỗi hoặc thành một Symbol (6.10.3). Ví dụ, trong chương 7 chúng ta sẽ thấy rằng việc sử dụng số trong đầu dấu ngoặc vuông là phổ biến

### **6.3.1 Objects As Associative Arrays**

- Như đã giải thích trong phần trước, hai biểu thức Js sau có cùng giá trị
    
    ```jsx
    object.property
    object["property"]
    ```
    
- Cú pháp đầu tiên sử dụng dấu chấm và một định danh, giống như cú pháp được sử dụng để truy cập một môi trường tĩnh của một struct hoặc một object trong C hoặc Java. Cú pháp thứ 2 sử dụng dấu ngoặc vuông và một chuỗi, trông giống như truy cập mảng, nhưng đối với 1 mảng được lập index bằng chuỗi chứ không phải bằng số. Loại mảng này gọi là mảng kết hợp (associative arrays) (hoặc hash hoặc map hoặc dictionary). Các object Js là mảng kết hợp và phần này giải thích lý do tại sao điều đó quan trọng
- Trong C, C++, Java và một số ngôn ngữ được nhập mạnh tương tự, một object chỉ có thể có một số lượng property cố định và tên của các property này phải được xác định trước. Vì Js là một ngôn ngữ được nhập lỏng lẻo, nên quy tắc này không được áp dụng: một chương trình có thể tạo bất kỳ số lượng property nào trong bất kỳ object nào. Tuy nhiên khi bạn sử dụng toán tử `.` để truy cập 1 property của object, tên của property được biểu thị dưới dạng một định danh. Các định danh phải được nhập theo đúng nghĩa đen vào chương trình Js của bạn; chúng không phải là một kiểu dữ liệu, vì vậy chúng không thể thao tác bởi chương trình
- Mặt khác, khi bạn truy cập một property của 1 object bằng `[]`, tên của property được biểu thị dưới dạng 1 chuỗi. Chuỗi là kiểu dữ liệu Js, vì vậy chúng có thể được thao tác và tạo trong khi chương trình đang chạy. Vì vậy, ví dụ, bạn có thể viết code sau trong Js
- Đoạn mã này đọc và nối các thuộc tính address0, address1, address2 và address3 của đối tượng customer.
- Ví dụ ngắn gọn này thể hiện tính linh hoạt của việc sử dụng ký hiệu mảng để truy cập các property của một object với các biểu thức chuỗi. Đoạn code này có thể viết lại bằng cách sử dụng ký hiệu `.`, nhưng có những trường hợp mà chỉ có `[]` mới thực hiện được. Ví dụ, giả sử bạn viết một chương trình sử dụng tài nguyên mạng để tính toán giá trị hiện tại của các khoản đầu tư của thị trường chứng khoán của người dùng. Chương trình cho phép người dùng nhập tên của từng cổ phiếu mà họ sở hữu cũng như số lượng cổ phiếu của từng cổ phiếu. Bạn có thể sử dụng một object có tên `portfolio` để lưu giữ thông tin này. Object có một property cho mỗi cổ phiếu. Tên của property là tên của mỗi cổ phiếu và giá trị property là số lượng cổ phiếu đó. Vì vậy, nếu người dùng nắm giữ 50 cổ phiếu IBM thì property [`portfolio.ibm`](http://portfolio.ibm) có giá trị là 50
- Một phần của chương trình này có thể là một hàm để thêm một cổ phiếu mới vào danh mục đầu tư
    
    ```jsx
    function addstock(portfolio, stockname, shares) {
      portfolio[stockname] = shares;
    }
    ```
    
- Ví dụ người dùng nhập tên cổ phiếu tại thời điểm chạy, nên không có cách nào để bạn biết tên property trước thời hạn. Vì bạn không thể biết tên property khi bạn viết chương trình, nên không có cách nào để bạn sử dụng toán tử `.` để truy cập các property của object `portfolio`. Tuy nhiên bạn có thể sử dụng toán tử `[]` vì nó sử dụng giá trị chuỗi (là động và có thể thay đổi trong thời gian chạy) thay vì định danh (là tĩnh và được mã hoá cứng trong chương trình) để đặt tên cho property
- Trong chương 5, chúng ta đã giới thiệu vòng lặp `for/in` (và chúng ta sẽ thấy nó một lần nữa trong thời gian ngắn, trong 6.6). Sức mạnh của câu lệnh JS này trở nên rõ ràng khi bạn xem xét việc sử dụng nó với mảng kết hợp. Đây là cách bạn sẽ sử dụng nó khi tính toán tổng giá trị của một danh mục đầu tư
    
    ```jsx
    function computeValue(portfolio) {
      let total = 0.0;
      for(let stock in portfolio) { // Đối với mỗi cổ phiếu trong danh mục đầu tư:
        let shares = portfolio[stock]; // lấy số lượng cổ phiếu
        let price = getQuote(stock); // tra cứu giá cổ phiếu
        total += shares * price; // thêm giá trị cổ phiếu vào tổng giá trị
      }
      return total; // Tr trả về tổng giá trị.
    }
    ```
    
- Các object Js thường được sử dụng làm mảng kết hợp như được hiển thị ở đây và điều quan trọng là phải hiểu được cách thức hoạt động này. Tuy nhiên, trong ES6 trở lên, class Map được mô tả trong 11.1.2 thường là lựa chọn tốt hơn so với việc sử dụng 1 object đơn giản

### **6.3.2 Inheritance**

- Các object Js có một tập hợp “property riêng” và chúng cũng kế thừa một tập hợp các property từ prototype object (object nguyên mẫu) của chúng. Để hiểu điều này, chúng ta phải xem xét việc truy cập property chi tiết hơn. Các ví dụ trong phần này sử dụng `Object.create()` để tạo các object với các `prototype` được chỉ định. Tuy nhiên, chúng ta sẽ thấy trong chương 9, mỗi khi bạn tạo một thể hiện mới với `new`, bạn đang tạo 1 object kế thừa các property từ một prototype object
- Giả sử  bạn truy vấn property `x` trong object `o`. Nếu `o` không có property riêng có tên đó, thì prototype object của `o` được truy vấn cho property `x`. Nếu prototype object không có property riêng có tên đó, nhưng bản thân nó có một prototype, thì truy vấn được thực hiện trên prototype của prototype. Điều này tiếp tục cho đến khi tìm thấy property `x` hoặc đến khi object prototype `null` được tìm kiếm. Như bạn có thể thấy, prototype attribute của một object tạo ra một chuỗi danh sách được liên kết mà từ đó các property được kế thừa
    
    ```jsx
    let o = {}; // o kế thừa các phương thức đối tượng từ Object.prototype
    o.x = 1; // và bây giờ nó có thuộc tính riêng x.
    let p = Object.create(o); // p kế thừa các thuộc tính từ o và Object.prototype
    p.y = 2; // và có thuộc tính riêng y.
    let q = Object.create(p); // q kế thừa các thuộc tính từ p, o, và ...
    q.z = 3; // ... Object.prototype và có thuộc tính riêng z.
    let f = q.toString(); // toString được kế thừa từ Object.prototype
    q.x + q.y // => 3; x và y được kế thừa từ o và p
    ```
    
- Bây giờ giả sử bạn gán cho property `x` của object `o`. Nếu `o` đã có một property riêng (không phải kế thừa) có tên `x`, thì phép gán chỉ đơn giản là thay đổi giá trị của property hiện có này. Nếu không, phép gán này sẽ tạo một property mới có tên là `x` trên object `o`. Nếu `o` trước đó đã kế thừa property `x` thì property được kế thừa đó bây giờ bị ẩn bởi property riêng mới được tạo có cùng tên
- Phép gán property chỉ kiểm tra chuỗi prototype để xem phép gán có được phép hay không. Ví dụ, nếu `o` kế thừa một property chỉ đọc có tên `x`, thì phép gán không được phép. (Chi tiết về thời điểm có thể đặt property có trong 6.3.3). Tuy nhiên, nếu phép gán được phép, thì nó luôn tạo hoặc đặt một property trong object ban đầu và không bao giờ sửa đổi các object trong prototype. Thực tế là kế thừa xảy ra khi truy vấn các property nhưng không xảy ra khi thiết lập chúng là một tính năng quan trọng của Js vì nó cho phép chúng ta ghi đè một cách có chọn lọc các property được kế thừa
    
    ```jsx
    let unitcircle = { r: 1 }; // Một đối tượng để kế thừa từ
    let c = Object.create(unitcircle); // c kế thừa thuộc tính r
    c.x = 1; c.y = 1; // c định nghĩa hai thuộc tính riêng của nó
    c.r = 2; // c ghi đè thuộc tính được kế thừa của nó
    unitcircle.r // => 1: nguyên mẫu không bị ảnh hưởng
    ```
    
- Có một ngoại lệ đối với quy tắc mà phép gán property không thành công hoặc tạo, đặt property trong object ban đầu. Nếu `o` kế thừa property `x` và property đó là property accessor với method setter (6.10.6), thì method setter đó được gọi thay vì tạo property `x` mới trong `o`. Tuy nhiên, lưu ý rằng method setter được gọi trên object `o`, không phải trên object prototype định nghĩa property, vì vậy nếu method setter định nghĩa bất kỳ property nào, nó sẽ làm như vậy trên `o` và nó sẽ để lại nguyên chuỗi prototype không bị sửa đổi

### **6.3.3 Property Access Errors**

- Các biểu thức truy cập property không phải lúc nào cũng trả về hoặc thiết lập 1 giá trị. Phần này sẽ giải thích những điều có thể xảy ra sai sót khi bạn truy vấn hoặc đặt một property
- Việc truy vấn một property không tồn tại không phải lỗi. Nếu property `x` không được tìm thấy dưới dạng property riêng hoặc property được kế thừa bởi `o`, thì biểu thức truy cập property `o.x` được đánh giá thành undefined. Nhớ lại object book của chúng ta có property `sub-title` nhưng không có property `subtitle`
    
    ```php
    book.subtitle // => undefined: thuộc tính không tồn tại
    ```
    
- Tuy nhiên, việc cố gắng truy cập một property của một object không tồn tại là một lỗi. Các giá trị null và undefined không có property và việc truy vấn các property của giá trị này là một lỗi
    
    ```php
    let len = book.subtitle.length; // !TypeError: undefined không có length
    ```
    
- Các biểu thức truy cập property sẽ không thành công nếu vế trái  của `.` là `null` hoặc `undefined`. Vì vậy khi viết 1 biểu thức như [`book.author](http://book.author).surname` bạn cần phải cẩn thận nếu bạn không chắc chắn rằng book và book.author thực sự được xác định. Dưới đây là 2 cách để bảo vệ chống lại loại vấn đề này
    
    ```php
    // Một kỹ thuật dài dòng và rõ ràng
    let surname = undefined;
    if (book) {
      if (book.author) {
        surname = book.author.surname;
      }
    }
    
    // Một cách thay thế ngắn gọn và惯用 để lấy họ hoặc null hoặc undefined
    surname = book && book.author && book.author.surname;
    ```
    
- Để hiểu tại sao biểu thức này hoạt động để ngăn chặn các `TypeError`, bạn có thể cần xem lại toán tử `&&` trong 4.10.1
- Như được mô tả trong 4.4.1, ES2020 hỗ trợ truy cập property có điều kiện với `?.`, cho phép chúng ta viết lại biểu thức gán trước đó
    
    ```php
    let surname = book?.author?.surname;
    ```
    
- Cố gắng thiết lập một property trên null hoặc undefined cũng gây ra `TypeError`. Nỗ lực thiết lập các property trên các giá trị khác cũng không phải lúc nào cũng thành công: một số property chỉ đọc không thể thiết lập và một số object cũng không cho phép thêm property mới. Ở chế độ strict (5.6.3), TypeError được ném ra bất cứ khi nào cố gắng thiết lập một property không thành công, ở chế độ non-strict thì điều này thường im lặng
- Các quy tắc chỉ định khi nào phép gán property thành công và khi nào nó không thành công là trực quan nhưng khó diễn đạt một cách ngắn gọn. Nỗ lực thiết lập property `p` của object `o` không thành công trong các trường hợp sau
    - `o` có property riêng `p` chỉ đọc: không thể thiết lập các property chỉ đọc
    - `o` có property kế thừa `p` chỉ đọc: không thể ẩn property chỉ đọc kế thừa bằng property riêng cùng tên
    - `o` không có property riêng `p`; `o` không kế thừa property `p` với method setter và property mở rộng của `p` (xem 14.2) là `false`. Vì `p` chưa tồn tại trong `o` và nếu không có method setter nào để gọi, thì `p` phải được thêm vào `o`. Nhưng nếu `o` không thể mở rộng, thì không thể định nghĩa các property mới trên đó

## **6.4 Deleting Properties**

- Toán tử `delete` (4.13.4) loại bỏ một property khỏi một object. Toán hạng duy nhất của nó là một biểu thức truy cập property. Đáng ngạc nhiên, `delete` không hoạt động trên giá trị của property mà trên chính property
    
    ```jsx
    delete book.author; // Đối tượng book hiện không có thuộc tính author.
    delete book["main title"]; // Bây giờ nó cũng không có "main title".
    ```
    
- Toán tử delete chỉ xoá các property riêng, không xoá các property kế thừa. (Để xoá một property được kế thừa, bạn phải xoá nó khỏi prototype object mà nó được xác định. Làm điều này ảnh hưởng đến mọi object kế thừa từ prototype đó).
- Biểu thức delete được đánh giá là true nếu việc xoá thành công hoặc việc xoá không có tác dụng (chẳng hạn như xoá một property không tồn tại. `delete` cũng được đánh giá là true khi được sử dụng (vô nghĩa) với một biểu thức không phải là biểu thức truy cập property
    
    ```jsx
    let o = {x: 1}; // o có thuộc tính riêng x và kế thừa thuộc tính toString
    delete o.x // => true: xóa thuộc tính x
    delete o.x // => true: không làm gì cả (x không tồn tại) nhưng vẫn là true
    delete o.toString // => true: không làm gì cả (toString không phải là thuộc tính riêng)
    delete 1 // => true: vô nghĩa, nhưng vẫn là true
    ```
    
- `delete` không loại bỏ các property có property configurable là false. Các property nhất định của các object tích hợp sẵn không thể định cấu hình, cũng như các property của global object được tạo ở khai báo biến và hàm. Ở chế độ strict, việc cố gắng xoá một property không thể định cấu hình sẽ gây ra `TypeError`. Ở chế độ non-strict, delete chỉ đơn giản là đánh giá thành false
    
    ```jsx
    // Ở chế độ strict, tất cả các lần xóa này đều ném ra TypeError thay vì trả về false
    delete Object.prototype // => false: thuộc tính không thể định cấu hình
    var x = 1; // Khai báo một biến toàn cục
    delete globalThis.x // => false: không thể xóa thuộc tính này
    function f() {} // Khai báo một hàm toàn cục
    delete globalThis.f // => false: cũng không thể xóa thuộc tính này
    ```
    
- Khi xoá một property có thể định cấu hình của global object ở chế độ non-strict, bạn có thể bỏ qua tham chiếu đến global object và chỉ cần theo toán tử delete với tên property
    
    ```jsx
    globalThis.x = 1; // Tạo một thuộc tính toàn cục có thể định cấu hình (không có let hoặc var)
    delete x // => true: thuộc tính này có thể bị xóa
    ```
    
- Tuy nhiên, ở chế độ strict, delete đưa ra SyntaxError nếu toán hạng của nó là một định danh không đủ điều kiện như `x` và bạn phải rõ ràng về việc truy cập property
    
    ```jsx
    delete x; // SyntaxError ở chế độ strict
    delete globalThis.x; // Điều này hoạt động
    ```
## **6.5 Testing Properties**

- Các object Js có thể được coi là tập hợp các property và thường rất hữu ích khi có thể kiểm tra sự tồn tại trong tập hợp - để kiểm tra xem một object có property có tên nhất định hay không. Bạn có thể làm điều này với toán tử `in`, với các method `hasOwnProperty()` và `propertyIsEnumerable()`, hoặc đơn giản bằng cách truy vấn property. Các ví dụ được hiển thị ở đây đều sử dụng chuỗi làm tên property, nhưng chúng cũng hoạt động với Symbol(6.10.3)
- Toán tử `in` mong đợi một tên property ở bên trái và một object ở bên phải. Nó trả về true nếu object có property riêng hoặc property được kế thừa theo tên đó
    
    ```jsx
    let o = { x: 1 };
    "x" in o // => true: o có thuộc tính riêng "x"
    "y" in o // => false: o không có thuộc tính "y"
    "toString" in o // => true: o kế thừa thuộc tính toString
    ```
    
- Method `hasOwnProperty()` của một object kiểm tra xem object đó có property riêng có tên nhất định hay không. Nó trả về false cho các property được kế thừa
    
    ```jsx
    let o = { x: 1 };
    o.hasOwnProperty("x") // => true: o có thuộc tính riêng x
    o.hasOwnProperty("y") // => false: o không có thuộc tính y
    o.hasOwnProperty("toString") // => false: toString là thuộc tính được kế thừa
    ```
    
- Method `propertyIsEnumerable()` tinh chỉnh kiểm tra `hasOwnProperty()` . Nó chỉ trả về true nếu property được đặt tên là property riêng và property `enumerable()` của nó là true. Các property tích hợp sẵn nhất định không thể liệt kê được. Các property được định nghĩa bằng Js thường có thể liệt kê được trừ khi bạn sử dụng một trong các kỹ thuật được hiển thị trong 14.1 để làm cho chúng không thể liệt kê được
    
    ```jsx
    let o = { x: 1 };
    o.propertyIsEnumerable("x") // => true: o có thuộc tính riêng có thể liệt kê x
    o.propertyIsEnumerable("toString") // => false: không phải là thuộc tính riêng
    Object.prototype.propertyIsEnumerable("toString") // => false: không thể liệt kê
    ```
    
- Thay vì sử dụng toán tử in, thường thì chỉ cần truy vấn property và sử dụng `!==` để đảm bảo rằng nó không phải là `undefined`
    
    ```jsx
    let o = { x: 1 };
    o.x !== undefined // => true: o có thuộc tính x
    o.y !== undefined // => false: o không có thuộc tính y
    o.toString !== undefined // => true: o kế thừa thuộc tính toString
    ```
    
- Có một điều mà toán tử `in` làm được mà kỹ thuật truy cập property đơn giản được hiển thị ở đây không thể hiện được. `in` có thể phân biệt giữa các property không tồn tại và các property tồn tại nhưng đã được đặt thành undefined
    
    ```jsx
    let o = { x: undefined }; // Thuộc tính được đặt rõ ràng thành undefined
    o.x !== undefined // => false: thuộc tính tồn tại nhưng là undefined
    o.y !== undefined // => false: thuộc tính thậm chí không tồn tại
    "x" in o // => true: thuộc tính tồn tại
    "y" in o // => false: thuộc tính không tồn tại
    delete o.x; // Xóa thuộc tính x
    "x" in o // => false: nó không còn tồn tại nữa
    ```
## **6.6 Enumerating Properties**

- Thay vì kiểm tra sự tồn tại của các property riêng lẻ, đôi khi, chúng ta muốn lặp lại hoặc lấy danh sách tất cả các property của một object. Có một số cách khác nhau để làm điều này
- Vòng lặp for in được đề cập trong 5.4.5. Nó chạy phần thân của vòng lặp một lần cho mỗi property có thể liệt kê (riêng hoặc được kế thừa) của object được chỉ định, gán tên của property cho biến vòng lặp. Các method tích hợp mà các object kế thừa không thể liệt kê được, nhưng các property mà code của bạn thêm vào object, có thể liệt kê được theo mặc định
    
    ```jsx
    let o = {x: 1, y: 2, z: 3}; // Ba thuộc tính riêng có thể liệt kê
    o.propertyIsEnumerable("toString") // => false: không thể liệt kê
    for(let p in o) { // Lặp qua các thuộc tính
      console.log(p); // In x, y và z, nhưng không phải toString
    }
    ```
    
- Để bảo vệ chống lại việc liệt kê các property được kế thừa bằng for in, bạn có thể kiểm tra rõ ràng bên trong phần thân của vòng lặp
    
    ```jsx
    for(let p in o) {
      if (!o.hasOwnProperty(p)) continue; // Bỏ qua các thuộc tính được kế thừa
    }
    
    for(let p in o) {
      if (typeof o[p] === "function") continue; // Bỏ qua tất cả các phương thức
    }
    ```
    
- Như một cách thay thế cho việc sử dụng vòng lặp for in, thường dễ dàng hơn để lấy một mảng các tên property cho một object và sau đó lặp qua mảng đó bằng vòng lặp for of. Có 4 hàm bạn có thể sử dụng để lấy một mảng các tên property
    - `Object.keys()` trả về một mảng các tên property riêng có thể liệt kê của một object. Nó không bao gồm các property không thể liệt kê, các property được kế thừa hoặc các property có tên là Symbol (6.10.3)
    - `Object.getOwnPropertyNames()` hoạt động như Object.keys() nhưng trả về một mảng các tên của property riêng không thể liệt kê, miễn là tên của chúng không phải là chuỗi
    - `Object.getOwnPropertySymbols()` trả về các property riêng có tên là Symbol, cho dù chúng có liệt kê hay không
    - `Reflect.ownKeys()` trả về tất cả các tên property riêng, cả có thể và không thể liệt kê và cả chuỗi và Symbol (14.6)
- Có các ví dụ về việc sử dụng `Object.keys()` với vòng lặp for of trong 6.7

### **6.6.1 Property Enumeration Order**

- ES6 chính thức xác định thứ tự mà các property của một object được liệt kê. 4 method ở trên và các method có liên quan như `JSON.stringify()` đều liệt kê các property theo thứ tự sau, tuân theo các ràng buộc bổ sung của riêng chúng về việc liệu chúng có thể liệt kê các property không thể liệt kê hay các property có tên là chuỗi hoặc Symbol hay không:
    - Các property chuỗi có tên là số nguyên không âm được liệt kê trước, theo thứ tự từ số nhỏ nhất đến số lớn nhất. Quy tắc này có nghĩa là các array và object sẽ có các property của chúng được liệt kê theo thứ tự
    - Sau khi tất cả các property trông như index array được liệt kê, tất cả các property còn lại có tên chuỗi được liệt kê (bao gồm cả các property trông giống như số âm hoặc float). Các property này được liệt kê theo thứ tự chúng được thêm vào object. Đối với các property được xác định trong object literal, thứ tự này giống như thứ tự xuất hiện trong literal
    - Cuối cùng, các property có tên là Symbol object được liệt kê theo thứ tự chúng được thêm vào object
- Thứ tự liệt kê cho vòng lặp for in không được chỉ định chặt chẽ như đối với hàm liệt kê này, nhưng các triển khai thường liệt kê các property riêng theo thứ tự vừa mô tả, sau đó đi lên chuỗi prototype liệt kê các property theo thứ tự cho mỗi prototype object. Tuy nhiên lưu ý rằng một property sẽ không được liệt kê nếu một property có cùng tên đã được liệt kê hoặc ngay cả khi một property không thể liệt kê có cùng tên đã được xem xét

## **6.7 Extending Objects**

- Một thao tác phổ biến trong các chương trình Js là cần sao chép các property của object sang một object khác. Thật dễ ràng để làm điều đó với code này
    
    ```php
    let target = {x: 1}, source = {y: 2, z: 3};
    for(let key of Object.keys(source)) {
      target[key] = source[key];
    }
    target // => {x: 1, y: 2, z: 3}
    ```
    
- Nhưng vì đây là một thao tác phổ biến, nên các framework Js khác nhau đã định nghĩa các hàm tiện ích, thường được đặt tên là extend(), để thực hiện thao tác sao chép này. Cuối cùng, trong ES6, khả năng này được đưa vào Js cốt lõi dưới dạng `Object.assign()`
- `Object.assign()` mong đợi 2 hoặc nhiều object làm đối số của nó. Nó sửa đổi và trả về đối số đầu tiên, là đối tượng đích nhưng không thay đổi đối số thứ hai hoặc bất kỳ đối số nào tiếp theo, là các object nguồn. Đối với các object nguồn, nó sao chép các property riêng có thể liệt kê của object đó (bao gồm cả những property có tên là Symbol) vào đối tượng đích. Nó xử lý các đối tượng nguồn theo thứ tự danh sách đối số để các property trong object nguồn đầu tiên ghi đè các property có cùng tên trong object đích và các property trong object nguồn thứ 2 (nếu có) ghi đè các property cùng tên trong object nguồn đầu tiên
- `Object.assign()` sao chép các property với các thao tác lấy và đặt property thông thường, vì vậy nếu một object nguồn có method getter hoặc object đích có method setter, chúng sẽ được gọi trong quá trình sao chép nhưng bản thân chúng sẽ không được sao chép
- Một lý do để gán một property từ object này sang object khác là khi bạn có một object xác định các giá trị mặc định cho nhiều property và bạn muốn sao chép các property mặc định đó vào một object khác nếu property có tên đó chưa tồn tại trong object đó. Sử dụng `Object.assign()` một cách ngây thơ sẽ không làm những gì bạn muốn
    
    ```php
    Object.assign(o, defaults); // ghi đè mọi thứ trong o bằng defaults
    ```
    
- Thay vào đó, những gì bạn có thể làm là tạo một object mới, sao chép các giá trị mặc định vào đó, sau đó ghi đè các mặc định đó bằng các property trong o
    
    ```php
    o = Object.assign({}, defaults, o);
    ```
    
- Chúng ta sẽ thấy trong 6.10.4 rằng bạn có thể biểu thị các thao tác sao chép và ghi đè object này bằng cách sử dụng toán tử spead `...` như sau
    
    ```php
    o = {...defaults, ...o};
    ```
    
- Chúng ta cũng có thể tránh chi phí tạo và sao chép object bổ sung bằng cách viết một phiên bản của `Object.assign()` chỉ sao chép các property nếu chúng bị thiếu
    
    ```php
    // Giống như Object.assign() nhưng không ghi đè các thuộc tính hiện có
    // (và cũng không xử lý các thuộc tính Symbol)
    function merge(target, ...sources) {
      for(let source of sources) {
        for(let key of Object.keys(source)) {
          if (!(key in target)) { // Điều này khác với Object.assign()
            target[key] = source[key];
          }
        }
      }
      return target;
    }
    
    Object.assign({x: 1}, {x: 2, y: 2}, {y: 3, z: 4}) // => {x: 2, y: 3, z: 4}
    merge({x: 1}, {x: 2, y: 2}, {y: 3, z: 4}) // => {x: 1, y: 2, z: 4}
    ```
    
- Việc viết các tiện ích thao tác property khác như hàm `merge()` này rất đơn giản. Ví dụ hàm `restrict()` có thể xoá các property của một object nếu chúng không xuất hiện trong một object mẫu khác. Hoặc 1 hàm `substract()` có thể loại bỏ tất cả các property của một object khỏi một object khác

## **6.8 Tuần tự hóa đối tượng (Serializing Objects)**

- Tuần tự hoá object là quá trình chuyển đổi trạng thái của một object thành một chuỗi mà từ đó nó có thể được khôi phục sau này. Các hàm `JSON.stringify()` và `JSON.parse()` tuần tự hoá và khôi phục các object Js. Các hàm này sử dụng định dạng trao đổi dữ liệu JSON. JSON là viết tắt của `Javascript Object Notation` và cú pháp của nó rất giống với cú pháp của object literal và array literal của Js
    
    ```php
    let o = {x: 1, y: {z: [false, null, ""]}}; // Định nghĩa một đối tượng thử nghiệm
    let s = JSON.stringify(o); // s == '{"x":1,"y":{"z":[false,null,""]}}'
    let p = JSON.parse(s); // p == {x: 1, y: {z: [false, null, ""]}}
    ```
    
- Cú pháp JSON là một tập hợp con của cú pháp JS và nó không thể biểu diễn tất cả  các giá trị JS. Các object, array, chuỗi, số hữu hạn, true, false và null được hỗ trợ và có thể được tuần tự hoá khôi phục. `NaN, Infinity và -Infinity` được tuần tự hoá thành null. Các object Date được tuần tự hoá thành các chuỗi ngày được định dạng theo ISO (xem hàm `Date.toJson())`, nhưng `Json.parse()` để chúng ở dạng chuỗi và không khôi phục object date ban đầu. Các object function, regexp, error và giá trị undefined không thể được tuần tự hoá hoặc khôi phục. `JSON.stringify()` chỉ tuần tự hoá các property riêng có thể liệt kê của 1 object. Nếu một giá trị của property không thể được tuần tự hoá, thì property đó chỉ đơn giản là bị bỏ qua khỏi đầu ra được tuần tự hoá thành chuỗi
- Cả `JSON.stringify()` và `JSON.parse()` đều chấp nhận các đối số thứ 2 tuỳ chọn có thể được sử dụng để điều chỉnh quá trình tuần tự hoá và/hoặc khôi phục bằng cách chỉ định danh sách các property được tuần tự hoá, ví dụ, hoặc bằng cách chuyển đổi các giá trị nhất định trong quá trình tuần tự hoá hoặc chuỗi hoá. Tài liệu đầy đủ cho các hàm này có trong 11.6

## **6.9 Phương thức đối tượng (Object Methods)**

- Như đã thảo luận trước đó, tất cả các object Js (ngoại trừ những object được tạo rõ ràng mà không có prototype) đều kế thừa các property từ `Object.prototype`. Các property được kế thừa này chủ yếu là các method và vì chúng có sẵn ở mọi nơi, nên chúng đặc biệt được các lập trình viên JS quan tâm. Ví dụ chúng ta đã thấy các method `hasOwnProperty()` và `propertyIsEnumerable()`. (Và chúng ta cũng đã đề cập đến khá nhiều hàm tĩnh được định nghĩa trên hàm tạo object, chẳng hạn như `Object.create()` và `Object.keys()`.) Phần này giải thích một số object method phổ biến được định nghĩa trên `Object.prototype` nhưng được dự định sẽ được thay thế bằng các triển khai khác, chuyên biệt hơn. Trong các phần tiếp theo, chúng ta sẽ chỉ ra các ví dụ về việc định nghĩa các method này trên một object duy nhất. Trong chương 9, bạn sẽ tìm hiểu cách định nghĩa các method này một cách tổng quát hợn cho toàn bộ class object

### **6.9.1 Phương thức toString()**

- `toString()` method không nhận đối số, nó trả về một chuỗi bằng một cách nào đó biểu diễn giá trị của object mà nó được gọi. Js gọi method này của một object bất cứ khi nào nó cần chuyển đổi object thành một string. Ví dụ điều này xảy ra khi bạn sử dụng toán tử `+` để nối 1 chuỗi với một object hoặc khi bạn chuyển một object cho một method mong đợi 1 chuỗi
- Method `toString()` mặc định không cung cấp nhiều thông tin (mặc dù nó hữu ích để xác định class của 1 object, như chúng ta sẽ thấy trong 14.4.3). Ví dụ dòng code sau chỉ đơn giản là đánh giá thành chuỗi “[object Object]”
    
    ```jsx
    let s = { x: 1, y: 1 }.toString(); // s == "[object Object]"
    ```
    
- Vì method mặc định này không hiển thị nhiều thông tin hữu ích, nên nhiều class định nghĩa các phiên bản toString() của riêng chúng. Ví dụ 1 mảng được chuyển đổi thành một chuỗi, bạn sẽ nhận được 1 danh sách các phần tử của mảng, mỗi phần tử tự chuyển đổi thành một chuỗi và khi một hàm được chuyển đổi thành một chuỗi, bạn sẽ nhận được mã nguồn của hàm. Bạn có thể định nghĩa method `toString() của riêng mình như thế này
    
    ```jsx
    let point = {
      x: 1,
      y: 2,
      toString: function() { return `(${this.x}, ${this.y})`; }
    };
    String(point) // => "(1, 2)": toString() được sử dụng để chuyển đổi chuỗi
    ```
    

### **6.9.2 Phương thức toLocaleString()**

- Ngoài method `toString()` cơ bản, tất cả các object đều có `toLocaleString()`. Mục đích của method này là trả về một biểu diễn chuỗi được bản địa hoá object. Method này mặc định được định nghĩa bởi Object không tự thực hiện bất kỳ bản địa hoá nào: nó chỉ đơn giản là gọi `toString()` và trả về giá trị đó
- Các class `Date` và `Number` định nghĩa các phiên bản tuỳ chỉnh của `toLocaleString()` cố gắng định dạng số, ngày và giờ theo quy ước địa phương. `Array` định nghĩa một method `toLocaleString()` hoạt động giống như toString() ngoại trừ việc nó định dạng các phần tử mảng bằng cách gọi các method `toLocaleString()` của chúng thay vì các method toString() của chúng. Bạn có thể làm điều tương tự với một `point` như thế này
    
    ```jsx
    let point = {
      x: 1000,
      y: 2000,
      toString: function() { return `(${this.x}, ${this.y})`; },
      toLocaleString: function() {
        return `(${this.x.toLocaleString()}, ${this.y.toLocaleString()})`;
      }
    };
    point.toString() // => "(1000, 2000)"
    point.toLocaleString() // => "(1,000, 2,000)": lưu ý dấu phân cách hàng nghìn
    ```
    

### **6.9.3 Phương thức valueOf()**

- Method `valueOf()` rất giống với method `toString()` , nhưng nó được gọi khi Js cần chuyển đổi 1 object thành một số kiểu nguyên thuỷ nào đó khác ngoài chuỗi - thường là một số. Js tự động gọi method này nếu một object được sử dụng trong ngữ cảnh yêu cầu giá trị nguyên thuỷ. `valueOf` method mặc định không làm gì thú vị, nhưng một số class tích hợp sẵn định nghĩa method valueOf() của riêng chúng. Class Date định nghĩa valueOf() để chuyển đổi ngày thành số và điều này cho phép object Date được so sánh theo thứ tự thời gian với `<` và `>`. Bạn có thể làm một điều gì đó tương tự với một object `point`, định nghĩa một method valueOf() trả về khoảng cách từ gốc đến điểm
    
    ```jsx
    let point = {
      x: 3,
      y: 4,
      valueOf: function() { return Math.hypot(this.x, this.y); }
    };
    Number(point) // => 5: valueOf() được sử dụng để chuyển đổi sang số
    point > 4 // => true
    point > 5 // => false
    point < 6 // => true
    ```
    

### **6.9.4 Phương thức toJSON()**

- `Object.prototype` không thực sự định nghĩa method `toJson()`, nhưng method `JSON.stringify()` (xem 6.8) sẽ tìm kiếm method `toJSON()` trên bất cứ object nào mà nó được yêu cầu tuần tự hoá. Nếu method này tồn tại trên object sẽ được tuần tự hoá, nó sẽ được gọi và giá trị trả về được tuần tự hoá, thay vì object ban đầu. Class `Date` (xem 11.4) định nghĩa một method `toJSON()` trả về một biểu diễn chuỗi có thể tuần tự hoá của ngày. Chúng ta có thể làm điều tương tự  cho object `Point` của mình như thế này
    
    ```jsx
    let point = {
      x: 1,
      y: 2,
      toString: function() { return `(${this.x}, ${this.y})`; },
      toJSON: function() { return this.toString(); }
    };
    JSON.stringify([point]) // => '["(1, 2)"]'
    ```
    
## **6.10 Cú pháp object literal mở rộng (Extended Object Literal Syntax)**

- Các phiên bản gần đây của Js đã mở rộng cú pháp cho object literal theo một số cách hữu ích. Các phần phụ sau đây sẽ giải thích các phần mở rộng này

### **6.10.1 Thuộc tính viết tắt (Shorthand Properties)**

- Giả sử bạn có các giá trị được lưu trữ trong biến x và y và muốn tạo một object có các property có x và y chứa các giá trị đó. Với object literal cơ bản, bạn phải lặp lại mỗi định danh này 2 lần
    
    ```jsx
    let x = 1, y = 2;
    let o = {
      x: x,
      y: y
    };
    ```
    
- Trong ES6 trở lên, bạn có thể bỏ hai dấu hai chấm và một bản sao của định danh và kết thúc với code đơn giản hơn nhiều
    
    ```jsx
    let x = 1, y = 2;
    let o = { x, y };
    o.x + o.y // => 3
    ```
    

### **6.10.2 Tên thuộc tính được tính toán (Computed Property Names)**

- Đôi khi bạn cần tạo một object với một property cụ thể, nhưng tên của property đó không phải là hằng số thời gian biên dịch mà bạn có thể nhập theo nghĩa đen trong code của mình. Thay vào đó, tên property bạn cần được lưu trữ trong một biến hoặc là giá trị trả về của một hàm mà bạn gọi. Bạn không thể sử dụng object literal cơ bản cho loại property này. Thay vào đó, bạn cần phải tạo một object và thêm các property mong muốn như một bước bổ sung
    
    ```jsx
    const PROPERTY_NAME = "p1";
    function computePropertyName() { return "p" + 2; }
    let o = {};
    o[PROPERTY_NAME] = 1;
    o[computePropertyName()] = 2;
    ```
    
- Việc thiết lập một object như thế này đơn giản hơn nhiều với một tính năng ES6 gọi là **thuộc tính được tính toán (computed properties)** cho phép bạn lấy dấu ngoặc vuông từ code trước đó và di chuyển chúng trực tiếp vào object literal
    
    ```jsx
    const PROPERTY_NAME = "p1";
    function computePropertyName() { return "p" + 2; }
    let p = {
      [PROPERTY_NAME]: 1,
      [computePropertyName()]: 2
    };
    p.p1 + p.p2 // => 3
    ```
    
- Với cú pháp mới này, dấu ngoặc vuông phân định một biểu thức Js tuỳ ý. Biểu thức đó được đánh giá và giá trị kết quả (được chuyển đổi thành chuỗi, nếu cần) được sử dụng làm tên property
- Một tình huống mà bạn có thể muốn sử dụng property được tính toán là khi bạn có một thư viện code Js dự kiến sẽ được chuyển đổi thành Object với một tập hợp các property cụ thể và tên các property đó được được định nghĩa là hằng số trong thư viện đó. Nếu bạn đang viết code để tạo ra các object sẽ được chuyển đến thư viện đó, bạn có thể mã hoá cứng các tên property, nhưng bạn sẽ có nguy cơ gặp lỗi nếu bạn nhập sai tên property ở bất kỳ đâu và bạn cũng có khả năng gặp sự cố không khớp phiên bản nếu một phiên bản mới của thư viện thay đổi tên property bắt buộc. Thay vào đó, bạn có thể thấy rằng việc sử dụng cú pháp được tính toán với các hằng số tên property được xác định bởi thư viện sẽ làm cho code của bạn mạnh mẽ hơn

### **6.10.3 Symbol làm tên thuộc tính (Symbols as Property Names)**

- Cú pháp property được tính toán cho phép một tính năng object literal rất quan trọng khác. Trong ES6 trở lên, tên property có thể là chuỗi hoặc Symbol. Nếu bạn gán một symbol cho một biến hoặc một hằng số, thì bạn có thể sử dụng symbol đó làm tên property bằng cách sử dụng cú pháp property được tính toán
    
    ```jsx
    const extension = Symbol("my extension symbol");
    let o = {
      [extension]: { /* dữ liệu mở rộng được lưu trữ trong đối tượng này */ }
    };
    o[extension].x = 0; // Điều này sẽ không xung đột với các thuộc tính khác của o
    ```
    
- Như đã giải thích trong 3.6, Symbol là giá trị mờ đục. Bạn không thể làm gì với chúng ngoài việc sử dụng chúng là tên property. Tuy nhiên, mọi Symbol đều khác với mọi Symbol khác, có nghĩa là Symbol rất tốt để tạo tên property duy nhất. Tạo Symbol mới bằng cách gọi hàm factory Symbol(). (Symbol là các giá trị nguyên thuỷ, không phải là object, vì vậy Symbol() không phải là hàm tạo mà bạn gọi với new). Giá trị được trả về bởi Symbol() không bằng bất kỳ Symbol hoặc giá trị nào khác. Bạn có thể chuyển một chuỗi cho Symbol() và chuỗi này được sử dụng khi Symbol của bạn được chuyển đổi thành chuỗi. Nhưng đây chỉ là một trợ giúp gỡ lỗi: hai Symbol được tạo với cùng mội đối số chuỗi vẫn khác nhau
- Mục đích của Symbol không phải là bảo mật, mà là để xác định một cơ chế bảo mật an toàn cho các object Js. Nếu bạn nhận được một object từ code bên thứ ba mà bạn không kiểm soát và cần thêm một số property của riêng bạn vào object đó nhưng muốn chắc chắn rằng các property của bạn sẽ không xung đột với bất kỳ property nào có thể tồn tại trên object, bạn có thể sử dụng an toàn Symbol làm tên property của mình. Nếu bạn làm điều này, bạn có thể tự tin rằng code của bên thứ 3 sẽ không vô tình thay đổi các property được đặt tên tượng trưng của bạn. (Tất nhiên, code bên thứ 3 có thể sử dụng `Object.getOwnPropertySymbols()` để khám phá các Symbol bạn đang sử dụng và sau đó có thể thay đổi hoặc xoá các property của bạn. Đây là lý do tại sao Symbol không phải cơ chế bảo mật

### **6.10.4 Toán tử Spread**

- Trong ES2018 trở lên, bạn có thể sao chép các property của một object hiện có vào một object mới bằng cách sử dụng `...` bên trong object literal
    
    ```jsx
    let position = { x: 0, y: 0 };
    let dimensions = { width: 100, height: 75 };
    let rect = { ...position, ...dimensions };
    rect.x + rect.y + rect.width + rect.height // => 175 
    ```
    
- Trong code này, các property của object `position` và `dimensions` được “lan truyền” vào object literal `rect` như thể chúng đã được viết theo nghĩa đen bên trong các dấu ngoặc nhọn đó. Lưu ý rằng cú pháp `...` này được gọi là toán tử spread nhưng không phải toán tử Js thực sự theo bất kỳ nghĩa nào. Thay vào đó, nó là cú pháp trường hợp đặc biệt chỉ khả dụng trong object literal. (Ba chấm được sử dụng cho các mục đích khác trong ngữ cảnh Js khác, nhưng object literal là ngữ cảnh duy nhất mà dấu ba chấm gây ra kiểu nội suy object này sang object khác)
- Nếu object được spread và object mà nó đang spread vào đều có một property cùng tên thì giá trị của property đó sẽ là property được  xuất hiện sau cùng
    
    ```jsx
    let o = { x: 1 };
    let p = { x: 0, ...o };
    p.x // => 1: giá trị từ đối tượng o ghi đè giá trị ban đầu
    let q = { ...o, x: 2 };
    q.x // => 2: giá trị 2 ghi đè giá trị trước đó từ o.
    ```
    
- Cũng lưu ý rằng toán tử spread chỉ spread các property riêng của một object không phải bất kỳ property kế thừa nào
    
    ```jsx
    let o = Object.create({x: 1}); // o kế thừa thuộc tính x
    let p = { ...o };
    p.x // => undefined
    ```
    
- Cuối cùng, điều đáng chú ý là, mặc dù toán tử spread chỉ là dấu `...` nhỏ trong code của bạn nhưng nó có thể thể hiện một số công việc khá đáng kể đối với trình thông dịch Js. Nếu một object có n property, thì quá trình spread các property đó vào một object khác có thể là một thao tác `O(n)`. Điều này có nghĩa là nếu bạn thấy mình đang sử dụng `...` trong một vòng lặp hoặc một hàm đệ quy như một cách để tích luỹ dữ liệu vào một object lớn, bạn có thể đang viết một thuật toán O(n2) kém hiệu quả sẽ không mở rộng tốt khi n lớn hơn

### **6.10.5 Phương thức viết tắt (Shorthand Methods)**

- Khi một hàm được định nghĩa là một property của một object, chúng ta gọi hàm đó là một `method` (chúng ta sẽ nói thêm nhiều điều về method trong Chương 8 và 9). Trước ES6, bạn sẽ định nghĩa một method trong object literal bằng cách sử dụng biểu thức định nghĩa hàm giống như bạn định nghĩa bất kỳ property nào của một object
    
    ```jsx
    let square = {
      area: function() { return this.side * this.side; },
      side: 10
    };
    square.area() // => 100
    ```
    
- Tuy nhiên, trong ES6, cú pháp object literal (và cả cú pháp định nghĩa class mà chúng ta sẽ thấy trong chương 9) được mở rộng để cho phép một lối tắt trong đó từ khoá function và dấu hai chấm bị bỏ qua, dẫn đến code sẽ như thế này
    
    ```jsx
    let square = {
      area() { return this.side * this.side; },
      side: 10
    };
    square.area() // => 100
    ```
    
- Cả hai dạng code đều tương đương: cả 2 đều thêm một property có tên là `area` vào object literal và cả 2 đều đặt giá trị của property đó thành hàm được chỉ định. Cú pháp viết tắt làm cho rõ ràng hơn bằng `area()` là một method chứ không phải là property như side
- Khi bạn viết một method bằng cú pháp viết tắt này, tên property có thể có bất kỳ dạng nào hợp pháp trong object literal: ngoài định danh Js thông thường như tên `area` ở trên, bạn cũng có thể sử dụng chuỗi ký tự và tên property được tính toán, có thể bao gồm property Symbol
    
    ```jsx
    const METHOD_NAME = "m";
    const symbol = Symbol();
    let weirdMethods = {
      "method With Spaces"(x) { return x + 1; },
      [METHOD_NAME](x) { return x + 2; },
      [symbol](x) { return x + 3; }
    };
    weirdMethods["method With Spaces"](1) // => 2
    weirdMethods[METHOD_NAME](1) // => 3
    weirdMethods[symbol](1) // => 4
    ```
    
- Việc sử dụng Symbol làm tên method không kỳ lạ như vẻ bề ngoài của nó. Để làm cho một object có thể lặp lại (vì vậy nó có thể được sử dụng với vòng lặp for of), bạn phải định nghĩa một method có tên tượng trưng `Symbol.iterator` và có các ví dụ về cách thực hiện chính xác trong chương 12

### **6.10.6 Thuộc tính Getter và Setter (Property Getters and Setters)**

- Tất cả các object property mà chúng ta thảo luận cho đến nay cho đến giờ đều là các property dữ liệu có tên và giá trị thông thường. Js cũng hỗ trợ `accessor properties`, không có một giá trị duy nhất mà thay vào đó có một hoặc 2 method accessor: getter và/hoặc setter
- Khi một chương trình truy vấn giá trị của một property accessor, Js sẽ gọi method getter (không truyền đối số). Giá trị trả về của method này trở thành giá trị của biểu thức truy cập property
- Khi một chương trình đặt giá trị của một thuộc tính accessor, Js sẽ gọi method setter, truyền giá trị của vế phải phép gán. Method này chịu trách nhiệm “thiết lập” theo một nghĩa nào đó, giá trị property. Giá trị trả về của method setter bị bỏ qua
- Nếu một property có cả method setter và getter, thì đó là property đọc/ghi. Nếu nó chỉ có một method getter, thì đó là thuộc tính chỉ đọc. Và nếu nó chỉ có một method setter, thì đó là một property chỉ ghi (điều không thể xảy ra với các thuộc tính dữ liệu) và nỗ lực đọc của nó luôn đánh giá thành undefined
- Thuộc tính accessor có thể được định nghĩa với phần mở rộng cho cú pháp object literal (không giống như các phần mở rộng ES6 khác mà chúng ta đã thấy ở đây, getter và setter đã được giới thiệu trong ES5)
    
    ```jsx
    let o = {
      // Một thuộc tính dữ liệu thông thường
      dataProp: value,
      // Một thuộc tính accessor được định nghĩa là một cặp hàm.
      get accessorProp() { return this.dataProp; },
      set accessorProp(value) { this.dataProp = value; }
    };
    ```
    
- Property accessor được định nghĩa là một hoặc 2 method có tên giống với tên property. Chúng trông giống như các method thông thường được định nghĩa bằng cách sử dụng viết tắt ES6 ngoại trừ việc cách định nghĩa getter và setter được thêm tiền tố `get` và `set`. (Trong ES6, bạn cũng có thể sử dụng tên property được tính toán khi định nghĩa getter và setter. Chỉ cần thay thế tên property sau `get` và `set` bằng một biểu thức trong dấu ngoặc vuông)
- Các method accessor được định nghĩa ở trên chỉ đơn giản là lấy và đặt giá trị của một property data và không có lý do gì để property accessor hơn property data. Nhưng như một ví dụ thú vị hơn, hãy xem xét object sau đây đại diện cho một điểm Descartes 2D. Nó có các property data thông thường để biểu diễn các toạ độ x và y của điểm và nó không có các property accessor cung cấp toạ độ cực tương đương của điểm
    
    ```jsx
    let p = {
      // x và y là các thuộc tính dữ liệu đọc/ghi thông thường.
      x: 1.0,
      y: 1.0,
      // r là thuộc tính accessor đọc/ghi với getter và setter.
      // Đừng quên đặt dấu phẩy sau các phương thức accessor.
      get r() { return Math.hypot(this.x, this.y); },
      set r(newvalue) {
        let oldvalue = Math.hypot(this.x, this.y);
        let ratio = newvalue/oldvalue;
        this.x *= ratio;
        this.y *= ratio;
      },
      // theta là thuộc tính accessor chỉ đọc với getter only.
      get theta() { return Math.atan2(this.y, this.x); }
    };
    p.r // => Math.SQRT2
    p.theta // => Math.PI / 4
    ```
    
- Lưu ý việc sử dụng từ khoá `this` trong getter và setter trong ví dụ này. Js gọi các hàm này như các method của object mà chúng định nghĩa, có nghĩa là phần thân hàm, this tham chiếu đến object point `p`. Vì vậy, method getter cho property `r` có thể tham chiếu  đến các property x và y dưới dạng this.x và this.y. Method và từ khoá `this` được đề cập chi tiết hơn trong 8.2.2
- Các property accessor được kế thừa, giống như các data property, vì bạn có thể sử dụng object `p` được định nghĩa ở trên làm prototype cho các điểm khác. Bạn có thể cung cấp cho các object mới các property x và y của riêng chúng và chúng sẽ kế thừa  các property `r` và  `theta`
    
    ```jsx
    let q = Object.create(p); // Một đối tượng mới kế thừa getter và setter
    q.x = 3; q.y = 4; // Tạo các thuộc tính dữ liệu riêng của q
    q.r // => 5: các thuộc tính accessor được kế thừa hoạt động
    q.theta // => Math.atan2(4, 3)
    ```
    
- Code trên sử dụng property accessor để định nghĩa API cung cấp hai biểu diễn (toạ độ Descartes và toạ độ cực) của một tập hợp dữ liệu duy nhất. Các lý do khác để sử dụng một property accessor bao gồm kiểm tra tính hợp lệ của các lần ghi property và trả về giá trị khác nhau trên mỗi lần đọc property
    
    ```jsx
    // Đối tượng này tạo ra các số sê-ri tăng dần nghiêm ngặt
    const serialnum = {
      // Thuộc tính dữ liệu này chứa số sê-ri tiếp theo.
      // _ trong tên thuộc tính gợi ý rằng nó chỉ dành cho sử dụng nội bộ.
      _n: 0,
      // Trả về giá trị hiện tại và tăng nó
      get next() { return this._n++; },
      // Đặt một giá trị mới của n, nhưng chỉ khi nó lớn hơn hiện tại
      set next(n) {
        if (n > this._n) this._n = n;
        else throw new Error("serial number chỉ có thể được đặt thành một giá trị lớn hơn");
      }
    };
    serialnum.next = 10; // Đặt số sê-ri bắt đầu
    serialnum.next // => 10
    serialnum.next // => 11: giá trị khác nhau mỗi khi chúng ta nhận được next
    ```
    
- Cuối cùng, đây là một ví dụ nữa sử dụng method getter để triển khai property với hành vi “ma thuật”
    
    ```jsx
    // Đối tượng này có các thuộc tính accessor trả về các số ngẫu nhiên.
    // Ví dụ: biểu thức "random.octet", tạo ra một số ngẫu nhiên
    // từ 0 đến 255 mỗi khi nó được đánh giá.
    const random = {
      get octet() { return Math.floor(Math.random()*256); },
      get uint16() { return Math.floor(Math.random()*65536); },
      get int16() { return Math.floor(Math.random()*65536)-32768; }
    };
    ```
    

## Summary

- Chương này đã ghi lại các object Js rất chi tiết, bao gồm các chủ đề
    - Thuật ngữ object cơ bản, bao gồm các thuật ngữ như `enumerable` và `own property`
    - Cú pháp object literal, bao gồm nhiều tính năng mới trong ES6 trở lên
    - Cách đọc, ghi, xoá, liệt kê và kiểm tra sự hiện diện của các property của một object
    - Cách kế thừa dựa trên prototype (prototype-based inheritance) hoạt động trong Js và cách tạo một object kế thừa từ một object khác với `Object.create()`
    - Cách sao chép từ object này sang object khác với `Object.assign()`
- Tất cả các giá trị Js không phải là giá trị nguyên thuỷ đều là object. Điều này bao gồm cả mảng và hàm, là chủ đề của 2 chương tiếp theo
- Lưu ý:
    - Hầu hết các object đều có prototype nhưng hầu hết không có property có tên `prototype`. Kế thừa JS hoạt động ngay cả khi bạn không thể truy cập trực tiếp vào object prototype. Nhưng hãy xem 14.3 nếu bạn muốn tìm hiểu cách thực hiện điều đó

