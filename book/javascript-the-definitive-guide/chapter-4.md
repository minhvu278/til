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
