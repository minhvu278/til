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
