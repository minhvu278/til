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
