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

## 4.10 **Logical Expressions**

- Toán tử logic `&&, || và !` thực hiện đại số Boolean và thường được sử dụng cùng với các toán tử quan hệ để kết hợp 2 biểu thức quan hệ thành một biểu thức phức tạp hơn. Các toán tử này được mô tả trong các tiểu mục sau đây. Để hiểu đầy đủ về chúng, bạn có thể muốn xem lại khái niệm về các giá trị “truthy” và “falsy” được giới thiệu trong 3.4

### 4.10.1 Logical AND (&&)

- Toán tử && có thể được hiểu ở 3 cấp độ khác nhau. Ở cấp độ đơn giản nhất, khi được sử dụng với toán hạng boolean, `&&` thực hiện phép toán Boolean AND trên 2 giá trị: nó trả về true nếu và chỉ khi cả toán hạng thứ 1 và thứ 2 của nó đều là true. Nếu 1 hoặc cả 2 toán hạng này là false, nó sẽ trả về false
- && thường được sử dụng như một liên từ để nối 2 biểu thức quan hệ
    
    ```jsx
    x === 0 && y === 0 // true nếu và chỉ khi x và y đều bằng 0 
    ```
    
- Các biểu thức quan hệ luôn được đánh giá là true hoặc false, vì vậy khi được sử dụng như thế này, bản thân toán tử && sẽ trả về true hoặc false
- Các toán tử quan hệ có độ ưu tiên cao hơn && (và ||), vì vậy các biểu thức như thế này có thể được viết một cách an toàn mà không cần dấu ngoặc đơn
- Nhưng && không yêu cầu các toán hạng của nó phải là giá trị boolean. Nhớ lại tất cả các giá trị Js đề là “truthy” hoặc “falsy”. (Xem 3.4 để biết chi tiết. Các giá trị sai là false, null, undefined, 0, -0, NaN và “”. Tất cả các giá trị khác, bao gồm tất cả các object, đều là truthy). Mức thứ 2 mà && có thể được hiểu là một toán tử Boolean AND cho các giá trị truthy và falsy. Nếu cả 2 toán hạng đều là truthy, toán tử sẽ trả về một giá trị truthy. Nếu không, một hoặc cả 2 toán hạng phải là sai và toán tử trả về 1 giá trị falsy. Trong Js, bất kỳ biểu thức hoặc câu lệnh nào mong đợi một giá trị boolean sẽ hoạt động với một giá trị truthy hoặc falsy, vì vậy thực tế là && không phải lúc nào cũng trả về true hoặc false không gây ra vấn đề thực tế
- Lưu ý rằng mô tả này nói rằng toán tử trả về “một giá trị truthy” hoặc”một giá trị falsy” nhưng không chỉ định giá trị đó là gì. Đối với điều đó, chúng ta cần mô tả && ở cấp độ thứ 3 và cuối cùng. Toán tử này bắt đầu bằng cách đánh giá toán hạng thứ 1 của nó, biểu thức ở bên trái của nó. Nếu giá trị ở bên trái sai, thì giá trị của toàn bộ biểu thức cũng phải là sai, vì vậy && chỉ đơn giản là trả về giá trị ở bên trái và thậm chí không đánh giá biểu thức ở bên phải
- Mặt khác, nếu giá trị ở bên trái là truthy, thì giá trị tổng thể của biểu thức phụ thuộc vào giá trị ở bên phải. Nếu giá trị ở bên phải là truthy, thì giá trị tổng thể phải là truthy và nếu giá trị bên phải là sai, thì giá trị tổng thể phải là sai. Vì vậy, khi giá trị ở bên trái là truthy, toán tử && đánh giá và trả về giá trị ở bên phải
    
    ```jsx
    let o = {x: 1};
    let p = null;
    o && o.x // => 1: o là chân lý, vì vậy trả về giá trị của o.x
    p && p.x // => null: p là sai, vì vậy trả về nó và không đánh giá p.x 
    ```
    
- Điều quan trọng là phải hiểu rằng && có thể hoặc không thể đánh giá toán hạng bên phải của nó. Trong ví dụ code này, biến `p` được đặt thành null và biểu thức `p.x` , nếu được đánh giá, sẽ gây ra TypeError. Nhưng code sử dụng && theo cách thành ngữ để `p.x` chỉ được đánh giá nếu p là truthy - không phải null hoặc undefined
- Hành vi của && đôi khi được gọi là đoản mạch và đôi khi bạn có thể thấy code cố ý khai thác hành vi này để thực thi code có điều kiện. Ví dụ: hai dòng code Js sau có tác dụng tương đương
    
    ```jsx
    if (a === b) stop(); // Gọi stop() chỉ khi a === b
    (a === b) && stop(); // Điều này làm điều tương tự 
    ```
    
- Nói chung, bạn phải cần thận bất cứ khi nào bạn viết một biểu thức có tác dụng phụ (phép gán, tăng, giảm hoặc gọi hàm) ở bên phải của &&. Việc những tác dụng phụ đó có xảy ra hay không phụ thuộc vào giá trị của bên trái
- Mặc dù cách toán tử này thực sự hoạt động có phần phức tạp, nhưng nó thường được sử dụng nhất như một toán tử đại số Boolean đơn giản hoạt động trên các giá trị truthy và falsy

### 4.10.2 Logical OR (||)

- Toán tử || thực hiện phép toán Boolean OR trên 2 toán hạng của nó. Nếu một hoặc cả 2 toán hạng là truthy, nó sẽ trả về một giá trị truthy. Nếu cả 2 toán hạng đều là falsy, nó sẽ trả về một giá trị falsy
- Mặc dù toán tử || thường được sử dụng đơn giản như 1 toán tử Boolean OR, nhưng nó giống như toán tử &&, có hành vi phức tạp hơn. Nó bắt đầu bằng cách đánh giá toán hạng thứ 1 của nó, biểu thức ở bên trái của nó. Nếu giá trị của toán hạng thứ 1 là truthy, nó sẽ đoản mạch và trả về giá trị truthy đó mà không bao giờ đánh giá biểu thức thức ở bên phải. Mặt khác, nếu giá trị của toán hạng thứ 1 là sai, thì || đánh giá toán hạng thứ 2 của nó và trả về giá trị của biểu thức đó
- Cũng như toán tử &&, bạn nên tránh các toán hạng bên phải bao gồm tác dụng phụ, trừ khi bạn cố ý muốn sử dụng thực tế là biểu thức bên phải có thể không được đánh giá
- Cách sử dụng thành ngữ của toán tử này là chọn giá trị truthy đầu tiên trong một tập hợp các lựa chọn thay thế
    
    ```jsx
    // Nếu maxWidth là chân lý, hãy sử dụng nó. Nếu không, hãy tìm kiếm một giá trị trong
    // đối tượng preferences. Nếu điều đó không đúng, hãy sử dụng một hằng số được mã hóa cứng.
    let max = maxWidth || preferences.maxWidth || 500; 
    ```
    
- Lưu ý rằng, nếu 0 là giá trị hợp pháp cho `maxWith`, thì code này sẽ không hoạt động chính xác, vì 0 là giá trị falsy. Xem toán tử `??` (4.13.2) để biết cách thay thế
- Trước ES6, thành ngữ này thường được sử dụng trong các hàm để cung cấp các giá trị mặc định cho các tham số
    
    ```jsx
    // Sao chép các thuộc tính của o sang p và trả về p
    function copy(o, p) {
        p = p || {}; // Nếu không có đối tượng nào được truyền cho p, hãy sử dụng một đối tượng mới được tạo.
        // phần thân hàm nằm ở đây
    } 
    ```
    
- Tuy nhiên trong ES6 trở lên, thủ thuật này không còn cần thiết nữa vì giá trị tham số mặc định có thể được viết đơn giản trong chính định nghĩa hàm: `function copy(o, p={}) {...}`

### 4.10.3 Logical NOT (!)

- Toán tử ! là một toán tử đơn nhất; nó được đặt trước một toán hạng duy nhất. Mục đích của nó là đảo ngược giá trị boolean của toán hạng của nó. Ví dụ nếu x là truthy, !x được đánh giá là false. Nếu x là false thì !x là true
- Không giống như các toán tử && và ||, toán tử ! chuyển đổi các toán hạng của nó thành giá trị boolean (sử dụng các quy tắc được mô tả trong chương 3) trước khi đảo ngược giá trị đã chuyển đổi. Điều này có nghĩa là ! luôn trả về true hoặc false và bạn có thể chuyển đổi bất kỳ giá trị x nào thành giá trị boolean tương ứng của nó bằng cách áp dụng toán tử này 2 lần `!!x` (xem 3.9.2)
- Là một toán tử đơn nhất, ! có độ ưu tiên cao và liên kết chặt chẽ. Nếu bạn muốn đảo ngược giá trị của một biểu thức như `p && q`, bạn cần sử dụng dấu ngoặc đơn: `!(p && q)`. Điều đáng chú ý là hai định luật của đại số Boolean ở đây mà chúng ta có thể biểu thị bằng cú pháp Js
```js
// Định luật DeMorgan
!(p && q) === (!p || !q) // => true: cho tất cả các giá trị của p và q
!(p || q) === (!p && !q) // => true: cho tất cả các giá trị của p và q 
```
## 4.11 **Assignment Expressions**

- Js sử dụng toán tử = để gán một giá trị cho một biến hoặc thuộc tính
    
    ```jsx
    i = 0; // Đặt biến i thành 0.
    o.x = 1; // Đặt thuộc tính x của đối tượng o thành 1. 
    ```
    
- Toán tử = mong đợi toán hạng bên trái của nó là một Ivalue: một biến hoặc một property của object (hoặc element mảng). Nó mong đợi toán hạng bên phải của nó là một giá trị tuỳ ý thuộc bất kỳ loại nào. Giá trị của một biểu thức gán là giá trị của toán hạng bên phải. Là một tác dụng phụ, toán tử = gán giá trị ở bên phải cho biến hoặc property ở bên trái để các tham chiếu trong tương lai đến biến hoặc property đó được đánh giá thành giá trị đó
- Mặc dù các biểu thức gán thường khá đơn giản, nhưng đôi khi bạn có thể thấy giá trị của một biểu thức gán được sử dụng như một phần của một biểu thức lớn hơn. Ví dụ: bạn có thể gán và kiểm tra một giá trị trong cùng một biểu thức bằng code sau
    
    ```jsx
    (a = b) === 0 
    ```
    
- Nếu bạn làm điều này, hãy chắc chắn rằng bạn hiểu rõ sự khác biệt giữa các toán tử = và ===! Lưu ý rằng = có độ ưu tiên rất thấp và dấu ngoặc đơn thường cần thiết khi giá trị của một phép gán được sử dụng trong một biểu thức lớn hơn
- Toán tử gán có tính kết hợp từ phải sang trái, có nghĩa là khi nhiều toán tử gán xuất hiện trong một biểu thức, chúng sẽ được đánh giá từ phải sang trái. Do đó, bạn có thể viết code như sau để gán một giá trị duy nhất cho nhiều biến
    
    ```jsx
    i = j = k = 0; // Khởi tạo 3 biến thành 0 
    ```
    

### 4.11.1 **Assignment with Operation**

- Bên cạnh toán tử gán = thông thường, Js hỗ trợ một số toán tử gán khác cung cấp các phím tắt bằng cách kết hợp phép gán với một số phép toán khác. Ví dụ: toán tử `+=` thực hiện phép cộng và phép gán. Biểu thức sau
    
    ```jsx
    total += salesTax; 
    ```
    
- Tương đương với biểu thức này
    
    ```jsx
    total = total + salesTax; 
    ```
    
- Như bạn có thể mong đợi, toán tử `+=` hoạt động cho số hoặc chuỗi. Đối với các toán hạng số, nó thực hiện phép cộng và phép gán; đối với các toán hạng chuỗi, nó thực hiện phép nối và phép gán
- Các toán tử tương tự bao gồm `-=`, `*=`, `&=`,…
    
    ```jsx
    Toán tử	Ví dụ	Tương đương
    +=	a += b	a = a + b
    -=	a -= b	a = a - b
    *=	a *= b	a = a * b
    /=	a /= b	a = a / b
    %=	a %= b	a = a % b
    **=	a **= b	a = a ** b
    <<=	a <<= b	a = a << b
    >>=	a >>= b	a = a >> b
    >>>=	a >>>= b	a = a >>> b
    &=	a &= b	a = a & b
    `	=`	`a
    ^=	a ^= b	a = a ^ b
    ```
    
- Trong hầu hết các trường hợp, biểu thức
    
    ```jsx
    a op= b 
    ```
    
- Trong đó `op` là một toán tử tương đương với biểu thức
    
    ```jsx
    a = a op b 
    ```
    
- Ở dòng đầu tiên, biểu thức a được đánh giá 1 lần. Ở dòng thứ 2, nó được đánh giá 2 lần. Hai trường hợp sẽ khác nhau chỉ khi `a` bao gồm các tác dụng phụ như được gọi hàm hoặc toán tử tăng. Ví dụ 2 phép gán sau đây không giống nhau
    
    ```jsx
    data[i++] *= 2;
    data[i++] = data[i++] * 2; 
    ```

## 4.12 **Evaluation Expressions**

- Giống như nhiều ngôn ngữ thông dịch, Js có khả năng thông dịch các chuỗi mã nguồn Js, đánh giá chúng để tạo ra một giá trị. Js thực hiện việc này với hàm `eval()` toàn cục
    
    ```jsx
    eval("3+2") // => 5 
    ```
    
- Việc đánh giá động các chuỗi mã nguồn là một tính năng ngôn ngữ mạnh mẽ mà hầu như không bao giờ cần thiết trong thực tế. Nếu bạn thấy mình đang sử dụng `eval()`, bạn nên cân nhắc kỹ xem liệu bạn có thực sự cần sử dụng nó hay không. Đặc biệt `eval()` có thể là một lỗ hổng bảo mật và bạn không bao giờ nên chuyển bất kỳ chuỗi nào có nguồn gốc từ đầu vào của người dùng tới `eval()`. Với một ngôn ngữ phức tạp như Js, không có cách nào để vệ sinh đầu vào của người dùng để làm cho nó an toàn khi sử dụng với `eval()`. Do những vấn đề bảo mật này, một số máy chủ web sử dụng tiêu đề HTTP “Content-Security-Policy” để tắt eval() cho toàn bộ trang web
- Các tiểu mục sau đây giải thích cách sử dụng cơ bản của `eval()` và giải thích 2 phiên bản bị hạn chế của nó ít ảnh hưởng đến trình tối ưu hoá hơn

### **EVAL() LÀ MỘT HÀM HAY MỘT TOÁN TỬ?**

- `eval()` là một hàm, nhưng nó được bao gồm trong chương này về các biểu thức vì nó thực sự nên là một toán tử. Các phiên bản đầu tiên của ngôn ngữ đã định nghĩa một hàm `eval()` và kể từ đó, các nhà thiết kế ngôn ngữ và người viết trình thông dịch đã đặt ra các hạn chế đối với nó khiến nó ngày càng trở nên giống toán tử hơn. Các trình thông dịch Js hiện đại thực hiện rất nhiều phân tích và tối ưu hoá code. Nói chung nếu một hàm gọi `eval()`, trình thông dịch không thể tối ưu hoá hàm đó. Vấn đề với việc định nghĩa `eval()` như một hàm là nó có thể được đặt tên khác
    
    ```jsx
    let f = eval;
    let g = f; 
    ```
    
- Nếu điều này được phép, thì trình thông dịch không thể biết chắc hàm nào gọi `eval()`, vì vậy nó không thể tối ưu hoá một các quyết liệt. Vấn đề này có thể đã được tránh nếu eval() là một toán tử (và một từ dành riêng). Chúng ta sẽ tìm hiểu (trong 4.12.2 và 4.12.3) về các hạn chế được đặt ra với eval() để làm cho nó giống toán tử hơn

### **4.12.1 eval()**

- `eval()` mong đợi 1 đối số. Nếu bạn truyền bất kỳ giá trị nào khác ngoài chuỗi, nó sẽ chỉ trả về giá trị đó. Nếu bạn truyền 1 chuỗi, nó sẽ cố gắng phân tích cú pháp chuỗi dưới dạng code Js, ném ra SyntaxError nếu không thành công. Nếu nó phân tích cú pháp chuỗi thành công, thì nó sẽ đánh giá mã và trả về giá trị của biểu thức hoặc câu lệnh cuối cùng trong chuỗi hoặc undefined nếu biểu thức hoặc câu lệnh cuối cùng không có giá trị. Nếu chuỗi được đánh giá ném ra 1 ngoại lệ, thì ngoại lệ đó sẽ lan truyền lệnh gọi tới `eval()`
- Điều quan trọng về `eval()` (khi được gọi thế này) là nó sử dụng môi trường biến của mã gọi nó. Tức là nó tra cứu các giá trị của các biến và định nghĩa các biến và hàm mới giống như cách mà code cục bộ làm. Nếu một hàm định nghĩa một biến cục bộ x và sau đó gọi eval(”x”), nó sẽ nhận được giá trị của biến cục bộ. Nếu nó gọi eval(”x=1”), nó sẽ thay đổi giá trị của biến cục bộ. Và nếu hàm gọi eval(”var y = 3”), nó sẽ khai bá biến cục bộ y mới. Mặt khác, nếu chuỗi được đánh giá sử dụng let hoặc const, thì biến hoặc hằng số được khai báo sẽ là cục bộ đối với việc đánh giá và sẽ không được định nghĩa trong môi trường gọi
- Tương tự, một hàm có thể khai báo một hàm cục bộ với code như sau
    
    ```jsx
    eval("function f() { return x+1; }"); 
    ```
    
- Tất nhiên, nếu bạn gọi eval() từ code cấp cao nhất, nó sẽ hoạt động trên các biến toàn cục và các hàm toàn cục
- Lưu ý rằng chuỗi code bạn chuyển tới eval() phải có ý nghĩa về mặt cú pháp: bạn không thể sử dụng no để dán các đoạn code vào một hàm. Ví dụ: không có ý nghĩa gì hết khi viết eval(”return;”), vì return chỉ hợp lệ trong các hàm và thực tế là chuỗi được đánh giá sử dụng cùng một môi trường như hàm gọi không làm cho nó trở thành một phần của hàm đó. Nếu chuỗi của bạn có ý nghĩa như một tập lệnh độc lập (thậm chí là một tập lệnh rất ngắn như x = 0), thì việc chuyển đến eval() là hợp pháp. Nếu không, eval() sẽ ném ra SyntaxError

### **4.12.2 Global eval()**

- Chính khả năng thay đổi các biến cục bộ của eval() là vấn đề đối với các trình tôi ưu hoá Js. Tuy nhiên, như một giải pháp thay thế, các trình thông dịch chỉ đơn giản là thực hiện ít tối ưu hoá hơn trên bất kỳ hàm nào gọi eval(). Tuy nhiên, trình thông dịch Js nên làm gì nếu một tập lệnh định nghĩa một bí danh cho eval() và sau đó gọi hàm đó bằng một tên khác? Đặc tả Js tuyên bố rằng khi eval() được gọi bằng bất kỳ tên nào khác ngoài “eval”, nó sẽ đánh giá chuỗi như thể nó là mã toàn cục cấp cao nhất. Mã được đánh giá có thể định nghĩa các biến toàn cục hoặc hàm toàn cục mới và nó có thể đặt các biến toàn cục, nhưng nó sẽ không sử dụng hoặc sửa đổi bất kỳ biến cục bộ nào đổi với hàm gọi và do đó sẽ không can thiệp vào việc tối ưu hoá cục bộ
- “Direct eval” là một lệnh gọi tới hàm eval() với một biểu thức sử dụng chính xác tên không đủ tiêu chuẩn “eval” (bắt đầu giống như một từ dành riêng). Các lệnh gọi trực tiếp tới eval() sử dụng môi trường biến của ngữ cảnh gọi. Bất kỳ lệnh gọi nào khác - một lệnh gọi gián tiếp - đều sử dụng object toàn cục làm môi trường biến của nó và không thể đọc, ghi hoặc định nghĩa các biến hoặc hàm cục bộ. (Cả lệnh gọi trực tiếp và gián tiếp đều chỉ có thể định nghĩa các biến mới bằng var. Việc sử dụng let và const bên trong một chuỗi được đánh giá tạo ra các biến và hằng số là cục bộ đôi với việc đánh giá và không làm thay đổi môi trường gọi hoặc toàn cục)
    
    ```jsx
    const geval = eval; // Sử dụng một tên khác thực hiện một global eval
    let x = "global", y = "global"; // Hai biến toàn cục
    function f() { // Hàm này thực hiện một local eval
        let x = "local"; // Định nghĩa một biến cục bộ
        eval("x += 'changed';"); // Direct eval đặt biến cục bộ
        return x; // Trả về biến cục bộ đã thay đổi
    }
    function g() { // Hàm này thực hiện một global eval
        let y = "local"; // Một biến cục bộ
        geval("y += 'changed';"); // Indirect eval đặt biến toàn cục
        return y; // Trả về biến cục bộ không thay đổi
    }
    console.log(f(), x); // Biến cục bộ đã thay đổi: in "localchanged global":
    console.log(g(), y); // Biến toàn cục đã thay đổi: in "local globalchanged": 
    ```
    
- Lưu ý rằng khả năng thực hiện global eval không chỉ là một sự điều chỉnh cho nhu cầu của trình tối ưu hoá; nó thực sự là một tính năng cực kỳ hữu ích cho phép bạn thực thi các chuỗi code như thể chung là các tập lệnh độc lập, cấp cao nhất. Như đã lưu ý ở đầu phần này, hiếm khi thực sự cần đánh giá một chuỗi code. Nhưng nếu bạn thấy cần thiết, bạn có nhều khả năng muốn thực hiện global eval hơn là local eval

### **4.12.3 Strict eval()**

- Chế độ nghiêm ngặt (xem 5.6.3) áp đặt các hạn chế bổ sung đối với hành vi của hàm eval() và thậm chí đối với việc sử dụng định danh “eval”
- Khi eval() được gọi từ code ở chế độ nghiêm ngặt hoặc khi chính chuỗi code được đánh giá bắt đầu bằng chỉnh lệnh “use strict”, thì eval() sẽ thực hiện local eval với một môi trường biến riêng tư. Điều này có nghĩa là ở chế độ nghiêm ngặt, code được đánh giá có thể truy vấn và đặt các biến cục bộ, nhưng nó không thể định nghĩa các biến hoặc hàm mới trong phạm vi cục bộ
- Hơn nữa, chế độ nghiêm ngặt làm cho eval() thậm chí giống toán tử hơn bằng cách biến “eval” thành một từ dành riêng một cách hiệu quả. Bạn không được phép ghi đè hàm eval() bằng một giá trị mới. Và bạn không được phép khai báo một biến, hàm, tham số khối `catch` với tên “eval”

## 4.13 **Miscellaneous Operators**

- Js hỗ trợ một số toán tử linh tinh khác, được mô tả trong các phần sau

### 4.13.1 The Conditional Operator (?:)

- Toán tử điều kiện là toán tử ba ngôi duy nhất (ba toán hạng) trong Js và đôi khi thực sự được gọi là toán tử ba ngôi . Toán tử này đôi khi được viết là `?:`, mặc dù nó không hoàn toàn xuất hiện như vậy trong code. Vì toán tử này có 3 toán hạng, toán hạng đầu tiên nằm trước `?`, toán hạng thứ 2 nằm giữa `?` và `:`, và toán hạng thứ 3 nằm sau `:`. Nó được sử dụng như thế này
    
    ```jsx
    x > 0 ? x : -x // Giá trị tuyệt đối của x 
    ```
    
- Các toán hạng của toán tử điều kiện có thể thuộc bất kỳ loại nào. Toán hạng đầu tiên được đánh giá và hiểu là một boolean. Nếu giá trị của toán hạng đầu tiên là truthy, thì toán hạng thứ 2 được đánh giá và giá trị của nó được trả về. Nếu không, nếu toán hạng đầu tiên là sai, thì toán hạng thứ 3 được đánh giá và giá trị của nó được trả về. Chỉ một trong 2 toán hạng thứ 2 và thứ 3 được đánh giá; không bao giờ cả hai
- Mặc dù bạn có thể đạt được kết quả tương tự bằng cách sử dụng câu lệnh if (5.3.1), nhưng toán tử `?:` thường cung cấp một lôi tắt tiện dụng. Dưới đây là cách sử dụng điển hình, kiểm tra để đảm bảo rằng một biến được định nghĩa (và có một giá trị truthy, có ý nghĩa) và sử dụng nó nếu có hoặc cung cấp một giá trị mặc định nếu không
    
    ```jsx
    greeting = "hello " + (username ? username : "there"); 
    ```
    
- Điều này tương tự với câu lệnh if sau
    
    ```jsx
    greeting = "hello ";
    if (username) {
        greeting += username;
    } else {
        greeting += "there";
    } 
    ```
    

### 4.13.2 First-Defined (??)

- Toán tử giá trị đầu tiên được xác định `??` được đánh giá thành toán hạng được xác định đầu tiên của nó: nếu toán hạng bên trái của nó không phải null và không phải undefined, nó sẽ trả về giá trị đó. Nếu không, nó sẽ trả về giá trị của tón hạng bên phải. Giống như các toán tử && và ||, ?? là đoản mạch: nó chỉ đánh giá toán hạng thứ 2 của nó nếu toán hạng đầu tiên được đánh giá là null hoặc undefined. Nếu biểu thức a không có tác dụng phụ, thì biểu thức `a ?? b` tương đương với
    
    ```jsx
    (a !== null && a !== undefined) ? a : b 
    ```
    
- `??` là một lựa chọn thay thế hữu ích cho || (4.10.2) khi bạn muốn chọn toán hạng được xác định đầu tiên thay vì toán hạng truthy đầu tiên. Mặc dù || trên danh nghĩa là toán tử OR logic, nhưng nó cũng được sử dụng theo cách thành ngữ để chọn toán hạng không sai đầu tiên với mã sau
    
    ```jsx
    // Nếu maxWidth là chân lý, hãy sử dụng nó. Nếu không, hãy tìm kiếm một giá trị trong
    // đối tượng preferences. Nếu điều đó không đúng, hãy sử dụng một hằng số được mã hóa cứng.
    let max = maxWidth || preferences.maxWidth || 500; 
    ```
    
- Vấn đề với cách sử dụng thành ngữ này là số 0, chuỗi rỗng và false đều là các giá trị sai có thể hoàn toàn hợp lệ trong một số trường hợp. Trong ví dụ code này, nếu `maxWith` bằng 0, giá trị đó sẽ bị bỏ qua. Nhưng nếu chúng ta thay đổi toán tử `||` thành `??`, chúng ta sẽ kết thúc với một biểu thức trong đó số 0 là một giá trị hợp lệ
    
    ```jsx
    // Nếu maxWidth được xác định, hãy sử dụng nó. Nếu không, hãy tìm kiếm một giá trị trong
    // đối tượng preferences. Nếu điều đó không được xác định, hãy sử dụng một hằng số được mã hóa cứng.
    let max = maxWidth ?? preferences.maxWidth ?? 500; 
    ```
    
- Dưới đây là thêm các ví dụ cho thấy `??` hoạt động như thế nào khi toán hạng đầu tiên là false. Nếu toán hạng đó là sai nhưng được xác định, thì `??` trả về nó. Chỉ khi toán hạng đầu tiên là “nullish” (tức là null hoặc undefined) thì toán tử này mới đánh giá và trả về toán hạng thứ 2
    
    ```jsx
    let options = { timeout: 0, title: "", verbose: false, n: null };
    options.timeout ?? 1000 // => 0: như được định nghĩa trong đối tượng
    options.title ?? "Untitled" // => "": như được định nghĩa trong đối tượng
    options.verbose ?? true // => false: như được định nghĩa trong đối tượng
    options.quiet ?? false // => false: thuộc tính không được định nghĩa
    options.n ?? 10 // => 10: thuộc tính là null 
    ```
    
- Lưu ý rằng các biểu thức timeout, title và verbose ở đây sẽ có các giá trị khác nhau nếu chúng ta sử dụng `||` thay vì `??`
- Toán tử `??` tương tự như các toán tử `&&` và `||` nhưng không có độ ưu tiên cao hơn hoặc thấp hơn chúng. Nếu bạn sử dụng nó trong một biểu thức với một trong 2 toán tử đó, bạn phải sử dụng dấu ngoặc đơn rõ ràng để chỉ định thao tác nào bạn muốn thực hiện trước
    
    ```jsx
    (a ?? b) || c // ?? trước, sau đó ||
    a ?? (b || c) // || trước, sau đó ??
    a ?? b || c // SyntaxError: yêu cầu dấu ngoặc đơn 
    ```
    
- Toán tử `??` được xác định bởi ES2020 và kể từ đầu năm 2020 mới được hỗ trợ bởi các phiên bản hiện tại hoặc phiên bản beta của tất cả các trình duyệt chính. Toán tử này được gọi chính thức là toán tử “hợp nhất nullish”, nhưng tôi tránh thuật ngữ đó vì toán tử này chọn một trong các toán hạng của nó nhưng không “hợp nhất” chúng theo bất kỳ cách nào mà tôi có thể thấy

### 4.13.3 The typeof Operator

- `typeof` là một toán tử đơn nhất được đặt trước toán hạng duy nhất của nó, có thể thuộc bất kỳ loại nào. Giá trị của nó là một chuỗi chỉ định kiểu của toán hạng. Bảng 4-3 chỉ định giá trị của toán tử `typeof` cho bất kỳ giá trị Js nào
    
    ```jsx
    Bảng 4-3. Giá trị được trả về bởi toán tử typeof
    
    x	typeof x
    undefined	"undefined"
    null	"object"
    true hoặc false	"boolean"
    bất kỳ số hoặc NaN	"number"
    bất kỳ BigInt	"bigint"
    bất kỳ chuỗi	"string"
    bất kỳ symbol	"symbol"
    bất kỳ hàm	"function"
    bất kỳ đối tượng không phải hàm	"object"
    ```
    
- Bạn có thể sử dụng toán tử typeof trong một số biểu thức sau
    
    ```jsx
    // Nếu giá trị là một chuỗi, hãy đặt nó trong dấu ngoặc kép, nếu không, hãy chuyển đổi
    (typeof value === "string") ? "'" + value + "'" : value.toString() 
    ```
    
- Lưu ý rằng, typeof trả về “object” nếu giá trị toán hạng là null. Nếu bạn muốn phân biệt null với các object, bạn phải kiểm tra rõ ràng giá trị trường hợp đặt biệt này
- Mặc dù các function Js là một loại object, nhưng toán tử typeof coi các hàm đủ khác biệt để chúng có giá trị trả về riêng
- Vì typeof được đánh giá là “object” cho tất cả các giá trị object và array khác với function, nên nó chỉ hữu ích để phân biệt object với các kiểu nguyên thuỷ khác. Để phân biệt một class object này với một class object khác, bạn phải sử dụng kỹ thuật khác, chẳng hạn như toán tử `instanceof` (4.9.4) hoặc thuộc tính hàm tạo (xem 9.2.2 và 14.3)

### 4.13.4 The delete Operator

- `delete` là một toán tử đơn nhất cố gắng xoá property object hoặc element array được chỉ định làm toán hạng của nó. Giống như các toán tử gán, tăng và giảm, `delete` thường được sử dụng cho tác dụng phụ xoá property của nó chứ không phải cho giá trị mà nó trả về
    
    ```jsx
    let o = { x: 1, y: 2}; // Bắt đầu với một đối tượng
    delete o.x; // Xóa một trong các thuộc tính của nó
    "x" in o // => false: thuộc tính không còn tồn tại nữa
    let a = [1,2,3]; // Bắt đầu với một mảng
    delete a[2]; // Xóa phần tử cuối cùng của mảng
    2 in a // => false: phần tử mảng 2 không còn tồn tại nữa
    a.length // => 3: lưu ý rằng độ dài mảng không thay đổi, mặc dù 
    ```
    
- Lưu ý rằng một property hoặc 1 element mảng đã xoá không chỉ đơn thuần được đặt thành giá trị undefined. Khi một property bị xoá, thuộc tính đó sẽ không còn tồn tại. Việc cố gắng đọc 1 property không tồn tại sẽ trả về undefined, nhưng bạn có thể kiểm tra sự tồn tại thực tế của một thuộc tính bằng toán tử `in` (4.9.3). Việc xoá một phần tử mảng sẽ để lại 1 “lỗ hổng” trong mảng và không thay đổi độ dài của mảng. Mảng kết quả là thưa thớt (7.3)
- `delete` mong đợi toán hạng của nó là 1 Ivalue. Nếu nó không phải là Ivalue, toán tử sẽ không thực hiện hành động nào và trả về true. Nếu không, `delete` cố gắng xoá Ivalue đã chỉ định. `delete` trả về true nếu nó xoá thành công Ivalue đã chỉ định. Tuy nhiên, không phải tất cả các property đều có thể bị xoá: các property không thể định cấu hình (14.1) được miễn trừ khỏi việc xoá
- Ở chế độ nghiêm ngặt, `delete` sẽ tạo ra SyntaxError nếu toán hạng của nó là một định danh không đủ tiêu chuẩn chẳng hạn như biến, hàm hoặc tham số hàm: nó chỉ hoạt động khi toán hạng là một biểu thức truy cập thuộc tính (4.4). Chế độ nghiêm ngặt cũng chỉ định rằng `delete` sẽ tạo ra TypeError nếu được yêu cầu xoá bất kỳ thuộc tính nào không thể định cấu hình (tức là không thể xoá). Bên ngoài chế độ nghiêm ngặt, không có ngoại lệ nào xảy ra trong những trường hợp này và `delete` chỉ đơn giản là trả về false cho biết rằng toán hạng không thể bị xoá
    
    ```jsx
    let o = {x: 1, y: 2};
    delete o.x; // Xóa một trong các thuộc tính đối tượng; trả về true.
    typeof o.x; // Thuộc tính không tồn tại; trả về "undefined".
    delete o.x; // Xóa một thuộc tính không tồn tại; trả về true.
    delete 1; // Điều này vô nghĩa, nhưng nó chỉ trả về true.
    // Không thể xóa một biến; trả về false hoặc SyntaxError ở chế độ nghiêm ngặt.
    delete o; 
    // Thuộc tính không thể xóa: trả về false hoặc TypeError ở chế độ nghiêm ngặt.
    delete Object.prototype; 
    ```
    
- Chúng ta sẽ thấy toán tử delete một lần nữa trong 6.4

### 4.13.5 The await Operator

- `await` được giới thiệu trong ES2017 như một cách để làm cho lập trình bất đồng bộ trở nên tự nhiên hơn trong Js. Bạn cần đọc chương 13 để hiểu toán tử này. Tuy nhiên, tóm tắt lại `await` mong đợi 1 object Promise (đại diện cho một phép tính bất đồng bộ) làm toán hạng duy nhất của nó và làm cho chương trình của bạn hoạt động như thể nó đang đợi phép tính bất đồng bộ hoàn thành (nhưng nó thực hiện điều này mà không thực sự chặn và nó không ngăn cả các hoạt động bất đồng bộ khác tiến hành cùng một lúc). Giá trị của toán tử `await` là giá trị hoàn thành của object Promise. Điều quan trọng, `await` chỉ hợp pháp trong các hàm đã được khai báo là bất đồng bộ với từ khoá `async`. Một lần nữa, hãy xem chương 13 để biết đầy đủ chi tiết

### 4.13.6 The void Operator

- `void` là một toán tử đơn nhất xuất hiện trước toán hạng duy nhất của nó, có thể thuộc bất kỳ loại nào. Toán tử này là bất thường và hiếm khi được sử dụng; nó đánh giá toán hạng của nó, sau đó loại bỏ giá trị và trả về undefined. Vì giá trị toán hạng bị loại bỏ, nên việc sử dụng toán tử `void` chỉ có ý nghĩa nếu toán hạng có tác dụng phụ
- Toán tử `void` rất khó hiểu đến nỗi khó có thể đưa ra một ví dụ thực tế về cách sử dụng nó. Một trường hợp sẽ là khi bạn muốn định nghĩa một hàm không trả về gì nhưng cũng sử dụng cú pháp tắt của arrow function (8.1.3) trong đó phần thân của hàm là một biểu thức duy nhất được đánh giá và trả về. Nếu bạn đang đánh giá biểu thức chỉ để biết tác dụng phụ của nó và không muốn trả về giá trị của nó, thì điều đơn giản nhất là sử dụng dấu ngoặc nhọn xung quanh phần thân hàm. Nhưng, như một giải pháp thay thế, bạn cũng có thể sử dụng toán tử `void` trong trường hợp này
    
    ```jsx
    let counter = 0;
    const increment = () => void counter++;
    increment() // => undefined
    counter // => 1 
    ```
    

### 4.13.7 The comma Operator (,)

- Toán tử dấy phẩy là một toán tử nhị phân có các toán hạng có thể thuộc bất kỳ loại nào. Nó đánh giá toán hạng bên trái của nó, đánh giá toán hạng bên phải của nó và sau đó trả về giá trị của toán hạng bên phải. Do đó, dòng sau
    
    ```jsx
    i=0, j=1, k=2; 
    ```
    
- Được đánh giá là 2 về cơ bản tương đương với
    
    ```jsx
    i = 0; j = 1; k = 2; 
    ```
    
- Biểu thức bên trái luôn được đánh giá, nhưng giá trị của nó bị loại bỏ, có nghĩa là chỉ có ý nghĩa khi sử dụng toán tử dấu phẩy khi biểu thức bên trái có tác dụng phụ. Tình huống duy nhất mà toán tử dấu phẩy được sử dụng là với vòng lặp for (5.4.3) co nhiều biến vòng lặp
    
    ```jsx
    // Dấu phẩy đầu tiên bên dưới là một phần của cú pháp của câu lệnh let
    // Dấu phẩy thứ hai là toán tử dấu phẩy: nó cho phép chúng ta nén 2
    // biểu thức (i++ và j--) thành một câu lệnh (vòng lặp for) mong đợi 1.
    for(let i=0,j=10; i < j; i++,j--) {
        console.log(i+j);
    } 
    ```

## 4.14 Summary

- Chương này bao gồm nhiều chủ đề khác nhau và có rất nhiều tài liệu tham khảo ở đây mà bạn có thể muốn đọc lại trong tương lai khi bạn tiếp tục học Js. Tuy nhiên, một số điểm chính cần nhớ là:
    - Biểu thức là các cụm từ của một chương trình Js
    - Bất kỳ biểu thức nào cũng có thể được đánh giá thành một giá trị Js
    - Biểu thức cũng có thể có tác dụng phụ (chẳng hạn như gán biến) ngoài việc tạo ra một giá trị
    - Các biểu thức đơn giản như chữ, tham chiếu biến và truy cập thuộc tính có thể được kết hợp với các toán tử để tạo ra các biểu thức lớn hơn
    - Js định nghĩa các toán tử cho số học, so sánh, logic Boolean, phép gán và thao tác bit, cùng với một số toán tử linh tinh bao gồm cả toán tử điều kiện 3 ngôi
    - Toán tử + của Js được sử dụng để vừa cộng số vừa nối chuỗi
    - Các toán tử logic && và || có hành vi “đoản mạch” đặc biệt và đôi khi chỉ đánh giá một trong các đối số của chúng. Các thành ngữ Js phổ biến yêu cầu bạn phải tìm hiể hành vi đặc biệt của các toán tử này
