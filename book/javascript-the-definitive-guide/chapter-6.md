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
