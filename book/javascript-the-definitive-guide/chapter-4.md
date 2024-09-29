# Expressions and Operators
- Chương này ghi lại các biểu thức Js và các toán tử mà nhiều biểu thức đó được xây dựng. Biểu thức là một cụm từ JS có thể được ước lượng để tạo ra một giá trị. Một hằng số được nhúng trực tiếp vào chương trình của bạn là 1 biểu thức rất đơn giản. Tên biến cũng là một biểu thức đơn giản được ước lượng thành bất kỳ giá trị nào đã được gán cho biến đó. Các biểu thức phức tạp được xây dựng từ các biểu thức phức tạp hơn
- Ví dụ: Một biểu thức truy cập array bao gồm biểu thức ước lượng thành 1 array theo sau là dấu ngoặc vuông mở, một biểu thức ước lượng thành một số nguyên và dấu ngoặc vuông đóng. Biểu thức mới, phức tạp hơn này ước lượng thành giá trị được lưu trữ tại index đã được chỉ định. Tương tự, một biểu thức gọi hàm bao gồm một biểu thức ước lượng thành một object hàm và không hoặc nhiều biể thức bổ sung được sử dụng làm đối số cho hàm
- Cách phổ biến nhất để xây dựng một biểu thức phức tạp từ các biểu thức đơn giản hơn là sử dụng toán tử. Toán tử kết hợp các giá trị của các toán hạng của nó (thường là hai trong số chúng) theo 1 cách nào đó và ước lượng thành một giá trị mới. Toán tử `*` là một ví dụ đơn giản. Biểu thức `x * y`  ước lượng thành tích của các giá trị biểu thức x và y. Để đơn giản, đôi khi chúng ta nói rằng một toán tử trả về một giá trị thay vì “ước lượng thành” một giá trị
- Chương này ghi lại tất cả các toán tử Js và nó cũng giải thích các biểu thức (chẳng hạn như lập index array và gọi function) không sử dụng toán tử. Nếu bạn đã biết một ngôn ngữ lập trình khác sử dụng cú pháp kiểu C, bạn sẽ thấy rằng cú pháp của hầu hết các biểu thức và toán tử của Js đã quen thuộc với bạn

## 4.1 Primary Expressions

- Các biểu thức đơn giản nhất, được gọi là primary expression, là những biểu thức độc lập - chúng không bao gồm bất kỳ biểu thức đơn giản nào khác. primary expression trong Js là các giá trị hằng số hoặc literal, một số từ khoá ngôn ngữ nhất định và các tham chiếu biến
- Literal là các giá trị hằng số được nhúng trực tiếp vào chương trình của bạn. Chúng trông giống như thế này
    
    ```jsx
    1.23 // Một literal số
    "hello" // Một literal chuỗi
    /pattern/ // Một literal biểu thức chính quy 
    ```
    
- Cú pháp Js cho literal số đã được đề cập trong 3.2. Literal chuỗi đã được ghi lại trong 3.3. Cú pháp literal biểu thức chính quy đã được giới thiệu trong 3.3.5 và sẽ được ghi lại chi tiết trong 11.3
- Một số từ khoá dành riêng của Js là primary expression
    
    ```jsx
    true // Ước lượng thành giá trị boolean true
    false // Ước lượng thành giá trị boolean false
    null // Ước lượng thành giá trị null
    this // Ước lượng thành object "hiện tại" 
    ```
    
- Chúng ta đã tìm hiểu về true, false và null trong 3.4 và 3.5. Không giống như các từ khoá khác, `this` không phải là một hằng sô - nó ước lượng thành các giá trị khác nhau ở các vị trí khác nhau trong chương trình. Từ khoá `this` được sử dụng trong lập trình hướng đối tượng. Trong phần thân của một phương thức, `this` ước lượng thành object mà phương thức đó gọi trên đó. Xem 4.5, Chương 8 (đặc biệt là 8.2.2) và chương 9 để biết thêm điều này
- Cuối cùng, loại biểu thức chính thứ 3 là tham chiếu đến 1 biến, hẳng số hoặc thuộc tính global object
    
    ```jsx
    i // Ước lượng thành giá trị của biến i.
    sum // Ước lượng thành giá trị của biến sum.
    undefined // Giá trị của thuộc tính "undefined" của object toàn cục
    ```
    
- Khi bất kỳ định danh nào xuất hiện đơn lẻ trong 1 chương trình, Js giả định rằng đó là một biến hoặc hằng số hoặc thuộc tính của global object và tra cứu giá trị của nó. Nếu không có biến nào có tên đó tồn tại, việc cố gắng ước lượng 1 biến không tồn tại sẽ ném ra `ReferenceError` thay thế

## 4.2 Object and Array Initializers

- Bộ khởi tạo object và array là các biểu thức có giá trị là một object hoặc array mới được tạo. Các biểu thức khởi tạo này đôi khi được gọi là literal object và literal array. Tuy nhiên không giống như literal thực, chúng không phải biểu thức chính, bởi vì chúng bao gồm một số biểu thức con chỉ định các giá trị thuộc tính và phần tử
- Bộ khởi tạo array có cú pháp đơn giản hơn 1 chút và chúng ta sẽ bắt đầu với những bộ khởi tạo đó
- Bộ khởi tạo array là một danh sách các biểu thức được phân tách bằng dấu phẩy chứa trong dấu ngoặc vuông. Giá trị của bộ khởi tạo array là một array mới được tạo. Các phần tử của array mới này được khởi tạo thành các giá trị của các biểu thức được phân tách bởi dấu phẩy
    
    ```jsx
    [] // Một array rỗng: không có biểu thức nào trong ngoặc vuông có nghĩa là không có phần tử
    [1+2,3+4] // Một array 2 phần tử. Phần tử đầu tiên là 3, phần tử thứ hai là 7 
    ```
    
- Các biểu thức phần tử trong bộ khởi tạo array có thể là bộ khởi tạo array, có nghĩa là các biểu thức này có thể tạo các array lồng nhau
    
    ```jsx
    let matrix = [[1,2,3], [4,5,6], [7,8,9]]; 
    ```
    
- Các biểu thức phần tử trong bộ khởi tạo array được ước lượng mỗi khi bộ khởi tạo array được ước lượng. Điều này có nghĩa là giá trị của biểu thức khởi tạo array có thể khác nhau mỗi khi nó được ước lượng
- Các phần tử undefined có thể được bao gồm trong 1 literal array bằng cách chỉ cần bỏ qua một giá trị giữa các dấu phẩy. Ví dụ:
    
    ```jsx
    let sparseArray = [1,,,,5]; 
    ```
    
- Một dấu phẩy ở cuối được phép sau biểu thức cuối cùng trong bộ khởi tạo array và không tạo phần tử undefined. Tuy nhiên, bất kỳ biểu thức truy cập array nào cho một index của biểu thức cuối cùng nhất thiết sẽ ước lượng thành undefined
- Biểu thức khởi tạo object giống như biểu thức khởi tạo array, nhưng dấu `[` được thay thế bằng `{` và mỗi biểu thức con được thêm tiền tố bằng tên property và dấu :
    
    ```jsx
    let p = { x: 2.3, y: -1.2 }; // Một object có 2 thuộc tính
    let q = {}; // Một object rỗng không có thuộc tính
    q.x = 2.3; q.y = -1.2; // Bây giờ q có cùng thuộc tính với p 
    ```
    
- Trong ES6, literal object có cú pháp phong phú hơn nhiều về tính năng (chi tiết trong 6.10). Literal object có thể lồng nhau
    
    ```jsx
    let rectangle = {
      upperLeft: { x: 2, y: 2 },
      lowerRight: { x: 4, y: 5 }
    }; 
    ```
    
- Chúng ta sẽ thấy bộ khởi tạo object và array trong chương 6 và 7

## 4.3 Function Definition Expressions

- Biểu thức định nghĩa function định nghĩa một Js và giá trị của biểu thức đó là hàm mới được định nghĩa. Theo một nghĩa nào đó, biểu thức định nghĩa hàm là một “literal hàm” giống như cách bộ khởi tạo object là một “literal object”. Biểu thức định nghĩa hàm thường bao gồm từ khoá `function` theo sau đó là một danh sách không hoặc nhiều định danh được phân tách bằng dấu phẩy (tên tham số) trong dấu ngoặc đơn và một block code Js (phần thân hàm) trong dấu ngoặc nhọn
    
    ```jsx
    // Hàm này trả về bình phương của giá trị được truyền cho nó.
    let square = function(x) { return x * x; }; 
    ```
    
- Biểu thức định nghĩa hàm cũng có thể bao gồm một tên cho hàm. Các hàm cũng có thể được định nghĩa bằng cách sử dụng câu lệnh hàm thay vì biểu thức hàm. Và trong ES6 trở về sau, các biểu thức hàm có thể sử dụng cú pháp “arrow” mới, gọn nhẹ
- Chi tiết đầy đủ về định nghĩa hàm có trong chương 8

## 4.4 Property Access Expressions

- Biểu thức truy cập thuộc tính ước lượng thành giá trị của một thuộc tính object hoặc 1 phần tử array. Js định nghĩa 2 cú pháp để truy cập thuộc tính
    
    ```jsx
    expression . identifier
    expression [ expression ]
    
    biểu_thức . định_danh
    biểu_thức [ biểu_thức ]
    ```
    
- Khi truy cập thuộc tính đầu tiên là một biểu thức theo sau là dấu chấm và một định danh. Biểu thức chỉ định object và định danh chỉ định tên thuộc tính mong muốn. Kiểu truy cập thuộc tính thứ 2 theo sau biểu thức đầu tiên (object hoặc array) với một biểu thức khác trong dấu ngoặc vuông. Biểu thức thứ 2 này chỉ định tên của thuộc tính mong muốn hoặc index của phần tử array mong muốn
    
    ```jsx
    let o = {x: 1, y: {z: 3}}; // Một object ví dụ
    let a = [o, 4, [5, 6]]; // Một array ví dụ chứa object
    
    o.x // => 1: thuộc tính x của biểu thức o
    o.y.z // => 3: thuộc tính z của biểu thức o.y
    o["x"] // => 1: thuộc tính x của object o
    a[1] // => 4: phần tử tại chỉ mục 1 của biểu thức a
    a[2]["1"] // => 6: phần tử tại chỉ mục 1 của biểu thức a[2]
    a[0].x // => 1: thuộc tính x của biểu thức a[0] 
    ```
    
- Với một trong 2 loại biểu thức truy cập thuộc tính, biểu thức trước dấu `.` hoặc `[` được ước lượng trước. Nếu giá trị là null hoặc undefined, biểu thức sẽ ném ra TypeError, vì đây là 2 giá trị Js không thể có property
- Nếu biểu thức object được theo sau bởi một dấu chấm và một định danh, giá trị của thuộc tính được đặt tên bởi định danh đó sẽ được tra cứu và trở thành giá trị chung của biểu thức
- Nếu biểu thức object được theo sau bởi một biểu thức khác trong dấu ngoặc vuông, thì biểu thức thứ 2 đó sẽ được ước lượng và chuyển đổi thành một chuỗi. Giá trị chung của biểu thức  sau đó là giá trị của một thuộc tính được đặt tên bởi chuỗi đó
- Trong cả 2 trường hợp, nếu thuộc tính được đặt tên không tồn tại, thì giá trị của biểu thức truy cập thuộc tính là undefined
- Cú pháp `.identify` là đơn giản hơn trong hai tuỳ chọn truy cập thuộc tính, nhưng lưu ý rằng nó chỉ có thể được sử dụng khi thuộc tính của bạn muốn truy cập có tên là một định danh hợp lệ và khi bạn biết tên khi bạn viết chương trình. Nếu tên thuộc tính bao gồm khoảng trắng hoặc dấu câu hoặc khi nó là một số (đối với array), bạn phải sử dụng ký hiệu dấu ngoặc vuông
- Dấu ngoặc vuông cũng được sử dụng khi tên thuộc tính không tĩnh mà bản thân nó là kết quả của một phép tính (xem 6.3.1 để biết ví dụ)
- Object và thuộc tính của chung được đề cập chi tiết trong chương 6 và array và các phần tử của chúng trong chương 7

### 4.4.1 Conditional Property Access

- ES2020 thêm 2 loại biểu thức truy cập thuộc tính mới
    
    ```jsx
    expression ?. identifier
    expression ?.[ expression ]
    
    biểu_thức ?. định_danh
    biểu_thức ?.[ biểu_thức ] 
    ```
    
- Trong Js, các giá trị null và undefined là 2 giá trị duy nhất không có properties. Trong một biểu thức truy cập thuộc tính thông thường sử dụng `.` hoặc `[]`, bạn sẽ nhận được TypeError nếu biểu thức ở bên trái ước lượng thành null hoặc undefined. Bạn có thể sử dụng cú pháp `?.` và `?.[]` để bảo vệ khỏi các lỗi thuộc loại này
- Hãy xem xét biểu thức `a?.b`. Nếu `a` là null hoặc undefined, thì biểu thức sẽ ước lượng thành undefined mà không cần bất kỳ nỗ lực nào để truy cập property `b`. Nếu `a` là một số giá trị khác, thì `a?.b` ước lượng thành bất kỳ giá trị nào mà `a.b` sẽ ước lượng (và nếu `a` không có property có tên `b`, thì giá trị sẽ lại là undefined)
- Dạng biểu thức truy cập thuộc tính này đôi khi được gọi là “chuỗi tuỳ chọn” bởi vì nó cũng hoạt động cho các biểu thức truy cập thuộc tính “chuỗi” dài hơn như biểu thức này
    
    ```jsx
    let a = { b: null };
    a.b?.c.d // => undefined 
    ```
    
- `a` là một object, vì vậy `a.b` là một biểu thức truy cập property hợp lệ. Nhưng giá trị của `a.b` là null, vì vậy `a.b.c` sẽ ném ra TypeError. Bằng cách sử dụng `?.` thay vì `.`, chúng ta tránh được TypeError và `a.b?.c` ước lượng thành undefined
- Điều này có nghĩa là `(a.b?.c).d` sẽ ném ra TypeError, bởi vì biểu thức đó cố gắng truy cập một property của giá trị undefined
- Nhưng - và đây là một phần quan trọng của “chuỗi tuỳ chọn” - `a.b?.c.d` (không có dâu ngoặc đơn) chỉ đơn giản là ước lượng thành undefined và không ném ra lỗi
- Điều này là do truy cập thuộc tính bằng `?.` là “ngắn mạch”: Nếu biểu thức con ở bên trái của `?.` ước lượng thành null hoặc undefined, thì toàn bộ biểu thức ngay lập tức ước lượng thành undefined mà không cần bất kỳ nỗ lực truy cập thuộc tính nào nữa
- Tất nhiên nếu `a.b` là 1 object và nếu object đó không có property có tên là `c`, thì `a.b?.c.d` sẽ ném ra TypeError và chúng ta sẽ muốn sử dụng một truy cập thuộc tính có điều kiện khác
    
    ```jsx
    let a = { b: {} };
    a.b?.c?.d // => undefined 
    ```
    
- Truy cập thuộc tính có điều kiện cũng có thể thực hiện được bằng cách sử dụng `?.[]` thay vì `[]`. Trong biểu thức `a?.[b].[c]` nếu giá trị của `a` là null hoặc undefined, thì toàn bộ biểu thức ngay lập tức ước lượng thành undefined và các biểu thức con b và c thậm chí không bao giờ được ước lượng
- Nếu một trong 2 biểu thức đó có tác dụng phụ, tác dụng phụ sẽ không xảy ra nếu a không được xác định
    
    ```jsx
    let a; // Ôi, chúng ta quên khởi tạo biến này!
    let index = 0;
    
    try {
      a[index++]; // Ném ra TypeError
    } catch(e) {
      index // => 1: tăng xảy ra trước khi TypeError bị ném ra
    }
    
    a?.[index++] // => undefined: bởi vì a là undefined
    index // => 1: không được tăng lên bởi vì ?.[] ngắn mạch
    a[index++] // !TypeError: không thể lập chỉ mục undefined. 
    ```
    
- Truy cập property với `?.` và `?.[]` là một trong những tính năng mới nhất của Js. Tính đến đầu năm 2020, cú pháp mới này được hỗ trợ trong các phiên bản hiện tại hoặc beta của hầu hết các trình duyệt chính

## 4.5 Invocation Expressions (Biểu thức gọi)

- Là cú pháp của Js để gọi (hoặc thực thi) một hàm hoặc một method. Nó bắt đầu bằng một biểu thức hàm xác định hàm được gọi. Biểu thức hàm được theo sau bởi dấu ngoặc đơn mở, danh sách không hoặc nhiều biểu thức đối số được phân tách bằng dấu phẩy và dấu ngoặc đơn đóng
    
    ```jsx
    f(0) // f là biểu thức hàm; 0 là biểu thức đối số.
    Math.max(x,y,z) // Math.max là hàm; x, y và z là các đối số.
    a.sort() // a.sort là hàm; không có đối số. 
    ```
    
- Khi một biểu thức gọi được ước lượng, biểu thức hàm được ước lượng trước, sau đó các biểu thức đối số được ước lượng để tạo ra một danh sách các giá trị số. Nếu giá trị của biểu thức hàm không phải là hàm, TypeError sẽ bị ném ra. Tiếp theo, các giá trị đối số được gán, theo thứ tự, cho các tên tham số được chỉ định khi hàm được định nghĩa và sau đó phần thân của hàm được thực thi
- Nếu hàm sử dụng câu lệnh `return` để trả về 1 giá trị, thì giá trị đó sẽ trở thành giá trị của biểu thức gọi. Nếu không, giá trị của biểu thức gọi là undefined
- Chi tiết đầy đủ về gọi hàm, bao gồm giải thích điều gì xảy ra khi số lượng biểu thức đối số không khớp với số lượng tham số trong định nghĩa hàm, có trong chương 8
- Mọi biểu thức đều bao gồm một cặp dấu ngoặc đơn và một biểu thức trước dấu ngoặc đơn mở. Nếu biểu thức đó là biểu thức truy cập thuộc tính, thì lời gọi được gọi là `gọi phương thức`. Trong `gọi phương thức`, object hoặc array là chủ thể của truy cập thuộc tính sẽ trở thành giá trị của từ khoá `this` trong khi phần thân của hàm đang được thực thi
- Điều này cho phép một mô hình OOP trong đó các hàm (mà chúng ta gọi là “method” khi được sử dụng theo cách này) hoạt động trên object mà chúng là một phần. Xem chi tiết ở chương 9

### 4.5.1 Conditional Invocation

- Trong ES2020, bạn cũng có thể gọi một hàm bằng cách sử dụng `?.()` thay vì `()
- Thông thường khi bạn gọi 1 hàm, nếu biểu thức ở bên trái dấu ngoặc đơn là null hoặc undefined hoặc bất kỳ hàm không nào khác, thì TypeError sẽ bị ném ra. Với cú pháp gọi `?.()` mới, nếu biểu thức ở bên trái của `?.` ước lượng thành null hoặc undefined, thì toàn bộ biểu thức gọi sẽ được ước lượng thành undefined và không có ngoại lệ được ném ra
- `Object Array` có một method `sort()` có thể tuỳ chọn được truyền một đối số hàm xác định thứ tự sắp xếp mong muốn cho các phần tử array. Trước ES2020, nếu bạn muốn viết 1 method như `sort()` nhận 1 đối số hàm tuỳ chọn, bạn thường sẽ sử dụng câu lệnh if để kiểm tra xem đối số hàm đã được xác định hay chưa trước khi gọi nó trong phần thân của if
    
    ```jsx
    function square(x, log) { // Đối số thứ hai là một hàm tùy chọn
      if (log) { // Nếu hàm tùy chọn được truyền vào
        log(x); // Gọi nó
      }
      return x * x; // Trả về bình phương của đối số
    } 
    ```
    
- Tuy nhiên, với cú pháp gọi có điều kiện này của ES2020, bạn có thể chỉ cần viết lời gọi hàm bằng cách sử dụng `?.()`, biết rằng lời gọi sẽ chỉ xảy ra nếu thực sự có 1 giá trị được gọi
    
    ```jsx
    function square(x, log) { // Đối số thứ hai là một hàm tùy chọn
      log?.(x); // Gọi hàm nếu có
      return x * x; // Trả về bình phương của đối số
    } 
    ```
    
- Tuy nhiên, lưu ý rằng `?.()` chỉ kiểm tra xem phía bên trái có phải là null hoặc undefined hay không. Nó không xác minh rằng giá trị thực sự là một hàm. Vì vậy, hàm `square()` trong ví dụ này vẫn sẽ ném ra ngoại lệ nếu bạn truyền 2 số cho nó chẳng hạn
- Giống như các biểu thức truy cập thuộc tính có điều kiện (4.4.1), gọi hàm với `?.()` là ngắn mạch: nếu giá trị ở bên trái của `?.` là null hoặc undefined thì không có biểu thức đối số nào trong dấu ngoặc đơn được ước lượng
    
    ```jsx
    let f = null, x = 0;
    
    try {
      f(x++); // Ném ra TypeError vì f là null
    } catch(e) {
      x // => 1: x được tăng lên trước khi ngoại lệ bị ném ra
    }
    
    f?.(x++) // => undefined: f là null, nhưng không có ngoại lệ nào bị ném ra
    x // => 1: tăng bị bỏ qua do ngắn mạch 
    ```
    
- Biểu thức có điều kiện với `?.()` hoạt động tốt với các method cũng như đối với các function. Nhưng vì gọi method cũng liên quan đến việc truy cập property nên đáng dành một chút thời gian để đảm bảo rằng bạn hiểu sự khác biệt giữa các biểu thức sau
    
    ```jsx
    o.m() // Truy cập thuộc tính thông thường, gọi thông thường
    o?.m() // Truy cập thuộc tính có điều kiện, gọi thông thường
    o.m?.() // Truy cập thuộc tính thông thường, gọi có điều kiện 
    ```
    
- Trong biểu thức đầu tiên, `o` phải là một object có property `m` và giá trị của property đó phải là một hàm. Trong biểu thức thứ 2, `o` nếu là null hoặc undefined, thì biểu thức sẽ được ước lượng thành undefined, nhưng nếu `o` có bất kỳ giá trị nào khác, thì nó phải có property `m` có giá trị là một hàm. Và trong biểu thức thứ 3, `o` không được là null hoặc undefined. Nếu nó không có property `m` hoặc giá trị property đó là null thì toàn bộ biểu thức được ước lượng thành undefined
- Gọi có điều kiện với `?.()` là một trong những tính năng mới nhất của Js. Kể từ những tháng đầu năm 2020, cú pháp này mới được hỗ trợ trong các phiên bản hiện tại hoặc beta của hầu hết các trình duyệt chính

## 4.6 **Object Creation Expressions**

- Một biểu thức tạo đối tượng sẽ tạo ra đối tượng mới và gọi 1 hàm (gọi là constructor - hàm tạo) để khởi tạo các thuộc tính của object đó
- Biểu thức tạo object giống như biểu thức gọi hàm, ngoại trừ việc chúng thêm từ khoá `new` vào trước
    
    ```jsx
    new Object()
    new Point(2,3) 
    ```
    
- Nếu không có tham số được truyền vào trong hàm tạo trong biểu thức tạo object , cặp ngoặc đơn rỗng có thể được bỏ qua
    
    ```jsx
    new Object
    new Date 
    ```
    
- Giá trị của một biểu thức tạo object mà 1 object mới được tạo ra
- constructor được giải thích trong chương 9

## 4.7 **Operator Overview**

- Toán tử được sử dụng cho các biểu thức số học, so sánh, logic. gán và nhiều hơn nữa trong Js
- Lưu ý rẳng hầu hết các toán tử được biểu diễn bằng ký tự dấu câu như `+` và `=` . Tuy nhiên, một số toán tử được biểu diễn bằng từ khoá như `delete` hoặc `instanceof` . Các toán tử từ khoá là các toán tử thông thường, giống như các toán tử được biểu diễn bằng dấu chấm câu; chúng chỉ đơn giản là có cú pháp dài hơn
- Bảng bên dưới được sắp xếp theo thứ tự ưu tiên của toán tử. Các toán tử được liệt kê trước có độ ưu tiên cao hơn các toán tử được liệt kê sau. Các toán tử được phân tách bằng một đường gạch ngang có các mức độ ưu tiên khác nhau. Cột có label `A` cho biết tính kết hợp của toán tử, có thể là `L` (trái sang phải) hoặc `R` (phải sang trái), và cột `N` chỉ định số lượng toán hạng. Cột có label `Types` liệt kê các loại toán hạng dự kiến và (sau ký hiệu `->`) loại kết quả cho toán tử. Các tiểu mục sau bảng giải thích các khái niệm về độ ưu tiên, tính kết hợp và loại toán hạng. Các toán tử được ghi lại riêng lẻ sau phần thảo luận đó
    
    ```jsx
    Bảng 4-1. Toán tử JavaScript
    
    Toán tử	Thao tác	A	N	Loại
    ++	Tăng trước hoặc tăng sau	R	1	lval→num
    --	Giảm trước hoặc giảm sau	R	1	lval→num
    -	Phủ định số	R	1	num→num
    +	Chuyển đổi sang số	R	1	any→num
    ~	Đảo bit	R	1	int→int
    !	Đảo giá trị boolean	R	1	bool→bool
    delete	Xóa một thuộc tính	R	1	lval→bool
    typeof	Xác định loại toán hạng	R	1	any→str
    void	Trả về giá trị undefined	R	1	any→undef
    **	Lũy thừa	R	2	num,num→num
    *, /, %	Nhân, chia, chia lấy dư	L	2	num,num→num
    +, -	Cộng, trừ	L	2	num,num→num
    +	Nối chuỗi	L	2	str,str→str
    <<	Dịch trái	L	2	int,int→int
    >>	Dịch phải với mở rộng dấu	L	2	int,int→int
    >>>	Dịch phải với mở rộng không	L	2	int,int→int
    <, <=, >, >=	So sánh theo thứ tự số	L	2	num,num→bool
    <, <=, >, >=	So sánh theo thứ tự bảng chữ cái	L	2	str,str→bool
    instanceof	Kiểm tra lớp đối tượng	L	2	obj,func→bool
    in	Kiểm tra xem thuộc tính có tồn tại không	L	2	any,obj→bool
    ==	Kiểm tra bằng không nghiêm ngặt	L	2	any,any→bool
    !=	Kiểm tra không bằng không nghiêm ngặt	L	2	any,any→bool
    ===	Kiểm tra bằng nghiêm ngặt	L	2	any,any→bool
    !==	Kiểm tra không bằng nghiêm ngặt	L	2	any,any→bool
    &	Tính toán bitwise AND	L	2	int,int→int
    ^	Tính toán bitwise XOR	L	2	int,int→int
    `	`	Tính toán bitwise OR	L	2
    &&	Tính toán logical AND	L	2	any,any→any
    `		`	Tính toán logical OR	L
    ??	Chọn toán hạng được xác định đầu tiên	L	2	any,any→any
    ?:	Chọn toán hạng thứ 2 hoặc thứ 3	R	3	bool,any,any→any
    =	Gán cho một biến hoặc thuộc tính	R	2	lval,any→any
    **=, *=, /=, %=, +=, -=, &=, ^=, `	=,<<=,>>=,>>>=`	Thực hiện phép toán và gán	R	2
    ,	Loại bỏ toán hạng thứ 1, trả về toán hạng thứ 2	L	2
    ```
    

### 4.7.1 **Number of Operands**

- Toán tử có thể được phân loại dựa trên số lượng toán hạng mà chúng mong đợi (arity của chúng). Hầu hết các toán tử Js, như toán tử `*` là các toán tử nhị phân kết hợp hai biểu thức thành một biểu thức phức tạp hơn
- Js cũng hỗ trợ một số toán tử đơn nhất, chuyển đổi một biểu thức thành một biểu thức phức tạp hơn. Toán tử `-` trong biểu thức `-x` là toán tử đơn nhất thực hiện phép toán phủ định trên toán hạng `x`. Cuối cùng, Js hỗ trợ một toán tử 3 ngôi, toán tử điều kiện `?:`, kết hợp 3 biểu thức thành một biểu thức

### 4.7.2 **Operand and Result Type**

- Một số toán tử hoạt động trên các giá trị của bất kỳ loại nào, nhưng hầu hết mong đợi toán hạng của chúng thuộc một loại cụ thể và hầu hết các toán tử trả về (hoặc đánh giá thành) một giá trị thuộc một loại cụ thể. Cột `Types` trong bảng trên chỉ định loại toán hạng (trước mũi tên) và kết quả (sau mũi tên) cho các toán tử
- Các toán tử Js thường chuyển đổi loại (3.9) của toán hạng khi cần thiết. Toán tử `*` mong đợi toán tử hạng số, nhưng biểu thức `"3" * "5"` là hợp lệ vì Js có thể chuyển đổi toán hạng thành số. Giá trị của biểu thức này là 15, tất nhiên không phải là chuỗi “15”. Cũng nên nhớ rằng mọi giá trị Js đều là truethy hoặc “falsy”, vì vậy các toán tử mong đợi toán hạng boolean sẽ hoạt động với toán hạng của bất kỳ loại nào
- Một số toán tử hoạt động khác nhau phụ thuộc vào loại toán hạng được sử dụng với chúng. Đáng chú ý nhất, toán tử `+` cộng các toán hạng số nhưng nối các toán hạng chuỗi. Tương tự, các toán tử so sánh như `<` thực hiện so sánh theo thứ tự số hoặc bảng chữ cái tuỳ thuộc vào loại toán hạng. Mô tả của toán tử riêng lẻ giải thích sự phụ thuộc vào loại của chúng và chỉ định loại chuyển đổi nào mà chúng thực hiện
- Lưu ý rằng các toán tử gán và một số toán tử khác được liệt kê trong bảng 4.1 trên mong đợi 1 toán hạng thuộc loại `Ival`. `Ivalue` là một thuật ngữ lịch sử có nghĩa là “một biểu thức có thể hợp pháp xuất hiện ở phía bên trái của biểu thức gán”. Trong Js, các biến, property của object và các phần tử của mảng là `Ivalues`

### 4.7.3 **Operator Side Effects**

- Việc đánh giá một toán tử đơn giản như `2 * 3` không bao giờ ảnh hưởng đến trạng thái của chương trình của bạn và bất kỳ phép tính nào trong tương lai mà chương trình của bạn thực hiện sẽ không bị ảnh hưởng bởi phép đánh giá đó. Tuy nhiên, một số biểu thức có tác dụng phụ và việc đánh giá chúng có thể ảnh hưởng đến kết quả của các phép đánh giá trong tương lai. Các toán tử gán là ví dụ rõ ràng nhất: Nếu bạn đang gán 1 giá trị cho một biến hoặc thuộc tính, điều đó sẽ thay đổi giá trị của bất kỳ biểu thức nào sử dụng biến hoặc thuộc tính đó. Các toán tử tăng `++` và `--` cũng tương tự vì chúng thực hiện 1 phép gán ngầm. Toán tử `delete` cũng có tác dụng phụ: xoá một thuộc tính giống như (nhưng không giống như) gán `undefined` cho thuộc tính đó
- Không có toán tử Js nào khác có tác dụng phụ, nhưng việc gọi hàm và biểu thức tạo object sẽ có tác dụng phụ nếu bất kỳ toán tử nào được sử dụng trong phần thân hàm hoặc hàm tạo có tác dụng phụ

### 4.7.4 **Operator Precedence**

- Các toán tử được liệt kê trong 4-1 được sắp xếp theo thứ tự từ độ ưu tiên cao đến độ ưu tiên thấp, với các đường ngang phân cách các nhóm toán tử ở cùng một mức độ ưu tiên. Độ ưu tiên của toán tử kiểm soát thứ tự thực hiện các phép toán. Các toán tử có độ ưu tiên cao hơn (gần đầu bảng hơn) được thực hiện trước các toán tử có độ ưu tiên thấp hơn (gần cuối bảng hơn)
    
    ```jsx
    w = x + y*z; 
    ```
    
- Toán tử `*` có độ ưu tiên cao hơn toán tử `+`, vì vậy phép nhân được thực hiện trước phép cộng. Hơn nữa, toán tử gán `=` có độ ưu tiên thấp nhất, vì vậy phép gán được thực hiện sau khi tất cả các phép toán ở phía bên phải được hoàn thành
- Độ ưu tiên của toán tử có thể được ghi đè bằng cách sử dụng rõ ràng dấu ngoặc đơn. Để buộc phép cộng trong ví dụ trước được thực hiện, hãy viết
    
    ```jsx
    w = (x + y)*z; 
    ```
    
- Lưu ý rằng biểu thức truy cập thuộc tính và gọi hàm có độ ưu tiên cao hơn bất kỳ toán tử nào được liệt kê trên bảng 4-1
    
    ```jsx
    // my là một đối tượng có thuộc tính có tên là functions có giá trị là một
    // mảng các hàm. Chúng ta gọi hàm số x, truyền cho nó đối số
    // y, và sau đó chúng ta hỏi về loại giá trị được trả về.
    typeof my.functions[x](y) 
    ```
    
- Mặc dù typeof là một trong những toán tử có độ ưu tiên cao nhất, nhưng thao tác typeof được thực hiện dựa trên kết quả của việc truy cập thuộc tính, index và gọi hàm, tất cả đều có độ ưu tiên cao hơn các toán tử
- Trong thực tế, nếu bạn hoàn toàn không chắc chắn về độ ưu tiên toán tử của mình, điều đơn giản nhất là sử dụng dấu ngoặc đơn để làm cho thứ tự đánh giá rõ ràng. Các quy tắc quan trọng cần biết là: phép nhân và phép chia được thực hiện trước phép cộng và phép trừ và phép gán có độ ưu tiên thấp nhất, hầu như luôn thực hiện cuối cùng
- Khi các toán tử được thêm vào Js, chúng không phải lúc nào cũng phù hợp một cách tự nhiên với sơ đồ ưu tiên này. Toán tử `??` (4.13.2) được hiển thị trong bảng có độ ưu tiên thấp hơn `||` và `&&` , nhưng trên thực tế, độ ưu tiên của nó so với các toán tử đó không được xác định và ES2020 yêu cầu bạn phải sử dụng rõ ràng dấu ngoặc đơn nếu bạn trộn `??` với `||` hoặc `&&` . Tương tự, toán tử luỹ thừa `**` mới không có độ ưu tiên được xác định so với các toán tử phủ định đơn nhất, bạn phải sử dụng dấu ngoặc đơn khi kết hợp phủ định với luỹ thừa

### 4.7.5 **Operator Associativity**

- Trong bảng 4-1, cột có lable A chỉ định tính kết hợp của toán tử. Giá trị L chỉ định kết hợp từ trái sang phải và giá trị R chỉ định kết hợp từ phải sang trái. Tính kết hợp của toán tử chỉ định thứ tự thực hiện các phép toán có cùng độ ưu tiên. Tính kết hợp từ trái sang phải có nghĩa là các phép toán được thực hiện từ trái sang phải. Ví dụ toán tử trừ có tính kết hợp từ trái qua phải vì vậy
    
    ```jsx
    w = x - y - z; 
    ```
    
- Giống với
    
    ```jsx
    w = ((x - y) - z); 
    ```
    
- Mặt khác, các biểu thức sau
    
    ```jsx
    y = a ** b ** c;
    x = ~-y;
    w = x = y = z;
    q = a?b:c?d:e?f:g; 
    ```
    
- Tương đương với
    
    ```jsx
    y = (a ** (b ** c));
    x = ~(-y);
    w = (x = (y = z));
    q = a?b:(c?d:(e?f:g)); 
    ```
    
- Vì các toán tử luỹ thừa, đơn nhất, gán và điều kiện 3 ngôi có tính kết hợp từ trái qua phải

### **4.7.6 Order of Evaluation**

- Độ ưu tiên và tính kết hợp của toán tử chỉ định thứ tự thực hiện các phép toán trong một biểu thức phức tạp, nhưng chúng không chỉ định thứ tự đánh giá các biểu thức con. Js luôn đánh giá thứ tự các biểu thức từ trái qua phải. Ví dụ trong biểu thức `w = x + y * z` , biểu thức con `w` được đánh giá trước, tiếp theo là x y z. Sau đó giá trị của y và z được nhân, cộng với giá trị của x và gán cho biến hoặc thuộc tính được chỉ định bởi biểu thức w. Việc thêm dấu ngoặc đơn vào các biểu thức có thể thay đổi thứ tự tương đối của phép nhân, phép cộng và phép gán nhưng không thay đổi thứ tự đánh giá từ trái sang phải
- Thứ tự đánh giá chỉ tạo ra sự khác biệt nếu bất kỳ biểu thức nào đang được đánh giá có tác dụng phụ ảnh hưởng đến giá trị của một biểu thức khác. Nếu biểu thức x tăng một biến được sử dụng bởi biểu thức z, thì thực tế là x được đánh giá trước z là quan trọng

## 4.8 Arithmetic Expressions

- Phần này bao gồm các toán tử thực hiện các phép toán số học hoặc các thao tác số khác trên các toán hạng của chúng. Các toán tử luỹ thừa, nhân chia và trừ khá đơn giản và đã đề cập trước. Toán tử cộng có một tiểu mục riêng vì nó có thể thực hiện nối chuỗi mà có một số quy tắc chuyển đổi kiểu bất thường. Các toán tử đơn nhất và toán tử bitwise cũng được đề cập trong các tiểu mục của riêng chúng
- Hầu hết các toán tử số học này (ngoại trừ những toán tử  được ghi chú như sau)  có thể được sử dụng với các toán hạng `BigInt` (3.2.5) hoặc với các số thông thường miễn là bạn không trộn lẫn 2 loại này
- Các toán tử số học cơ bản là `**` (luỹ thừa), *, /, %, +, -. Như đã lưu ý, chúng ta sẽ thảo luận toán tử + ở 1 phần riêng. Năm toán tử còn lại chỉ đơn giản là đánh giá các toán hạng của chúng , chuyển đổi các giá trị thành số nếu cần và sau đó tính toán luỹ thừa , tích, thương, phần dư hoặc hiệu số. Các toán hạng không phải là số có thể được chuyển đổi thành số sẽ được chuyển đổi thành giá trị `NaN` . Nếu một trong 2 toán hạng là (hoặc được chuyển đổi thành) NaN, kết quả của phép toán (hầu như luôn luôn) là NaN
- Toán tử ** có độ ưu tiên cao hơn *, / và % (lần lượt có độ ưu tiên cao hơn + và -). Không giống như các toán tử khác, ** hoạt động từ phải sang trái, vì vậy `2**2**3` giống với `2**8`, không phải `4**3`
- Có một sự mơ hồ tự nhiên đối với các biểu thức như  `-3**2`. Tuỳ thuộc vào độ ưu tiên tương đối của dấu trừ đơn nhất và luỹ thừa, biểu thức đó có thể có nghĩa là `(-3)**2` hoặc `-(3**2)`. Các ngôn ngữ khác nhau xử lý điều này khác nhau và thay vì chọn bên, Js chỉ đơn giản là biến nó thành lỗi cú pháp nếu bỏ qua dấu ngoặc đơn trong trường hợp này, buộc bạn phải viết 1 biểu thức rõ ràng. `**` là toán tử số học mới nhất của Js: nó  đã được thêm vào ES2016. Tuy nhiên, hàm `Math.pow()` đã có sẵn từ phiên bản Js sớm nhất và nó thực hiện chính xác cùng một phép toán như toán tử `**`
- Toán tử chia toán hạng thứ 1 cho toán hạng thứ 2. Nếu bạn đã quen với các ngôn ngữ lập trình phân biệt giữa số nguyên và dấu phẩy động, bạn có thể mong đợi  nhận được kết quả là số nguyên khi bạn chia một số nguyên cho một số nguyên khác. Tuy nhiên, trong Js, tất cả các số đều là số dấu phẩy động, vì vậy tất cả các phép chia đều có kết quả lầ dấu phẩy động: `5/2` được đánh giá là `2.5`, không phải 2. Chia cho 0 sẽ tạo ra dương vô cực, trong khi `0/0` được đánh giá là NaN: Không có trường hợp nào trong số này gây ra lỗi
- Toán tử `%` tính toán toán hạng thứ 1 modulo toán tử thứ 2. Nói cách khác, nó trả về phần dư sau khi chia số nguyên toán hạng thứ nhất cho toán hạng thứ 2. Dấu của kết quả giống với dấu của toán hạng thứ 1. Ví dụ `5 % 2` được đánh giá là 1 và `-5 % 2` được đánh giá là -1
- Mặc dù toán tử modulo thường được sử dụng với các toán hạng số nguyên, nhưng nó cũng hoạt động cho các giá trị dấu phẩy động. Ví dụ `6.5 % 2.1` được đánh giá là 0.2

### 4.8.1 The + Operator

- Toán tử nhị phân `+` cộng các toán hạng số hoặc các toán hạng chuỗi
    
    ```jsx
    1 + 2 // => 3
    "hello" + " " + "there" // => "hello there"
    "1" + "2" // => "12" 
    ```
    
- Khi giá trị của cả 2 toán hạng là số hoặc đều là chuỗi, thì rõ ràng toán tử `+` làm gì. Tuy nhiên, trong bất kỳ trường hợp nào khác, cần phải chuyển đổi kiểu và thao tác được thực hiện phụ thuộc vào việc chuyển đổi được thực hiện. Các quy tắc chuyển đổi cho `+` ưu tiên nối chuỗi: Nếu một trong 2 toán hạng là chuỗi hoặc 1 object được chuyển đổi thành chuỗi, toán hạng kia sẽ được chuyển đổi thành chuỗi và phép nối được thực hiện. Phép cộng chỉ được thực hiện khi không có toán hạng nào giống chuỗi
- Về mặt kỹ thuật, toán tử `+` hoạt động như thế này
    - Nếu một trong các giá trị toán hạng của nó là một object, nó sẽ chuyển đổi nó thành một kiểu nguyên thuỷ bằng cách chuyển object thành nguyên thuỷ được mô tả trong 3.9.3. Các object `Date` được chuyển đổi bằng phương thức `toString()`  của chúng và tất các các object khác được chuyển đổi thông qua `valueOf()`, nếu method đó trả về 1 dữ liệu nguyên thuỷ. Tuy nhiên, hầu hết các object không có method valueOf() hữu ích, vì vậy chúng được chuyển đổi thông qua `toString()`
    - Sau khi chuyển đổi object thành nguyên thuỷ, nếu một trong 2 toán hạng là chuỗi, toán hạng kia sẽ được chuyển đổi thành chuỗi và phép nối được thực hiện
    - Nếu không, cả 2 toán hạng sẽ được chuyển đổi thành số (hoặc thành NaN) và phép cộng được thực hiện
- Đây là một số ví dụ
    
    ```jsx
    1 + 2 // => 3: cộng
    "1" + "2" // => "12": nối chuỗi
    "1" + 2 // => "12": nối chuỗi sau khi chuyển đổi số thành chuỗi
    1 + {} // => "1[object Object]": nối chuỗi sau khi chuyển đổi đối tượng thành chuỗi
    true + true // => 2: cộng sau khi chuyển đổi boolean thành số
    2 + null // => 2: cộng sau khi null được chuyển đổi thành 0
    2 + undefined // => NaN: cộng sau khi undefined được chuyển đổi thành NaN 
    ```
    
- Cuối cùng, điều cần lưu ý là khi toán tử `+` được sử dụng với chuỗi và số, nó có thể không có tính kết hợp. Tức là, kết quả còn phụ thuộc vào thứ tự thực hiện của các phép toán
    
    ```jsx
    1 + 2 + " blind mice" // => "3 blind mice"
    1 + (2 + " blind mice") // => "12 blind mice" 
    ```
    
- Dòng đầu tiên không có dấu ngoặc đơn và toán tử + có tính kết hợp từ trái sang phải, vì vậy 2 số được cộng trước và tổng của chúng được nối với chuỗi. Trong dòng thứ 2, dấu ngoặc đơn thay đổi thứ tự của các phép toán này: số 2 được nối với chuỗi để tạo ra một chuỗi mới. Sau đó, số 1 được nối với chuỗi mới để tạo ra kết quả cuối cùng

### 4.8.2 **Unary Arithmetic Operators**

- Toán tử đơn nhất sửa đổi giá trị của một toán hạng duy nhất để tạo ra một giá trị mới. Trong Js, tất cả các giá trị đơn nhất đều có độ ưu tiên cao và đều có tính kết hợp phải. Tất cả các toán tử đơn nhất được mô tả trong phần này (+, -, ++, —) đều chuyển đổi toán hạng duy nhất của chúng thành số, nếu cần. Lưu ý rằng các ký tự dấu câu + và - được sử dụng làm cả toán tử đơn nhất và toán tử nhị phân
- Các toán tử số học đơn nhất như sau:
- **Cộng đơn nhất (+)**
    - Toán tử cộng đơn nhất chuyển đổi toán hạng của nó thành số (hoặc thành NaN) và trả về giá trị đã chuyển đổi đó. Khi được sử dụng với một toán hạng là số, nó không làm gì cả. Toán tử này có thể không được sử dụng với các giá trị `BigInt`, vì chúng không được chuyển đổi thành số thông thường
- **Trừ đơn nhất (-)**
    - Khi - được sử dụng làm toán tử đơn nhất, nó sẽ chuyển toán hạng của chúng thành số, nếu cần và sau đó thay đổi dấu của kết quả
- **Tăng (++)**
    - Toán tử tăng ++ (tức là cộng 1 vào) toán hạng duy nhất của nó, phải là một Ivalue (một biến, một phần tử của mảng hoặc một property của object). Toán tử chuyển đổi toán hạng của chúng thành số, cộng 1 vào số đó và gán giá trị đã tăng trở lại vào biến, element hoặc property
    - Giá trị của toán tử `++` phụ thuộc vào vị trí của nó so với toán hạng. Khi được sử dụng trước toán hạng, được gọi là toán tử tăng trước, nó sẽ tăng toán hạng và đánh giá thành giá trị tăng của toán hạng đó. Khi được sử dụng sau toán hạng, được gọi là toán tử tăng sau, nó sẽ tăng toán hạng của nó nhưng đánh giá thành giá trị chưa tăng của toán hạng đó. Hãy xem sự khác biệt giữa 2 dòng này
        
        ```jsx
        let i = 1, j = ++i; // i và j đều là 2
        let n = 1, m = n++; // n là 2, m là 1 
        ```
        
    - Lưu ý rằng biểu thức `x++` không phải lúc nào cũng bằng `x = x + 1` . Toán tử ++ không bao giờ thực hiện nối chuỗi: nó luôn chuyển đổi toán hạng của nó thành số và tăng nó. Nếu x là “1”, `++x` là số 2, nhưng x + 1 là chuỗi “11”
    - Cũng lưu ý rằng do tính năng tự động chèn dấu ; của Js, bạn không thể chèn xuống dòng giữa toán tử tăng và toán hạng đứng trước nó. Nếu bạn làm như vậy, Js sẽ coi toán hạng là một câu lệnh hoàn chỉnh và chèn dấu chấm phẩy trước nó
    - Toán tử này, ở cả dạng ++ và — , thường được sử dụng nhất để tăng bộ đếm điều khiển vòng lặp for (5.4.3)
- **Giảm (—)**
    - Toán tử `--` mong đợi một toán hạng Ivalue. Nó chuyển đổi giá trị toán hạng thành số, trừ đi 1 và gán giá trị đã giảm trở lại cho toán hạng. Giống như ++, giá trị trả về của — phụ thuộc vào vị trí của nó so với toán hạng. Khi được sử dụng trươc toán hạng, nó sẽ giảm và trả về giá trị đã giảm. Khi sử dụng sau toán hạng, nó sẽ giảm toán hạng nhưng trả về giá trị chưa giảm. Khi được sử dụng sau toán hạng của nó, không được phép xuống dòng giữa các toán hạng

### 4.8.3 **Bitwise Operators**

- Các toán tử bitwise thực hiện các thao tác cấp thấp trên các bit trong biểu diễn nhị phân của các số. Mặc dù chúng không thực hiện các phép toán số học truyền thống, nhưng chúng được phân loại là toán tử số học ở đây vì chúng hoạt động trên các toán hạng số và trả về một giá trị số. Bốn trong số các toán tử này thực hiện đại số boolean trên các bit riêng lẻ của các toán hạng, hoạt động như thể mỗi bit trên các toán hạng là một giá trị boolean (1 = true, 0 = false). Ba toán tử bitwise còn lại được sử dụng để dịch chuyển các bit sang trái và sang phải. Các toán tử này không được sử dụng phổ biến trong lập trình JS và nếu bạn không quen thuộc với biểu diễn nhị phân của số nguyên, bao gồm cả biểu diễn bù 2 của số nguyên âm, bạn có thể bỏ qua phần này
- Các toán tử bitwise mong đợi các toán hạng số nguyên và hoạt động như thể các giá trị đó được biểu diễn dưới dạng số nguyên 32bit thay vì các giá trị float 64 bit. Các toán tử này chuyển đổi các toán hạng của chúng thành số, nếu cần và sau đó ép buộc các giá trị số thành số nguyên 32bit bằng cách bỏ bất kỳ phân số nào và bất kỳ bit nào vượt quá bit thứ 32. Các toán tử dịch chuyển yêu cầu các toán hạng bên phải nằm trong khoảng từ 0 đến 31. Sau khi chuyển đổi toán hạng này thành số nguyên 32bit không dấu, chúng ta sẽ bỏ bất kỳ bit nào vượt quá bit thứ 5, tạo ra một số trong phạm vi thích hợp
- Đáng ngạc nhiên là NaN, Infinity và -Infinity đều được chuyển đổi thành 0 khi được sử dụng làm toán hạng của các toán tử bitwise này
- Tất cả các toán tử bitwise này ngoại trừ `>>>` có thể được sử dụng với các toán hạng số thông thường hoặc với các toán hạng `BigInt` (3.2.5)
- **Bitwise AND (&)**
    - Toán tử & thực hiện phép toán Boolean AND trên mỗi bit của các đối số nguyên của nó. Mỗi bit được đặt trong kết quả chỉ khi bit tương ứng được đặt trong cả 2 toán hạng. Ví dụ: 0x1234 & 0x00FF được đánh giá là 0x0034.
- Bitwise OR (|)
    - Toán tử | thực hiện phép toán Boolean OR trên mỗi bit của các đối số nguyên của nó. Một bit được đặt trong kết quả nếu bit tương ứng được đặt trong một hoặc 2 toán hạng. Ví dụ: 0x1234 | 0x00FF được đánh giá là 0x12FF.
- **Bitwise XOR (^)**
    - Toán tử ^ thực hiện phép toán Boolean XOR (exclusive OR) trên mỗi bit của các đối số nguyên của nó. XOR có nghĩa là toán hạng 1  là đúng hoặc toán hạng 2 là đúng, nhưng không phải cả 2. Một bit được đặt trong kết quả của phép toán này nếu một bit tương ứng được đặt trong một (nhưng không phải cả hai) trong hai toán hạng. Ví dụ: 0xFF00 ^ 0xF0F0 được đánh giá là 0x0FF0
- **Bitwise NOT (~)**
    - Toán tử ~ là một toán tử đơn nhất xuất hiện trước toán hạng số nguyên duy nhất của nó. Nó hoạt động bằng cách đảo ngược tất cả các bit trong toán hạng. Do cách số nguyên có dấu được biểu diễn trong **JavaScript**, việc áp dụng toán tử ~ cho một giá trị tương đương với việc thay đổi dấu của nó và trừ đi 1. Ví dụ: ~0x0F được đánh giá là 0xFFFFFFF0 hoặc -16.
- **Dịch trái (<<)**
    - Toán tử << di chuyển tất cả các bit trong toán hạng thứ nhất của nó sang trái một số vị trí được chỉ định trong toán hạng thứ hai, phải là một số nguyên từ 0 đến 31. Ví dụ: trong phép toán a << 1, bit đầu tiên (bit đơn vị) của a trở thành bit thứ hai (bit hàng chục), bit thứ hai của a trở thành bit thứ ba, v.v. Số không được sử dụng cho bit đầu tiên mới và giá trị của bit thứ 32 bị mất. Dịch chuyển một giá trị sang trái một vị trí tương đương với nhân với 2, dịch chuyển hai vị trí tương đương với nhân với 4, v.v. Ví dụ: 7 << 2 được đánh giá là 28.
- **Dịch phải với dấu (>>)**
    - Toán tử >> di chuyển tất cả các bit trong toán hạng thứ nhất của nó sang phải một số vị trí được chỉ định trong toán hạng thứ hai (một số nguyên từ 0 đến 31). Các bit bị dịch chuyển ra khỏi bên phải sẽ bị mất. Các bit được điền vào bên trái phụ thuộc vào bit dấu của toán hạng ban đầu, để bảo toàn dấu của kết quả. Nếu toán hạng thứ nhất là dương, kết quả sẽ có các số 0 được đặt ở các bit cao; nếu toán hạng thứ nhất là âm, kết quả sẽ có các số 1 được đặt ở các bit cao. Dịch chuyển một giá trị dương sang phải một vị trí tương đương với chia cho 2 (bỏ phần dư), dịch chuyển sang phải hai vị trí tương đương với chia số nguyên cho 4, v.v. Ví dụ: 7 >> 1 được đánh giá là 3, nhưng lưu ý rằng -7 >> 1 được đánh giá là -4.
- **Dịch phải với điền số không (>>>)**
    - Toán tử >>> giống như toán tử >>, ngoại trừ việc các bit được dịch chuyển vào bên trái luôn là số không, bất kể dấu của toán hạng thứ nhất. Điều này hữu ích khi bạn muốn coi các giá trị 32 bit có dấu như thể chúng là số nguyên không dấu. Ví dụ: -1 >> 4 được đánh giá là -1, nhưng -1 >>> 4 được đánh giá là 0x0FFFFFFF. Đây là toán tử bitwise duy nhất của **JavaScript** không thể được sử dụng với các giá trị **BigInt**. **BigInt** không biểu diễn số âm bằng cách đặt bit cao theo cách mà số nguyên 32 bit làm và toán tử này chỉ có ý nghĩa đối với biểu diễn bù 2 cụ thể đó.

## 4.9 **Relational Expressions**

- Phần này mô tả các toán tử quan hệ của JS. Toán tử này kiểm tra mối quan hệ (chẳng hạn như “bằng”, “nhỏ hơn” hoặc “thuộc tính của”) giữa 2 giá trị và trả về true hoặc false tuỳ thuộc vào mối quan hệ đó có tồn tại hay không. Các biểu thức quan hệ luôn được đánh giá thành một giá trị boolean và giá trị đó thường được sử dụng để kiểm soát luồng thực thi chương trình trong các câu lệnh if, while và for (xem chương 5). Các tiểu mục sau đây ghi lại các toán tử bằng và không bằng , các toán tử so sánh và hai toán tử quan hệ khác của Js, in và insanceof

### 4.9.1 **Equality and Inequality Operators**

- Các toán tử == và === kiểm tra xem 2 giá trị có giống nhau hay không, sử dụng 2 định nghĩa khác nhau về sự giống nhau. Cả 2 toán tử đều chấp nhận các toán hạng thuộc bất kỳ loại nào và cả 2 đều trả về true nếu các toán hạng của chúng giống nhau và false nếu chúng khác nhau. Toán từ `===` được gọi là toán tử nghiêm ngặt (hoặc đôi khi là toán tử nhận dạng) và nó kiểm tra xem 2 toán hạng có “giống hệt nhau” hay không bằng cách sử dụng một định nghĩa nghiêm ngặt về sự giống nhau. Toán tử == được gọi là toán tử bằng; nó kiểm tra xem hai toán hạng của nó có “bằng nhau” hay không bằng nhau bằng cách sử dụng một cách định nghĩa lỏng lẻo hơn về sự giống nhau cho phép chuyển đổi kiểu
- Các toán từ `!=` và `!==` kiểm tra điều ngược lại chính xác của các toán tử == và ===. Toán tử `!=` trả về false nếu 2 giá trị bằng nhau theo `==` và trả về true trong trường hợp ngược lại. Toán tử `!==` sẽ trả về false nếu 2 giá trị bằng nhau nghiêm ngặt và trả về true trong trường hợp ngược lại. Như bạn sẽ thấy trong 4.10, toán tử ! tính toán phép toán boolean NOT. Điều này giúp dễ dàng ghi nhớ rằng `!=` và `!==` là viết tắt của “không bằng” và “không bằng nghiêm ngặt”

### Các toán tử =, ==, ===

- Js hỗ trợ các toán tử =, ==, ===. Hãy chắc chắn rằng bạn hiểu sự khác biệt giữa các toán tử gán, bằng và bằng nghiêm ngặt này và hãy cẩn thận sử dụng toán tử đúng khi viết code
- Mặc dù rất hấp dẫn khi đọc cả 3 toán tử là bằng, nhưng có thể giúp giảm bớt sự nhầm lẫn nếu bạn đọc “nhận” hoặc “được gán” cho `=`, “bằng” cho `==` và “bằng nghiêm ngặt” cho `===`
- Toán tử `==` là một tính năng kế thừa của Js và được coi là một nguồn gây ra lỗi. Bạn hầu như nên sử dụng `===` thay vì `==` và `!==` thay vì `!=`
- Như đã đề cập trong 3.8, các object Js được so sánh bằng tham chiếu, không phải bằng giá trị. Một object bằng chính nó, nhưng không bằng bất kỳ object nào khác. Nếu 2 object riêng biệt có cùng số lượng property với cùng tên và giá trị, thì chúng vẫn không bằng nhau. Tương tự, 2 mảng có cùng các phần tử theo cùng thứ tự không bằng nhau

### STRICT EQUALITY

- Toán tử bằng nghiêm ngặt === đánh giá các toán hạng của nó, sau đó so sánh 2 giá trị như sau, không thực hiện chuyển đổi kiểu
    - Nếu 2 giá trị có kiểu khác nhau, thì chúng không bằng nhau
    - Nếu cả 2 giá trị đều là null hoặc đều là undefined, thì chúng bằng nhau
    - Nếu cả 2 giá trị đều là giá trị boolean true hoặc false thì chúng bằng nhau
    - Nếu 1 hoặc cả 2 giá trị là NaN, thì chúng không bằng nhau (Điều này đáng ngạc nhiên, nhưng giá trị NaN không bao giờ bằng bất kỳ giá trị nào khác, bao gồm cả chính nó! Để kiểm tra giá trị x có phải là NaN không, hãy sử dụng `x !== x` hoặc `isNaN()`
    - Nếu cả hai giá trị đều là số và có cùng giá trị thì chúng bằng nhau. Nếu một giá trị là 0 và giá trị kia là -0 thì chúng cũng bằng nhau
    - Nếu cả 2 giá trị đều là chuỗi và chứa chính xác các giá trị 16bit giống nhau (3.3) ở cùng 1 vị trí thì chúng bằng nhau. Nếu các chuỗi khác nhau về độ dài hoặc nội dung, thì chúng không bằng nhau. Hai chuỗi có thể có cùng ý nghĩa và cùng hình thức trực quan nhưng vẫn được mã hoá bằng các chuỗi giá trị 16bit khác nhau. Js không thực hiện chuẩn hoá Unicode và một cặp chuỗi như thế này không được coi là bằng nhau với các toán tử === hoặc ==
    - Nếu cả 2 giá trị đều tham chiếu đến cùng một object, array hoặc function thì chúng bằng nhau. Nếu chúng tham chiếu đến các object khác nhau, thì chúng không bằng nhau ngay cả nếu cả 2 object có các thuộc tính giống hệt nhau

### EQUALITY WITH TYPE CONVERSION

- Toán tử == giống như toán tử bằng nghiêm ngặt, nhưng nó ít nghiêm ngặt hơn. Nếu giá trị của 2 toán hạng không cùng loại, nó sẽ thử một số chuyển đổi kiểu và thử so sánh lại
- Nếu 2 giá trị có cùng kiểu, hãy kiểm tra chúng xem có bằng nhau nghiêm ngặt hay không như được mô tả trước đó. Nếu chúng bằng nhau nghiêm ngặt, thì chúng bằng nhau và ngược lại
- Nếu 2 giá trị không cùng kiểu, toán tử == vẫn có thể coi chúng là bằng nhau. Nó sử dụng quy tắc và chuyển đổi kiểu sau để kiểm tra xem có bằng nhau không
    - Nếu một giá trị là null và giá trị kia là undefined thì chúng bằng nhau
    - Nếu một giá trị là chuỗi và 1 giá trị là số, hãy chuyển đổi chuỗi thành số và thử so sánh lại, sử dụng giá trị đã chuyển đổi
    - Nếu 1 trong 2 giá trị là true, hãy chuyển đổi nó thành 1 và thử so sánh lại, và với 0 đối với false
    - Nếu 1 giá trị là object, giá trị kia là chuỗi hoặc số, hãy chuyển đổi object thành 1 kiểu nguyên thuỷ bằng cách sử dụng thuật toán được mô tả trong 3.9.3 và thử so sánh lại. Một object được chuyển thành 1 giá trị nguyên thuỷ bằng phương thức `toString()` hoặc `valueOf()` của nó. Các class tích hợp sẵn của lõi Js cố gắng chuyển đổi `valueOf()` trước khi chuyển qua `toString()`, ngoại trừ class Date, class này thực hiện chuyển đổi `toString()`
    - Bất kỳ sự kết hợp nào khác của giá trị đều không bằng nhau
- Ví dụ để kiểm tra có bằng nhau không, hãy xem phép so sánh
    
    ```jsx
    "1" == true // => true 
    ```
    
- Biểu thức này được đánh giá là true, cho biết các giá trị trông rất khác nhau này thực sự bằng nhau. Giá trị true trước tiên được chuyển đổi thành số 1 và phép so sánh được thực hiện lại. Tiếp theo, chuỗi “1” được chuyển đổi thành số 1. Vì cả 2 giá trị hiện nay đều giống nhau, nên phép so sánh trả về true

### 4.9.2 **Comparison Operators**

- Các toán tử so sánh kiểm tra thứ tự tương đối (số hoặc chữ cái) của 2 toán hạng của chúng
- **Nhỏ hơn (<)**
    - Toán tử < được đánh giá là true nếu toán hạng thứ nhất của nó nhỏ hơn toán hạng thứ hai của nó; ngược lại, nó được đánh giá là false.
- **Lớn hơn (>)**
    - Toán tử > được đánh giá là true nếu toán hạng thứ nhất của nó lớn hơn toán hạng thứ hai của nó; ngược lại, nó được đánh giá là false.
- **Nhỏ hơn hoặc bằng (<=)**
    - Toán tử <= được đánh giá là true nếu toán hạng thứ nhất của nó nhỏ hơn hoặc bằng toán hạng thứ hai của nó; ngược lại, nó được đánh giá là false.
- **Lớn hơn hoặc bằng (>=)**
    - Toán tử >= được đánh giá là true nếu toán hạng thứ nhất của nó lớn hơn hoặc bằng toán hạng thứ hai của nó; ngược lại, nó được đánh giá là false.
- Các toán hạng của toán tử so sánh này có thể thuộc bất kỳ loại nào. Tuy nhiên chỉ có thể thực hiện so sánh trên số và chuỗi, vì vậy các toán hạng không phải là chuỗi hay số sẽ không được chuyển đổi
- Việc so sánh và chuyển đổi sẽ xảy ra như sau
    - Nếu 1 trong 2 toán hạng được đánh giá là object, thì object đó sẽ được chuyển đổi thành một giá trị nguyên thuỷ, được mô tả trong cuối 3.9.3. Nếu method `valueOf()` của nó trả về một giá trị nguyên thuỷ, thì giá trị đó sẽ được sử dụng. Nếu không, giá trị trả về method `toString()` của nó sẽ được sử dụng
    - Nếu sau bất kỳ chuyển đổi object thành nguyên thuỷ nào được yêu cầu, cả 2 toán hạng đều là chuỗi, thì 2 chuỗi sẽ được so sánh, sử dụng thứ tự bảng chữ cái, trong đó thứ tự “bảng chữ cái” được xác định bởi thứ tự số của giá trị Unicode 16bit tạo nên các chuỗi
    - Nếu sau khi chuyển đổi object thành nguyên thuỷ, ít nhất một toán hạng không phải là chuỗi, thì cả 2 toán hạng sẽ được chuyển đổi thành số và được so sánh bằng số. 0 và -0 được coi là bằng nhau
    - Infinity lớn hơn bất kỳ số nào khác ngoài nó và -Infinity nhỏ hơn bất kỳ số nào ngoài chính nó. Nếu 1 trong 2 toán hạng là (hoặc chuyển đổi thành) NaN, thì toán tử so sánh luôn trả về false. Mặc dù các toán tử số học không cho phép các giá trị BigInt được trộn lẫn với các số thông thường, nhưng các toán tử so sánh cho phép so sánh giữa các số và BigInt
- Hãy nhớ rằng các chuỗi Js là các chuỗi có giá trị số nguyên 16bit và việc so sánh chuỗi chỉ là phép so sánh bằng số các giá trị trong chuỗi. Thứ tự mã hoá được xác định bởi Unicode có thể không khớp với thứ tự đối chiếu truyền thống được sử dụng trong bất kỳ ngôn ngữ hoặc địa phương cụ thể nào. Cụ thể, lưu ý rằng việc so sánh chuỗi phân biệt chữ hoa thường và tất cả các chữ cái ASCII viết hoa đều “nhỏ hơn” tất cả các chữ cái ASCII viết thường. Quy tắc này có thể gây ra kết quả khó hiểu nếu bạn không mong đợi nó. Ví dụ theo toán tử `<` , chuỗi “Zoo” đứng trước chuỗi “aardvark”
- Để có thuật toán so sánh chuỗi mạnh hơn, hãy thử method `String.localeCompare()`, method này cũng tính đến các định nghĩa cụ thể về địa phương của thứ tự bảng chữ cái. Đối với các phép toán so sánh không phân biệt chữ hoa thường, bạn có thể chuyển đổi tất cả về chữ thường hoặc chữ hoa bằng cách sử dụng `String.toLowerCase()` hoặc `String.toUppercase()`. Và để có một số công cụ so sánh chuỗi được bản địa hoá tốt hơn và tổng quát hơn, hãy sử dụng class `Int.Collator` được mô tả trong 11.7.3
- Cả toán tử + và các toán tử so sánh đều hoạt động khác nhau đối với các toán hạng số và chuỗi. `+` ưu tiên chuỗi: nó thực hiện phép nối nếu một trong 2 toán hạng là chuỗi. Các toán tử so sánh ưu tiên và chỉ thực hiện so sánh chuỗi nếu cả 2 toán hạng đều là chuỗi
    
    ```jsx
    1 + 2 // => 3: cộng.
    "1" + "2" // => "12": nối chuỗi.
    "1" + 2 // => "12": 2 được chuyển đổi thành "2".
    11 < 3 // => false: so sánh số.
    "11" < "3" // => true: so sánh chuỗi.
    "11" < 3 // => false: so sánh số, "11" được chuyển đổi thành 11.
    "one" < 3 // => false: so sánh số, "one" được chuyển đổi thành NaN. 
    ```
    
- Cuối cùng, lưu ý rằng toán từ `<=` và `>=` không dựa vào các toán tử == hoặc === để xác định xem 2 giá trị có bằng nhau hay không. Thay vào đó được định nghĩa đơn giản là không lớn hơn hoặc không nhỏ hơn. Ngoại lệ duy nhất xảy ra khi 1 trong 2 toán hạng là NaN, trong trường hợp đó, cả 4 toán tử đều trả về false

### 4.9.3 The in Operator

- Toán tử `in` mong đợi một toán hạng bên trái là một chuỗi, ký hiệu hoặc giá trị có thể chuyển đổi thành chuỗi. Nó mong đợi một toán hạng bên phải là một object. Nó được đánh giá là true nếu giá trị bên trái là tên của một thuộc tính của đối tượng bên phải
    
    ```jsx
    let point = {x: 1, y: 1}; // Định nghĩa một đối tượng
    "x" in point // => true: đối tượng có thuộc tính có tên là "x"
    "z" in point // => false: đối tượng không có thuộc tính "z".
    "toString" in point // => true: đối tượng kế thừa phương thức toString
    let data = [7,8,9]; // Một mảng có các phần tử (chỉ mục) 0, 1 và 2
    "0" in data // => true: mảng có một phần tử "0"
    1 in data // => true: các số được chuyển đổi thành chuỗi
    3 in data // => false: không có phần tử 3 
    ```
    

### 4.9.4 The instanceof Operator

- Toán tử `instanceof` mong đợi một toán hạng bên trái là 1 object và một toán hạng bên phải xác định một class object. Toán tử được đánh giá là true nếu object bên trái là một thể hiện của class bên phải và được đánh giá là false nếu không. Chương 9 giải thích rằng, trong Js, các class object được xác định bởi constructor. Do đó, toán hạng bên phải của instanceof phải là 1 function. Đây là 1 ví dụ
    
    ```jsx
    let d = new Date(); // Tạo một đối tượng mới với hàm tạo Date()
    d instanceof Date // => true: d được tạo bằng Date()
    d instanceof Object // => true: tất cả các đối tượng đều là thể hiện của Object
    d instanceof Number // => false: d không phải là một đối tượng Number
    let a = [1, 2, 3]; // Tạo một mảng với cú pháp literal của mảng
    a instanceof Array // => true: a là một mảng
    a instanceof Object // => true: tất cả các mảng đều là đối tượng
    a instanceof RegExp // => false: các mảng không phải là biểu thức chính quy 
    ```
    
- Lưu ý rằng, tất cả các object đều là thể hiện của `Object`. `instanceof` xem xét các “superclass” khi quyết định xem object có phải là thể hiện của 1 class hay không. Nếu toán hạng bên trái của instanceof không phải là một object, instanceof sẽ trả về false. Nếu bên phải không phải là một object, nó sẽ trả về `TypeError`
- Để hiểu rõ cách hoạt động của toán tử instanceof, bạn phải hiểu “chuỗi nguyên mẫu (prototype chain)”. Đây là cơ chế kế thừa của Js và nó được mô tả trong 6.3.2. Để đánh giá biểu thức `o instanceof f` , Js đánh giá `f.prototype` và sau đó tìm kiếm giá trị đó trong chuỗi nguyên mẫu của o. Nếu nó tìm thấy nó, thì o là 1 thể hiện của f (hoặc của 1 class con của f) và toán tử trả về true. Nếu `f.prototype` không phải là một trong các giá trị trong chuỗi nguyên mẫu của o, thì o không phải là một thể hiện của f và instanceof trả về false
