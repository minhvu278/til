# Functions
- Chương này đề cập đến các hàm Js. Hàm là khối cơ bản xây dựng nên các chương trình Js và là một đặc chưng trong hầu hết các ngôn ngữ lập trình. Bạn co thể đã quen thuộc với khái niệm về hàm dưới dạng tên gọi như thủ tục con hoặc chương trình con
- Hàm là block code Js được định nghĩa một lần nhưng có thể được thực thi hoặc gọi nhiều lần. Hàm Js được tham số hoá: một định nghĩa hàm có thể bao gồm danh sách các định danh, được gọi là tham số, hoạt động như các biến cục bộ cho phần thân của hàm. Việc gọi hàm cung cấp các giá trị hoặc đối số cho các tham số của hàm. Hàm thường sử dụng các giá trị đối số của chúng để tính toán giá trị trả về, giá trị này trở thành giá trị của biểu thức gọi hàm. Ngoài các đối số, mỗi lần gọi đều có một giá trị khác - ngữ cảnh gọi (context) - đó là giá trị của từ khoá `this`
- Nếu một hàm được gán cho một property của object, nó được gọi là method của object đó. Khi một hàm được gọi trên hoặc thông qua một object, object đó là ngữ cảnh gọi hoặc giá trị `this` cho hàm. Các hàm được thiết kế để khởi tạo một object mới được tạo được gọi là hàm tạo (constructor). Các hàm tạo được mô tả trong 6.2 và sẽ được đề cập lại trong chương 9
- Trong Js, hàm là các object và chúng có thể được thao tác bởi các chương trình. Ví dụ, Js có thể gán các hàm cho các biết và truyền chúng cho các hàm khác. Vì các hàm là các object, bạn có thể đặt các property trên chúng và thậm chí gọi các method trên chúng
- Định nghĩa hàm Js có thể được lồng trong các hàm khác và chúng có quyền truy cập vào bất kỳ biến nào nằm trong phạm vi mà chúng được định nghĩa. Điều này có nghĩa là các hàm Js là các bao đóng và nó cho phép các kỹ thuật lập trình quan trọng và mạnh mẽ

# **8.1 Định nghĩa hàm (Defining Functions)**

- Cách đơn giản nhất để định nghĩa một hàm Js là sử dụng từ khoá function, có thể được sử dụng như một khai báo hoặc như một biểu thức. ES6 định nghĩa một cách mới quan trọng để định nghĩa các hàm mà không cần từ khoá `function`: “arrow function” có cú pháp đặc biệt gọn nhẹ và hữu ích khi truyền một hàm làm đối số cho một hàm khác. Các tiểu mục sau đây đề cập đến ba cách định nghĩa hàm này. Lưu ý rằng một số chi tiết về cú pháp định nghĩa hàm liên quan đến các tham sô được hoãn lại đến 8.3
- Trong các object literal và định nghĩa class, có một cú pháp viết tắt thuận tiện để định nghĩa các method. Cú pháp viết tắt này đã được đề cập trong 6.10.5 và tương đương với việc sử dụng biểu thức định nghĩa hàm và gán nó cho một property bằng cách sử dụng cú pháp object literal cơ bản `name:value`. Trong một trường hợp đặc biệt khác, bạn có thể sử dụng các từ khoá `get` và `set` trong các object literal để định nghĩa các method getter và setter thuộc tính đặc biệt. Cú pháp định nghĩa hàm này đã được đề cập trong 6.10.6
- Lưu ý rằng các hàm cũng có thể được định nghĩa bằng hàm tạo `Function()`, là chủ đề của 8.7.7. Ngoài ra, Js định nghĩa một số loại hàm chuyên biệt. `function*` định nghĩa các hàm tạo (xem chương 12) và `async function` định nghĩa các hàm không đồng bộ (xem Chương 13)

## **8.1.1 Khai báo hàm (Function Declarations)**

- Khai báo hàm bao gồm tử khoá function, theo sau là các thành phần này:
    - Một định danh đặt tên cho hàm. Tên là phần bắt buộc của khai báo hàm: nó được sử dụng làm tên của một biến và object function mới được định nghĩa được gán cho biến đó
    - Một cặp dấu ngoặc đơn xung quanh danh sách phân tách bằng dấu phẩy của không hoặc nhiều định danh. Các định danh này là tên tham số cho hàm và chúng hoạt động giống như các biến cục bộ trong phần thân của hàm
    - Một cặp dấu ngoặc nhọn với không hoặc nhiều câu lệnh Js bên trong. Các câu lệnh này là phần thân của hàm: chúng được thực thi bất cứ khi nào hàm được gọi
    
    ```jsx
    // In tên và giá trị của mỗi thuộc tính của o. Trả về undefined.
    function printprops(o) {
    	for(let p in o) {
    		console.log(`${p}: ${o[p]}\n`);
    	}
    }
    
    // Tính toán khoảng cách giữa các điểm Descartes (x1,y1) và (x2,y2).
    function distance(x1, y1, x2, y2) {
    	let dx = x2 - x1;
    	let dy = y2 - y1;
    	return Math.sqrt(dx*dx + dy*dy);
    }
    
    // Một hàm đệ quy (một hàm tự gọi chính nó) tính toán giai thừa
    // Nhớ lại rằng x! là tích của x và tất cả các số nguyên dương nhỏ hơn nó.
    function factorial(x) {
    	if (x <= 1) return 1;
    	return x * factorial(x-1);
    }
    ```
    
- Một trong những điều quan trọng cần hiểu về khai báo hàm là tên của hàm trở thành một biến có giá trị là chính hàm đó. Các câu lệnh khai báo được “nâng lên” đầu tập lệnh, hàm hoặc khối bao quanh để các hàm được định nghĩa theo cách này có thể được gọi từ code xuất hiện trước khi định nghĩa. Nói cách khác, tất cả các hàm được khai báo trong một block code Js sẽ được định nghĩa trong toàn bộ block code đó và chúng sẽ được định nghĩa trước khi trình thông dịch Js bắt đầu thực thi bất kỳ code nào trong block đó
- Các hàm `distance()` và `factorial()` mà chúng tôi đã mô tả được thiết kế để tính toán một giá trị và chúng sử dụng `return` để trả về giá trị đó cho hàm gọi nó. Câu lệnh `return` khiến hàm ngừng thực thi và trả về giá trị của biểu thức của nó (nếu có) cho hàm gọi. Nếu câu lệnh `return` không có biểu thức được liên kết, thì giá trị trả về của hàm là `undefined`
- Hàm `printprops()` thì khác: công việc của nó là xuất ra tên và giá trị của các property của một object. Không cần giá trị trả về và hàm không bao gồm câu lệnh `return`. Giá trị của việc gọi hàm `printprops()` luôn là `undefined`. Nếu một hàm không chứa câu lệnh `return`, nó chỉ đơn giản thực thi từng câu lệnh trong phần thân hàm cho đến khi đến cuôi và trả về giá trị undefined cho hàm gọi
- Trước ES6, khai báo hàm chỉ được phép ở cấp cao nhất trong một file Js hoặc trong một hàm khác. Trong khi một số triển khai bẻ cong quy tắc, nhưng về mặt kỹ thuật, việc định nghĩa các hàm bên trong phần thân của vòng lặp, điều kiện hoặc các block khác là không hợp lệ. Tuy nhiên, ở chế độ nghiêm ngặt của ES6, khai báo hàm được phép trong các block. Tuy nhiên, một hàm được định nghĩa trong một block chỉ tồn tại trong khối đó và không hiển thị ra bên ngoài block

## **8.1.2 Biểu thức hàm (Function Expressions)**

- Biểu thức hàm trông rất giống khai báo hàm, nhưng chúng xuất hiện trong ngữ cảnh của một biểu thức hoặc câu lệnh lớn hơn và tên là tuỳ chọn. Dưới đây là một số ví dụ về biểu thức hàm
    
    ```jsx
    // Biểu thức hàm này định nghĩa một hàm bình phương đối số của nó.
    // Lưu ý rằng chúng ta gán nó cho một biến
    const square = function(x) { return x*x; };
    
    // Biểu thức hàm có thể bao gồm tên, điều này rất hữu ích cho đệ quy.
    const f = function fact(x) { if (x <= 1) return 1; else return x*fact(x-1); };
    
    // Biểu thức hàm cũng có thể được sử dụng làm đối số cho các hàm khác:
    [3,2,1].sort(function(a,b) { return a-b; });
    
    // Biểu thức hàm đôi khi được định nghĩa và gọi ngay lập tức:
    let tensquared = (function(x) {return x*x;}(10));
    ```
    
- Lưu ý rằng tên hàm là tuỳ chọn cho các hàm được định nghĩa là biểu thức và hầu hết các biểu thức hàm trước đó mà chúng tôi đã hiển thị đều bỏ qua nó. Một khai báo hàm thực sự khai báo một biến và gán một object hàm cho nó. Mặt khác, biểu thức hàm không khai báo một biến: bạn có thể tự gán object hàm mới được định nghĩa cho một hằng số hoặc biến nếu bạn cần tham chiếu đến nó nhiều lần. Đó là một thực tế tốt để sử dụng `const` với các biểu thức hàm để bạn không vô tình ghi đè lên các hàm của mình bằng cách gán các giá trị mới
- Một tên được cho phép cho các hàm, như hàm `factorial` , cần tham chiếu đến chính nó. Nếu một biểu thức hàm bao gồm một tên, phạm vi hàm cục bộ cho hàm đó sẽ bao gồm một ràng buộc của tên đó với object hàm. Trên thực tế, tên hàm trở thành một biến cục bộ trong hàm. Hầu hết các hàm được định nghĩa là biểu thức không cần tên, điều này làm cho định nghĩa của chúng gọn gàng hơn (mặc dù không gọn gàng bằng arrow function, được mô tả ở bên dưới)
- Có một sự khác biệt quan trọng giữa việc định nghĩa một hàm `f()` bằng khai bao hàm và gán một hàm cho biến `f` sau khi tạo nó dưới dạng biểu thức. Khi bạn sử dụng dạng khai báo, các object hàm được tạo trước khi code chứa chúng bắt đầu chạy và các định nghĩa được nâng lên để bạn có thể gọi các hàm này từ code xuất hiện phía trên câu lệnh định nghĩa. Tuy nhiên, điều này không đúng với các hàm được định nghĩa là biểu thức: các hàm này không tồn tại cho đến khi biểu thức định nghĩa chúng thực sự được đánh giá. Hơn nữa, để gọi một hàm, bạn phải có thể tham chiếu đến nó và bạn không thể tham chiếu đến một hàm được định nghĩa là biểu thức cho đến khi nó được gán cho một biến, vì vậy các hàm được định nghĩa là biểu thức không thể được gọi trước khi chúng được định nghĩa

## **8.1.3 Hàm mũi tên (Arrow Functions)**

- Trong ES6, bạn có thể định nghĩa các hàm bằng cách sử dụng cú pháp đặc biệt gọn nhẹ được gọi là “arrow function”. Cú pháp này gợi nhớ đến ký hiệu toán học và sử dụng “mũi tên” `=>` để phân tách các tham số hàm khỏi phần thân hàm. Từ khoá `function` không được sử dụng và vì các arrow function là biểu thức thay vì câu lệnh, nên cũng không cần tên hàm. Dạng tổng quát của một hàm mũi tên là một danh sách các tham số được phân tách bằng dấu phẩy trong ngoặc đơn, theo sau là mũi tên `=>`, theo sau là phần thân hàm trong dấu ngoặc nhọn
    
    ```jsx
    const sum = (x, y) => { return x + y; };
    ```
    
- Nhưng các arrow function hỗ trợ cú pháp thậm chí còn gọn gàng hơn. Nếu phần thân của hàm là một câu lệnh `return` duy nhất, bạn có thể bỏ qua từ khoá `return`, dấu phẩy đi kèm với nó và dấu ngoặc nhọn, và viết phần thân của hàm dưới dạng biểu thức có giá trị được trả về
    
    ```jsx
    const sum = (x, y) => x + y;
    ```
    
- Hơn nũa, nếu một arrow function có chính xác một tham số, bạn có thể bỏ qua dấu ngoặc đơn xung quanh danh sách tham số
    
    ```jsx
    const polynomial = x => x*x + 2*x + 3;
    ```
    
- Tuy nhiên, lưu ý rằng một arrow function không có đối số nào phải được viết bằng một cặp dấu ngoặc đơn trống
    
    ```jsx
    const constantFunc = () => 42;
    ```
    
- Lưu ý rằng, khi viết một arrow function, bạn không được đặt một dòng mới giữa các tham số và mũi tên `=>`. Nếu không, bạn có thể kết thúc bằng một dòng như `const polynomial = x`, đây là một câu lệnh gán hợp lệ về mặt cú pháp
- Ngoài ra, nếu phần thân của hàm mũi tên của bạn là một câu lệnh `return` duy nhất nhưng biểu thức được trả về là một đối object literal, thì bạn phải đặt object literal trong dấu ngoặc đơn để tránh mơ hồ về cú pháp giữa dấu ngoặc nhọn của phần thân hàm và dấu ngoặc nhọn của object literal
    
    ```jsx
    const f = x => { return { value: x }; }; // Tốt: f() trả về một đối tượng
    const g = x => ({ value: x }); // Tốt: g() trả về một đối tượng
    const h = x => { value: x }; // Xấu: h() không trả về gì
    const i = x => { v: x, w: x }; // Xấu: Lỗi cú pháp
    ```
    
- Trong dòng thứ 3 của đoạn code này, hàm `h()` thực sự mơ hồ: code bạn định nghĩa là một object literal có thể được phân tích cú pháp như một câu lệnh được gắn nhãn, vì vậy một hàm trả về `undefined` được tạo. Tuy nhiên, trên dòng thứ 4, object literal phức tạp hơn không phải là câu lệnh hợp lệ và code bất hợp pháp này gây ra lỗi cú pháp
- Cú pháp ngắn gọn của arrow function khiến chúng trở nên lý tưởng khi bạn cần chuyển một hàm cho một hàm khác, đây là điều thường làm với các method mảng như `map(), filter() và reduce()` (xem 7.8.1)
    
    ```jsx
    // Tạo một bản sao của một mảng với các phần tử null bị xóa.
    let filtered = [1,null,2,3].filter(x => x !== null); // filtered == [1,2,3]
    
    // Bình phương một số số:
    let squares = [1,2,3,4].map(x => x*x); // squares == [1,4,9,16]
    ```
    
- Các arrow function khác với các hàm được định nghĩa theo những cách khác theo một cách quan trọng: chúng kế thừa giá trị của từ khoá `this` từ môi trường mà chúng được định nghĩa thay vì định nghĩa context gọi riêng chúng như các hàm được định nghĩa theo những cách khác. Đây là một tính năng quan trọng và rất hữu ích của các arrow function và chúng ta sẽ quay lại nó sau trong chương này. Các arrow function cũng khác với các hàm khác ở chỗ chúng không có property `prototype`, có nghĩa là chúng không thể được sử dụng làm hàm tạo cho các class mới (xem 9.2)

## **8.1.4 Hàm lồng nhau (Nested Functions)**

- Trong Js, các hàm có thể được lồng nhau trong các hàm khác
    
    ```jsx
    function hypotenuse(a, b) {
      function square(x) { return x*x; }
      return Math.sqrt(square(a) + square(b));
    }
    ```
    
- Điều thú vị về các hàm lồng nhau là các quy tắc phạm vi biến của chúng: chúng có thể truy cập các tham số và biến của hàm (hoặc các hàm) mà chúng được lồng vào đó. Ví dụ trong code được hiển thị ở đây, hàm bên trong `square()` có thể đọc và ghi các tham số a và b được định nghĩa bởi hàm bên ngoài `hypotenuse()`. Các quy tắc phạm vi này cho các hàm lồng nhau rất quan trọng và chúng ta sẽ xem xét lại chúng trong 8.6

# **8.2 Gọi Hàm (Invoking Functions)**

- Code Js tạo nên phần thân của hàm không được thực thi khi hàm được định nghĩa mà được thực thi khi nó được gọi. Hàm Js có thể được gọi theo 5 cách
    - Là các hàm
    - Là các method
    - Là các hàm tạo
    - Gián tiếp thông qua method `call()` và `apply()` của chúng
    - Ngầm định, thông qua các tính năng ngôn ngữ Js mà không xuất hiện giống như các cách gọi hàm thông thường

## **8.2.1 Gọi Hàm (Function Invocation)**

- Các hàm được gọi là các hàm hoặc là các method với một biểu thức gọi (4.5). Một biểu thức gọi bao gồm một biểu thức hàm được đánh giá thành một object hàm theo sau là dấu ngoặc đơn mở, một danh sách phân cách bằng dấu phẩy gồm không hoặc nhiều biểu thức đối số và dấu ngoặc đơn đóng. Nếu biểu thức hàm là một biểu thức truy cập property - nếu hàm là property của một object hoặc một phần tử của một mảng - thì đó là một biểu thức gọi method. Trường hợp đo sẽ được giải thích trong các ví dụ sau
    
    ```jsx
    printprops({x: 1});
    let total = distance(0,0,2,1) + distance(2,1,3,5);
    let probability = factorial(5)/factorial(13);
    ```
    
- Trong một lần gọi, mỗi biểu thức đối số (những biểu thức nằm giữa dấu ngoặc đơn) được đánh giá và các giá trị kết quả trở thành các đối số cho hàm. Các giá trị này được gán cho các tham số được đặt tên trong định nghĩa hàm. Trong phần thân của hàm, một tham chiếu đến một tham số được đánh giá thành giá trị đối số tương ứng
- Đối với cách gọi hàm thông thường, giá trị trả về của hàm trở thành giá trị của biểu thức gọi. Nếu hàm trả về vì trình thông dịch đến cuối, thì giá trị trả về là `undefined`. Nếu hàm trả về vì trình thông dịch thực thi một câu lệnh `return`, thì giá trị trả về là giá trị của biểu thức theo sau `return` hoặc là `undefined` nếu câu lệnh return không có giá trị

### **GỌI CÓ ĐIỀU KIỆN (CONDITIONAL INVOCATION)**

- Trong ES2020, bạn có thể chèn `?.` sau biểu thức hàm và trước dấu ngoặc đơn trong cách gọi hàm để chỉ gọi hàm nếu nó không phải là `null` hoặc `undefined`. Nghĩa là, biểu thức `f?.(x)` tương đương (giả sử không có tác dụng phụ) với:
    
    ```jsx
    (f !== null && f !== undefined) ? f(x) : undefined
    ```
    
    - Chi tiết đầy đủ về cú pháp gọi có điều kiện này có trong 4.5.1
- Đối với cách gọi hàm trong chế độ không nghiêm ngặt, ngữ cảnh gọi (giá trị `this`) là object toàn cục. Tuy nhiên, ở chế độ nghiêm ngặt, ngữ cảnh gọi là `undefined`. Lưu ý rằng các hàm được định nghĩa bằng cách sử dụng cú pháp arrow function hoạt động khác nhau: chúng luôn kế thừa giá trị `this` có hiệu lực ở nơi chúng được định nghĩa
- Các hàm được viết để được gọi là các hàm (và không phải là method) thường sử dụng từ khoá `this`. Tuy nhiên, từ khoá này có thể được sử dụng để xác định xem chế độ nghiêm ngặt có đang được bật không
    
    ```jsx
    // Định nghĩa và gọi một hàm để xác định xem chúng ta có đang ở chế độ nghiêm ngặt hay không.
    const strict = (function() { return !this; }());
    ```
    

### **HÀM ĐỆ QUY VÀ NGĂN XẾP (RECURSIVE FUNCTIONS AND THE STACK)**

- Hàm đệ quy là hàm, giống như hàm `factorial()` ở đầu chương này, tự gọi chính nó. Một số thuật toán, chẳng hạn như những thuật toán liên quan đến cấu trúc dữ liệu dựa trên cây, có thể được triển khai đặc biệt thanh lịch bằng các hàm đệ quy. Tuy nhiên, khi viết một hàm đệ quy, điều quan trọng là phải nghĩ đến các ràng buộc về bộ nhớ
- Khi một hàm A gọi hàm B, và sau đó hàm B gọi hàm C, trình thông dịch Js cần theo dõi ngữ cảnh thực thi cho cả 3 hàm. Khi hàm C hoàn thành, trình thông dịch cần biết vị trí tiếp tục thực thi hàm B hoàn thành, nó cần biết vị trí tiếp tục thực thi hàm A. Bạn có thể tưởng tượng các ngữ cảnh thực thi này như một ngăn xếp. Khi một hàm gọi một hàm khác, một ngữ cảnh thực thi mới được đẩy vào ngăn xếp. Khi hàm đó trả về, object ngữ cảnh thực thi nó được đẩy ra khỏi ngăn xếp
- Nếu một hàm tự gọi đệ quy 100 lần, ngăn xếp sẽ có 100 object được đẩy vào và sau đó 100 object đó được đẩy ra. Ngăn xếp cuộc gọi này chiếm bộ nhớ. Trên phần cứng hiện đại, thường có thể viết các hàm đệ quy tự gọi chính chúng hàng trăm lần. Nhưng nếu một hàm tự gọi chính nó mười nghìn lần, nó có thể sẽ không thành công với lỗi như “Vượt quá kích thước ngăn xếp cuộc gọi tối đa”

## **8.2.2 Gọi Phương thức (Method Invocation)**

- Method không khác gì là một hàm Js được lưu trữ trong một property của một object. Nếu bạn có 1 hàm `f` và 1 object `o`, bạn có thể định nghĩa một method có tên `m` của `o` bằng dòng sau
    
    ```jsx
    o.m = f;
    ```
    
- Sau khi đã định nghĩa method `m()` của object `o`, hãy gọi nó như thế này
    
    ```jsx
    o.m();
    ```
    
- Hoặc nếu `m()` mong đợi 2 đối số, bạn có thể gọi nó như thế này
    
    ```jsx
    o.m(x, y);
    ```
    
- Code trong ví dụ này là một biểu thức gọi: nó bao gồm một biểu thức hàm `o.m` và hai biểu thức đối số, `x` và `y`. Biểu thức hàm tự nó là một biểu thức truy cập proprerty và điều này có nghĩa là hàm được gọi như một method chứ không phải là một hàm thông thường
- Các đối số và giá trị trả về của một lời gọi method được xử lý chính xác như được mô tả cho cách gọi hàm thông thường. Tuy nhiên, cách gọi method khác với cách gọi hàm ở một điểm quan trọng: ngữ cảnh gọi. Các biểu thức truy cập property gồm 2 phần: một object (trường hợp này là `o`) và một tên property (`m`). Trong một biểu thức gọi method như thế này, object `o` trở thành ngữ cảnh gọi và phần thân hàm có thể tham chiếu đến object đó bằng cách sử dụng từ khoá `this`
    
    ```jsx
    let calculator = { // Một đối tượng literal
      operand1: 1,
      operand2: 1,
      add() { // Chúng ta đang sử dụng cú pháp viết tắt phương thức cho hàm này
        // Lưu ý việc sử dụng từ khóa this để tham chiếu đến đối tượng chứa.
        this.result = this.operand1 + this.operand2;
      }
    };
    calculator.add(); // Một lời gọi phương thức để tính 1+1.
    calculator.result // => 2
    ```
    
- Hầu hết các cách gọi method thường sử dụng dấu chấm để truy cập property, nhưng các biểu thức truy cập property sử dụng dấu ngoặc vuông cũng gây ra cách gọi method
    
    ```jsx
    o["m"](x,y); // Một cách khác để viết o.m(x,y).
    a[0](z) // Cũng là một cách gọi phương thức (giả sử a[0] là một hàm).
    ```
    
- Các cách gọi method cũng có thể liên quan đến các biểu thức truy cập property phức tạp hơn
    
    ```jsx
    customer.surname.toUpperCase(); // Gọi phương thức trên customer.surname
    f().m(); // Gọi phương thức m() trên giá trị trả về của f()
    ```
    
- Các method và từ khoá `this` là trung tâm của mô hình lập trình OOP. Bất kỳ hàm nào được sử dụng như một method đều được truyền một cách hiệu quả một cách hiệu quả một đối sô ngầm định - object mà no được gọi thông qua đó. Thông thường, một method thực hiện một số loại thao tác trên object đó và cú pháp gọi method là một cách thanh lịch để thể hiện thực tế là một hàm đang hoạt động trên 1 object
    
    ```jsx
    rect.setSize(width, height);
    setRectSize(rect, width, height);
    ```
    
- Các hàm giả định được gọi trong hai dòng code này có thể được thực hiện chính xác cùng một thao tác trên object (giả định) `rect`, nhưng cú pháp gọi method trong dòng đầu tiên chỉ ra rõ ràng hơn ý tưởng rằng chính object `rect` là trọng tâm chính của hoạt động
