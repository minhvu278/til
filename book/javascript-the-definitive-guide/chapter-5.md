# Statements
- Chương 4 đã mô tả các biểu thức (expressions) như là các cụm từ trong Js. Theo cách so sánh đó, các câu lệnh (statements) là các câu hoặc lệnh trong Js. Cũng giống như các câu tiếng Anh được kết thúc và phân tách bằng dấu chấm, các câu lệnh Js được kết thúc bằng dấu chấm phẩy (2.6)
- Các biểu thức được ước lượng để tạo ra một giá trị, nhưng các câu lệnh được `thực thi` để làm điều gì đó xảy ra
- Một cách để “làm cho điều gì đó xảy ra” là ước lượng một biểu thức có tác dụng phụ (side effects). Các biểu thức có tác dụng phụ, chẳng hạn như phép gán (assignments) và gọi hàm (function invocations), có thể đứng riêng lẻ như một câu lệnh và khi được sử dụng theo cách này được gọi là câu lệnh biểu thức (expression statements). Một loại câu lệnh tương tự là câu lệnh khai báo (declaration statements) dùng để khai báo các biến mới và định nghĩa các hàm mới
- Các chương trình Js không gì khác hơn là một chuỗi các câu lệnh để thực thi. Theo mặc định, trình thông dịch Js thực thi các câu lệnh này lần lượt theo thứ tự chúng được viết. Một các khác để “làm cho điều gì đó xảy ra” là thay đổi thứ tự thực thi mặc định này và Js có một số câu lệnh hoặc cấu trúc điều khiển để làm điề này
    - `Conditionals`: Các câu lệnh như if và switch làm cho trình thông dịch Js thực thi hoặc bỏ qua các câu lệnh khác tuỳ thuộc vào giá trị của một biểu thức
    - `Loops`: Các câu lệnh nhw `while` và `for` thực thi các câu lệnh khác lặp đi lặp lại
    - `Jumps`: Các câu lệnh như break, return và throw khiến trình thông dịch nhảy đến phần khác của chương trình
- Các phần sau đây mô tả các câu lệnh khác nhau trong Js và giải thích cú pháp của chúng. Bảng 5-1 ở cuối chương, tóm tắt cú pháp. Một chương trình Js đơn giản là một chuỗi các câu lệnh, được phân tách bằng dấu chấm phẩy, vì vậy, sau khi bạn đã quen thuộc với các câu lệnh của Js, bạn có thể bắt đầu viết các chương trình Js

## 5.1 **Expression Statements**

- Các loại câu lệnh đơn giản nhất trong Js là các biểu thức có tác dụng phụ. Loại câu lệnh này đã được trình bày trong chương 4
- Câu lệnh gán là một loại chính của câu lệnh biểu thức
    
    ```jsx
    greeting = "Hello " + name;
    i *= 3;
    ```
    
- Các toán tử tăng và giảm, `++` và `--`, có liên quan đến câu lệnh gán. Chúng có tác dụng phụ là thay đổi giá trị của biến, giống như thể một phép gán đã được thực hiện
    
    ```jsx
    counter++;
    ```
    
- Toán tử `delete` có tác dụng phụ quan trọng là xoá một object property. Do đó, nó hầu như luôn được sử dụng như một câu lệnh, thay vì là một phần của một biểu thức lớn hơn
    
    ```jsx
    delete o.x;
    ```
    
- Gọi hàm là một loại chính xác của câu lệnh biểu thức
    
    ```jsx
    console.log(debugMessage);
    displaySpinner(); // Một hàm giả định để hiển thị spinner trong ứng dụng web.
    ```
    
- Các câu lệnh gọi hàm này là các biểu thức, nhưng chúng có tác dụng phụ ảnh hưởng đến môi trường chủ (host environment) hoặc trạng thái chương trình và chúng được sử dụng ở đây như các câu lệnh. Nếu một hàm không có bất kỳ tác dụng phụ nào, thì việc gọi nó là vô nghĩa, trừ khi nó là một phần của một biểu thức lớn hơn hoặc một câu lệnh gán. Ví dụ, bạn sẽ không chỉ tính toán cosine và loại bỏ kết quả
    
    ```jsx
    Math.cos(x);
    ```
    
- Nhưng bạn cũng có thể tính toán giá trị và gán nó cho một biến để sử dụng sau
    
    ```jsx
    cx = Math.cos(x);
    ```

## 5.2 Compound and Empty Statements

- Cũng giống như các toán tử dấu phẩy (4.13.7) kết hợp nhiều biểu thức thành một biểu thức duy nhất, một khối lệnh (statement block) kết hợp nhiều câu lệnh thành một câu lệnh ghép duy nhất. Một khối lệnh đơn giản là 1 chuỗi các câu lệnh được đặt trong dấu ngoặc nhọn. Do đó, các dòng sau hoạt động như một câu lệnh duy nhất và có thể được sử dụng ở bất kỳ đâu mà Js mong đợi 1 câu lệnh duy nhất
    
    ```jsx
    {
    	x = Math.PI;
    	cx = Math.cos(x);
    	console.log("cos(π) = " + cx);
    }
    ```
    
- Có một vài điều cần lưu ý về khối lệnh này. Đầu tiên, nó không kết thúc bằng dấu chấm phẩy, nhưng bản thân khối không có. Thứ 2, các dòng bên trong khối được thụt lề so với dấu ngoặc nhọn bao quanh chúng. Điều này là tuỳ chọn nhưng nó làm cho code của bạn dễ đọc và dễ hiểu hơn
- Cũng giống như các biểu thức thường chứa các biểu thức con, nhiều câu lệnh chứa các câu lệnh con. Về mặt hình thức, cú pháp Js thường cho phép một câu lệnh duy nhất. Ví dụ: cú pháp vòng lặp `while` bao gồm một câu lệnh duy nhất đóng vai trò là phần thân của vòng lặp. Sử dụng một khối lệnh, bạn có thể đặt bất kỳ số lượng câu lệnh nào trong câu lệnh con duy nhất được phép này
- Một câu lệnh cho phép bạn sử dụng nhiều câu lệnh trong trường hợp cú pháp Js mong đợi 1 câu lệnh duy nhất. Câu lệnh rỗng thì ngược lại: nó cho phép bạn không bao gồm các câu lệnh nào trong trường hợp mong đợi một câu lệnh. Một câu lệnh rỗng trông sẽ như thế này
    
    ```jsx
    ;
    ```
    
- Trình thông dịch JS không thực hiện hành động nào khi nó thực thi một câu lệnh rỗng. Câu lệnh rỗng đôi khi hữu ích khi bạn muốn tạo một vòng lặp có phần thân rỗng. Hãy xem vòng for sau:
    
    ```jsx
    // Khởi tạo một mảng a
    for(let i = 0; i < a.length; a[i++] = 0) ;
    ```
    
- Trong vòng lặp này,  tất cả các công việc được thực hiện bởi biểu thức `a[i++] = 0` và không cần thân vòng lặp. Tuy nhiên cú pháp Js yêu cầu một câu lệnh làm phần thân vòng lặp, vì vậy, một câu lệnh rỗng - chỉ là một dấu chấm phẩy - được sử dụng
- Lưu ý rằng việc vô tình thêm dấu chấm phẩy sau dấu ngoặc đơn phải của vòng lặp for, while hoặc câu lệnh if có thể gây ra lỗi khó chịu và khó phát hiện. Ví dụ đoạn code sau đây có thể không thực hiện những gì tác giả dự định
    
    ```jsx
    if ((a === 0) || (b === 0)); // Oops! Dòng này không làm gì cả...
    o = null; // và dòng này luôn được thực thi.
    ```
    
- Khi bạn cố ý sử dụng câu lệnh rỗng, bạn nên chú thích code của mình theo cách làm rõ rằng bạn đang làm điều gì đó một cách có chủ ý
    
    ```jsx
    for(let i = 0; i < a.length; a[i++] = 0) /* empty */ ; 
    ```
    

## 5.3 Conditionals

- Câu lệnh điều kiện thực thi hoặc bỏ qua các câu lệnh khác tuỳ thuộc vào giá trị của một biểu thức được chỉ định. Những câu lệnh này là điểm quyết định trong code của bạn và đôi khi chúng còn được gọi là “nhánh”. Nếu bạn tưởng tượng trình thông dịch Js đang theo dõi 1 đường dẫn thông qua code của bạn, thì các câu lệnh điều kiện là những nơi mà code phân nhánh thành hai hoặc nhiều đường dẫn và trình thông dịch phải chọn đường dẫn nào để theo
- Các phần phụ sau đây giải thích điều kiện cơ bản của Js, câu lệnh if, else, switch case

### 5.3.1 if

- Câu lệnh if là câu lệnh điều khiển cơ bản cho phép Js đưa ra quyết định hoặc chính xác hơn là thực thi các câu lệnh có điều kiện. Câu lệnh này có 2 dạng. Dạng đầu tiên là
    
    ```jsx
    if (expression)
    statement
    ```
    
- Ở dạng này, `expression` được ước lượng. Nếu giá trị là truthy, `statement` được thực thi và ngược lại
    
    ```jsx
    if (username == null) // Nếu username là null hoặc undefined,
    username = "John Doe"; // định nghĩa nó
    ```
    
- Hoặc tương tự
    
    ```jsx
    // Nếu username là null, undefined, false, 0, "", hoặc NaN, hãy cung cấp cho nó một giá trị mới
    if (!username) username = "John Doe"; 
    ```
    
- Lưu ý rằng dấu ngoặc đơn xung quanh biểu thức là một phần bắt buộc của cú pháp cho câu lệnh if
- Cú pháp Js yêu cầu một câu lệnh duy nhất sau từ khoá if và biểu thức trong dấu ngoặc đơn, nhưng bạn có thể sử dụng khối lệnh để kết hợp nhiều câu lệnh thành một. Vì vậy, câu lệnh if có thể trông như thế này
    
    ```jsx
    if (!address) {
    	address = "";
    	message = "Vui lòng chỉ định địa chỉ gửi thư.";
    }
    ```
    
- Dạng thứ 2 của câu lệnh if giới thiệu mệnh đề else được thực thi khi expression là sai
    
    ```jsx
    if (expression)
    statement1
    else
    statement2
    ```
    
- Dạng câu lệnh này thực thi statement1 nếu expression là truthy và thực thi statement2 nếu expression là falsy.
    
    ```jsx
    if (n === 1)
    console.log("Bạn có 1 tin nhắn mới.");
    else
    console.log(`Bạn có ${n} tin nhắn mới.`);
    ```
    
- Khi bạn có khối lệnh if lồng nhau với mệnh đề else, cần cẩn trọng để đảm bảo rằng mệnh đề else đi với if thích hợp
    
    ```jsx
    i = j = 1;
    k = 2;
    if (i === j)
    	if (j === k)
    		console.log("i equals k");
    else
    	console.log("i doesn't equal j"); // WRONG!!
    ```
    
- Trong ví dụ này, câu lệnh if bên trong được tạo thành câu lệnh duy nhất được phép bởi cú pháp câu lệnh if bên ngoài. Thật không may, không rõ ràng (ngoại trừ việc gợi ý thụt lề) else đi với if nào. Và trong ví dụ này, thụt lề là sai bởi vì trình thông dịch Js thực sự giải thích ví dụ trước đó là
    
    ```jsx
    if (i === j) {
    	if (j === k)
    		console.log("i equals k");
    	else
    		console.log("i doesn't equal j"); // OOPS!
    }
    ```
    
- Quy tắc trong Js (như hầu hết các ngôn ngữ lập trình) là theo mặc định, mệnh đề else là một phần của câu lệnh if gần nhất. Để làm cho ví dụ này đơn giản, ít mơ hồ và dễ đọc hơn, bạn nên sử dụng dấu ngoặc nhọn
    
    ```jsx
    if (i === j) {
    	if (j === k) {
    		console.log("i equals k");
    	}
    } else { // What a difference the location of a curly brace makes!
    	console.log("i doesn't equal j");
    }
    ```
    
- Nhiều dev có thói quen đặt phần thân của câu lệnh if và else (cũng như các câu lệnh ghép khác, như while) trong dấu ngoặc nhọn, ngay cả khi phần thân chỉ bao gồm 1 câu lệnh duy nhất. Làm như vậy một cách nhất quán có thể ngăn ngừa loại vấn đề vừa được hiển thị và tôi khuyên bạn nên áp dụng và thực hiện cách này. Trong cuốn sách này, tôi ưu tiên giữ cho code ví dụ nhỏ gọn theo chiều dọc và tôi không phải lúc nào cũng làm theo lời khuyên của riêng mình về vấn đề này

### 5.3.2 else if

- Câu lệnh if else ước lượng một biểu thức và thực thi một trong 2 đoạn code, tuỳ thuộc vào kết quả. Nhưng điều gì xảy ra khi một trong nhiều đoạn code? Một trong những cách đề làm điều này là thực thi một câu lệnh else if. else if không thực sự là một câu lệnh Js, mà chỉ đơn giản là một thành ngữ lập trình được sử dụng thường xuyên khi các câu lệnh if else lặp lại được sử dụng
    
    ```jsx
    if (n === 1) {
    // Thực thi khối mã #1 
    } else if (n === 2) {
    // Thực thi khối mã #2
    } else if (n === 3) {
    // Thực thi khối mã #3
    } else {
    // Nếu tất cả đều thất bại, hãy thực thi khối #4
    }
    ```
    
- Không có gì đặc biệt về code này. Nó chỉ là một loạt các câu lệnh if , trong đó mỗi if là một phần của mệnh đề else của câu lệnh trước đó. Sử dụng thành ngữ else if thích hợp hơn và dễ đọc hơn so với việc viết các câu lệnh này ở dạng lồng nhau đầy đủ
    
    ```jsx
    if (n === 1) {
    // Thực thi khối mã #1
    }
    else {
    if (n === 2) {
    // Thực thi khối mã #2
    }
    else {
    if (n === 3) {
    // Thực thi khối mã #3
    }
    else {
    // Nếu tất cả đều thất bại, hãy thực thi khối #4
    }
    }
    }
    ```
    

### **5.3.3 switch**

- Câu lệnh if gây ra một nhánh trong luôn thực thi của chương trình và bạn có thể sử dụng thành ngữ else if để thực hiện một nhánh đa hướng. Tuy nhiên, đây không phải là giải pháp tốt nhất khi tất cả các nhánh phụ thuộc vào giá trị của cùng một biểu thức. Trong trường hợp này, việc lặp đi lặp lại ước lượng biểu thức đó trong nhiều câu lệnh if là lãng phí
- Câu lệnh `swich` xử lý chính xác tình huống này. Từ khoá switch được theo sau bởi một biểu thức trong dấu ngoặc đơn và block code trong dấu ngoặc nhọn
    
    ```jsx
    switch(expression) {
    	statements
    }
    ```
    
- Tuy nhiên cú pháp đầu đủ của câu lệnh switch phức tạp hơn thế này. Các vị trí khác nhau trong block code được gán lable bằng từ khoá case, theo sau là một biểu thức và dấu hai chấm. Khi một switch được thực thi, nó tính toán giá trị của expression và sau đó tìm kiếm 1 lable case mà biểu thức của nó ước lượng cùng giá trị (trong đó, sự giống nhau được xác định bởi toán tử ===). Nếu nó tìm thấy một, nó bắt đầu thực thi block code tại câu lệnh được gán label case. Nếu nó không tìm thấy case có giá trị khớp, nó sẽ tìm một câu lệnh được gán label default:. Nếu không có default, câu lệnh switch sẽ bỏ qua hoàn toàn block code
- switch là một câu lệnh khó giải thích; hoạt động của nó rõ ràng hơn với một ví dụ. Câu lệnh swich sau đây tương đương với các câu lệnh if else lặp lại được hiển thị trong phần trước
    
    ```jsx
    switch(n) {
    	case 1: // Bắt đầu tại đây nếu n === 1
    		// Thực thi khối mã #1.
    	break; // Dừng lại tại đây
    	case 2: // Bắt đầu tại đây nếu n === 2
    		// Thực thi khối mã #2.
    	break; // Dừng lại tại đây
    	case 3: // Bắt đầu tại đây nếu n === 3
    		// Thực thi khối mã #3.
    	break; // Dừng lại tại đây
    	default: // Nếu tất cả đều thất bại...
    		// Thực thi khối mã #4. 
    	break; // Dừng lại tại đây
    }
    ```
    
- Lưu ý từ khoá `break` được sử dụng ở cuối mỗi `case` trong code này. Câu lệnh break được mô tả ở phần sau của chương này khiến trình thông dịch nhảy đến cuối (hoặc “thoát ra”) của câu lệnh switch và tiếp tục với câu lệnh theo sau nó. Các mệnh đề case trong câu lệnh switch chỉ chỉ định điểm bắt đầu của code mong muốn; chúng không chỉ định bất kỳ điểm kết thúc nào. Trong trường hợp không có câu lệnh break, câu lệnh switch thực thi block code của nó tại label case khớp với giá trị biểu thức của nó và tiếp tục thực thi các câu lệnh cho đến khi nó đến cuối block. Trong những trường hợp hiếm hoi, sẽ hữu ích khi viết code như thế này “rơi xuyên qua” từ label case này sang label case tiếp theo, nhưng 99% thời gian bạn nên cẩn thận kết thúc mọi case bằng câu lệnh break. (Tuy nhiên khi sử dụng switch bên trong function, bạn có thể sử dụng câu lệnh return thay cho break. Cả 2 đều sử dụng để kết thúc câu lệnh switch và ngăn cho không cho việc thực thi rơi vào case tiếp theo).
- Dưới đây là một ví dụ cụ thể hơn về câu lệnh switch; nó chuyển đổi một giá trị thành một chuỗi phụ thuộc vào loại giá trị
    
    ```jsx
    function convert(x) {
    	switch(typeof x) {
    		case "number": // Chuyển đổi số thành số nguyên thập lục phân
    		return x.toString(16);
    		case "string": // Trả về chuỗi được đặt trong dấu ngoặc kép
    		return '"' + x + '"';
    		default: // Chuyển đổi bất kỳ loại nào khác theo cách thông thường 
    		return String(x);
    	}
    }
    ```
    
- Lưu ý rằng, 2 ví dụ trước, các từ khoá case được theo sau bởi các literal số và chuỗi, tương ứng. Đây là câu lệnh switch được sử dụng thường xuyên nhất trong thực tế, nhưng lưu ý rằng tiêu chuẩn ECMAScript cho phép mỗi case được theo sau bởi một biểu thức tuỳ ý
- Câu lệnh switch đầu tiên ước lượng biểu thức theo sau từ khoá switch và sau đó ước lượng các biểu thức case, theo thứ tự chúng xuất hiện, cho đến khi nó tìm thấy một giá trị khớp. `case` phù hợp được xác định bằng cách sử dụng toán tử nhận dạng ===, không phải ==, vì vậy các biểu thức phải khớp mà không cần bất kỳ chuyển đổi kiểu nào
- Vì không phải tất cả các biểu thức case đều được ước lượng mỗi khi câu lệnh switch được thực thi, bạn nên tránh sử dụng các biểu thức case có chứa các tác dụng phụ như gọi hàm hoặc gán. Cách an toàn nhất là chỉ giới hạn các biểu thức case của bạn thành các biểu thức hằng số
- Như đã giải thích trước đó, nếu không có biểu thức case nào khớp với biểu thức switch, câu lệnh switch sẽ bắt đầu thực thi phần thân của nó tại câu lệnh được gán label là `default:` . Nếu không có lable `default:`, câu lệnh switch sẽ bỏ qua phần thân của nó hoàn toàn. Lưu ý rằng trong các ví dụ được hiển thị , label default xuất hiện ở cuối phần thân của switch, theo sau tất cả các lable case. Đây là một vị trí thích hợp và phổ biến cho nó, nhưng nó có thể xuất hiện ở bất cứ đâu trong phần thân của câu lệnh
