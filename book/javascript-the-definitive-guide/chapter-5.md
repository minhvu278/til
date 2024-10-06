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

## 5.4 Loops

- Để hiểu về các câu lệnh điều kiện, chúng ta đã tưởng tượng trình thông dịch Js đi theo một đường dẫn phân nhánh thông qua code của bạn. Các câu lệnh lặp là những câu lệnh bẻ cong đường dẫn đó trở lại chính nó để lặp lại phần code của bạn. JS có 5 câu lệnh lặp: `while, do/while, for, for/of (và biến thể for/await của nó) và for/in` . Các phần phụ sau đây giải thích lần lượt từng phần. Một cách sử dụng phổ biến cho các vòng lặp lại là các element của một mảng 7.6 thảo luận chi tiết về loại vòng lặp này và đề cập đến các phương thức lặp đặc biệt được định nghĩa bởi class Array

### 5.4.1 while

- Cũng giống như câu lệnh if là điều kiện cơ bản của Js, câu lệnh while là vòng lặp cơ bản của Js
    
    ```jsx
    while (expression)
    statement
    ```
    
- Để thực thi câu lệnh while, trình thông dịch trước tiên ước lượng expression. Nếu giá trị biểu thức là falsy, thì trình thông dịch bỏ qua câu lệnh đóng vai trò là phần thân của vòng lặp và chuyển sang câu lệnh tiếp theo trong chương trình. Mặc khác, nếu là truthy, trình thông dịch sẽ thực thi câu lệnh và lặp lại, nhảy trở ngược lại đầu vòng lặp và ước lượng lại `expression`. Một cách khác để nói điều này là trình thông dịch thực thi `statement` lặp đi lặp lại khi `expression` là truthy. Lưu ý rằng, bạn có thể tạo ra 1 vòng lặp vô hạn với cú pháp while (true)
- Thông thường, bạn không muốn Js thực hiện chính xác một vùng thao tác lặp đi lặp lại. Trong hầu hết mọi vòng lặp, một hoặc nhiều biến thay đổi với mỗi lần của vòng lặp. Vì các biến thay đổi, nên các hành động được thực hiện bằng cách thực thi statement có thể khác nhau mỗi khi lặp qua vòng lặp. Hơn nữa, nếu biến hoặc các biến đang thay đổi có liên quan đến expression, thì giá trị biểu thức có thể khác nhau mỗi khi lặp qua vòng lặp. Điều này rất quan trọng; nếu không, một biểu thức bắt đầu là truthy sẽ không bao giờ thay đổi và vòng lặp sẽ không bao giờ kết thúc! Dưới đây là ví dụ về vòng lặp while in ra các số từ 0 đến 9
    
    ```jsx
    let count = 0;
    while(count < 10) {
    	console.log(count);
    	count++;
    }
    ```
    
- Như bạn có thể thấy, biến count bắt đầu từ 0 và được tăng lên mỗi khi phần thân của vòng lặp chạy. Sau khi vòng lặp đã thực thi 10 lần, biểu thức trở thành false (tức là biến count không còn nhỏ hơn 10), câu lệnh while kết thúc và trình thông dịch có thể chuyển sang câu lệnh tiếp theo trong chương trình. Nhiều vòng lặp có một biến đếm như count. Các tên biến i, j và k thường được sử dụng làm bộ đếm vòng lặp, mặc dù bạn nên sử dụng các tên mô tả hơn nếu nó làm cho code của bạn dễ hiểu hơn

### **5.4.2 do/while**

- Vòng lặp do/while này giống như vòng lặp while, ngoại trừ việc biểu thức được kiểm tra ở cuối vòng lặp chứ không phải ở đầu. Điều này có nghĩa là phần thân của vòng lặp luôn được thực thi ít nhất 1 lần
    
    ```jsx
    do
    	statement
    while (expression);
    ```
    
- Vòng lặp do/while thường ít được sử dụng hơn vòng lặp while - trong thực tế, việc chắc chắn rằng bạn muốn vòng lặp thực thi ít nhất một lần là điều không phổ biến. Dưới đây là ví dụ về vòng lặp do while
    
    ```jsx
    function printArray(a) {
    	let len = a.length, i = 0;
    	if (len === 0) {
    		console.log("Mảng trống");
    	} else {
    		do {
    			console.log(a[i]);
    		} while(++i < len);
    	}
    }
    ```
    
- Có một vài điểm khác biệt về cú pháp giữa vòng lặp do while và vòng lặp while thông thường. Đầu tiên, vòng lặp `do` yêu cầu cả từ khoá `do` (để đánh dầu phần đầu của thân vòng lặp) và từ khoá while (để đánh dấu phần cuối và giới thiệu điều kiện vòng lặp). Ngoài ra vòng lặp do phải luôn được kết thúc bằng dấu chấm phẩy. Vòng lặp while không cần dấu chấm phẩy nếu phần thân của vòng lặp được đặt trong dấu ngoặc nhọn

### **5.4.3 for**

- Câu lệnh for cung cấp một cấu trúc lặp thường thuận tiện hơn câu lệnh while. Câu lệnh for đơn giản hoá các vòng lặp theo một mẫu phổ biến. Hầu hết các vòng lặp đều có một biến đếm thuộc loại nào đó, biến này được khởi tạo trước khi vòng lặp bắt đầu và được kiểm tra trước mỗi lần lặp của vòng lặp. Cuối cùng biến đếm được tăng lên hoặc được cập nhật theo cách khác ở cuối phần thân của vòng lặp, ngay trước khi biến được kiểm tra lại. Trong loại vòng lặp này, khởi tạo, kiểm tra, cập nhật là ba thao tác quan trọng của một biến vòng lặp. Câu lệnh `for` mã hoá từng thao tác trong 3 thao tác này như một biểu thức và làm cho các biểu thức đó trở thành một phần rõ ràng của cú pháp vòng lặp
    
    ```jsx
    for(initialize ; test ; increment)
    statement
    ```
    
- initialize, test và increment  là 3 (biểu thức được phân tách bởi dấu chấm phẩy) chịu trách nhiệm khởi tạo, kiểm tra và tăng biến vòng lặp. Đặt tất cả chúng vào dòng đầu tiên của vòng lặp giúp dễ dàng hiểu vòng lặp for đang làm gì và ngăn ngừa các lỗi như quên khởi tạo hoặc tăng biến vòng lặp
- Cách đơn giản nhất để giải thích cách hoạt động của vòng lặp for là hiển thị vòng lặp while tương đương
    
    ```jsx
    initialize;
    while(test) {
    	statement
    	increment;
    }
    ```
    
- Nói cách khác, biểu thức initialize được ước lượng một lần trước khi vòng lặp bắt đầu. Để hữu ích, biểu thức này phải có tác dụng phụ (thường là phép gán). Js cũng cho phép initialize là một câu lệnh khai báo biến để bạn có thể bạn có thể khai báo và khởi tạo bộ đếm vòng lặp cùng một lúc. Biểu thức test được ước lượng trước mỗi lần lặp và kiểm soát xem phần thân của vòng lặp có được thực thi hay không. Nếu test được ước lượng thành giá trị truthy, thì câu lệnh là phần thân của vòng lặp sẽ được thực thi. Cuối cùng, biểu thức increment được ước lượng. Một lần nữa, đây là một biểu thức có tác dụng phụ để hữu ích. Nói chung, nó là một biểu thức gán hoặc nó sử dụng toán tử ++ hoặc —
- Chúng ta có thể in các số từ 0 đến 9 trong vòng lặp for như sau. So sánh với vòng lặp while được hiển thị trong phần trước
    
    ```jsx
    for(let count = 0; count < 10; count++) {
    	console.log(count);
    }
    ```
    
- Tất nhiên các vòng lặp có thể trở nên phức tạp hơn nhiều so với ví dụ đơn giản này và đôi khi nhiều biến thay đổi với mỗi lần của vòng lặp. Tình huống này là nơi duy nhất mà toán tử phẩy được dùng trong Js; nó cung cấp một cách để kết hợp nhiều biểu thức khởi tạo và tăng thành một biểu thức duy nhất thích hợp để sử dụng trong vòng lặp for
    
    ```jsx
    let i, j, sum = 0;
    for(i = 0, j = 10 ; i < 10 ; i++, j--) {
    	sum += i * j;
    }
    ```
    
- Trong tất cả các ví dụ vòng lặp của chúng ta cho đến nay, biến vòng lặp là số. Điều này khá phổ biến nhưng không cần thiết. Code sau sử dụng vòng lặp for để duyệt qua cấu trúc dữ liệu danh sách liên kết và trả về đối tượng cuối cùng trong danh sách (tức là đối tượng đầu tiên không có thuộc tính next)
    
    ```jsx
    function tail(o) { // Trả về phần đuôi của danh sách liên kết o
    	for(; o.next; o = o.next) /* empty */ ; // Duyệt qua trong khi o.next là truthy
    	return o; 
    }
    ```
    
- Lưu ý rằng code này không có biểu thức initialize. Bất kỳ biểu thức nào trong 3 biểu thức này đều có thể bị bỏ qua khỏi vòng lặp for, nhưng hai dấu chấm phẩy là bắt buộc. Nếu bạn bỏ qua biểu thức test, vòng lặp sẽ lặp mãi mãi và `for( ; ; )` là một cách khác để viết vòng lặp vô hạn giống như while(true)

### **5.4.4 for/of**

- ES6 định nghĩa một câu lệnh lặp mới: `for/of`. Loại vòng lặp mới này sử dụng từ khoá for nhưng là một loại vòng lặp hoàn toàn khác với vòng lặp for thông thường. (Nó cũng hoàn toàn khác với for in cũ hơn mà chúng ta sẽ mô tả trong 5.4.5)
- Vòng lặp for of hoạt động với các object có thể lặp lại (iterable objects). Chúng ta sẽ giải thích chính xác ý nghĩa của việc một object có thể lặp lại trong chương 12. Nhưng đối với chương này, bạn chỉ cần biết rằng mảng, chuỗi, tập hợp và map là có thể lặp lại: chúng đại diện cho một chuỗi hoặc tập hợp các phần tử mà bạn có thể lặp hoặc lặp lại thông qua việc sử dụng vòng lặp for of
- Ví dụ đây là cách chúng ta có thể sử dụng for of để lặp qua các phần tử của một mảng số và tính tổng của chúng
    
    ```jsx
    let data = [1, 2, 3, 4, 5, 6, 7, 8, 9], sum = 0;
    for(let element of data) {
    	sum += element;
    }
    sum // => 45
    ```
    
- Bề ngoài, cú pháp trông như vòng lặp for thông thường: từ khoá for được theo sau bởi dấu ngoặc đơn chứa chi tiết về những gì vòng lặp nên làm. Trong trường hợp này, dấu ngoặc đơn chứa một khai báo biến (hoặc đối với các biến được khai báo, chỉ đơn giản là tên của biến) theo sau bởi từ khoá `of` và một biểu thức ước lượng thành một object có thể lặp lại, như mảng data trong trường hợp này. Như với tất cả các vòng lặp, phần thân của vòng lặp for/of theo sau dấu ngoặc đơn thường nằm trong dấu ngoặc nhọn
- Trong đoạn code vừa hiển thị, phần thân vòng lặp chạy một lần cho mỗi phần tử của mảng data. Trước mỗi lần thực thi phần thân của vòng lặp, phần tử tiếp theo được gán cho biến element. Các phần tử mảng lặp theo thứ tự từ đầu đến cuối
- Mảng được lặp lại “trực tiếp” - những thay đổi được thực hiện trong quá trình lặp có thể ảnh hưởng đến kết quả của lần lặp. Nếu chúng ta sửa đổi code trước đó bằng cách thêm dòng `data.push(sum)` bên trong phần thân của vòng lặp, thì chúng ta tạo ra một vòng lặp vô hạn vì lần lặp sẽ không bao giờ có thể đến phần tử cuối cùng của mảng

### FOR/OF WITH OBJECTS

- Các object (theo mặc định) không thể lặp lại. Việc cố gắng sử dụng for/of trên một object thông thường sẽ đưa ra TypeError trong thời gian chạy
    
    ```jsx
    let o = { x: 1, y: 2, z: 3 };
    for(let element of o) { // Đưa ra TypeError vì o không thể lặp lại
    	console.log(element); 
    }
    ```
    
- Nếu bạn muốn lặp qua các property của một object, bạn có thể sử dụng vòng lặp for/in (được giới thiệu trong 5.4.5) hoặc sử dụng for of với method `Object.keys()`
- Điều này hoạt động vì `Object.keys()` trả về một mảng các tên thuộc tính cho một đối tượng và mảng có thể lặp lại với for of. Cũng lưu ý rằng, lần lặp này của các key của một object không phải là trực tiếp như là mảng ở ví dụ trên - những thay đổi đối với object `o` được thực hiện trong phần thân của vòng lặp sẽ không ảnh hưởng đến lần lặp. Nếu bạn không quan tâm đến các khoá của một object, bạn cũng có thể lặp qua các giá trị tương ứng của chúng như sau
    
    ```jsx
    let sum = 0;
    for(let v of Object.values(o)) {
    sum += v;
    }
    sum // => 6
    ```
    
- Và nếu bạn quan tâm đến cả key và value của các property của object, bạn có thể sử dụng for of với `Object.entries()` và destructuring assignment
    
    ```jsx
    let pairs = "";
    for(let [k, v] of Object.entries(o)) {
    pairs += k + v;
    }
    pairs // => "x1y2z3"
    ```
    
- `Object.entries()` trả về một mảng các mảng, trong đó mỗi mảng bên trong đại diện cho một cặp key và value cho một property của object. Chúng tôi sử dụng cú pháp gán destructuring trong ví dụ code này để giải nén các mảng bên trong đó thành 2 mảng riêng lẻ

### FOR/OF WITH STRINGS

- Chuỗi có thể lặp lại theo từng ký tự trong ES6
    
    ```jsx
    let frequency = {};
    for(let letter of "mississippi") {
    	if (frequency[letter]) {
    		frequency[letter]++;
    	} else {
    		frequency[letter] = 1;
    	}
    }
    frequency // => {m: 1, i: 4, s: 4, p: 2}
    ```
    
- Lưu ý rằng chuỗi được lặp lại bởi điểm mã Unicode, không phải ký tự UTF-16. Chuỗi I ❤ 🐈“ có độ dài .length là 5 (vì mỗi 2 ký tự biểu tượng cảm xúc yêu cầu 2 ký tự UTF-16 để biểu diễn). Nhưng nếu bạn lặp lại chuỗi đó bằng for of, phần thân vòng lặp sẽ chạy 3 lần, một lần cho mỗi 3 điểm code “I”, “❤️”, và “🐈”

### FOR/OF WITH SET AND MAP

- Các class `Set` và `Map` tích hợp sẵn của ES6 có thể lặp lại. Khi bạn lặp lại một `Set` bằng `for/of`, phần thân của vòng lặp sẽ chạy một lần cho mỗi phần tử của tập hợp. Bạn có thể sử dụng code như thế này để in các từ duy nhất trong một chuỗi văn bản
    
    ```jsx
    let text = "Na na na na na na na na Batman!";
    let wordSet = new Set(text.split(" "));
    let unique = [];
    for(let word of wordSet) {
    	unique.push(word);
    }
    unique // => ["Na", "na", "Batman!"]
    ```
    
- `Map` là một trường hợp thú vị vì trình vòng lặp cho một object `Map` không lặp lại các key Map hoặc các value Map, mà là các cặp key/value. Mỗi lần lặp lại, trình vòng lặp trả về một mảng có phần tử đầu tiên là key và phần tử thứ 2 là value tương ứng. Cho một Map m, bạn có thể lặp lại và destructuring các cặp key value của nó như sau
    
    ```jsx
    let m = new Map([[1, "one"]]);
    for(let [key, value] of m) {
    	key // => 1
    	value // => "one"
    }
    ```
    

### ASYNCHRONOUS ITERATION WITH FOR/AWAIT

- ES2018 giới thiệu một loại trình vòng lặp mới, được gọi là trình vòng lặp bất đồng bộ (asynchronous iterator) và một biến thể trên vòng lặp for of , được gọi là vòng lặp for/await, nhưng đây là cách nó trông giống code
    
    ```jsx
    // Đọc các khối từ một luồng có thể lặp lại bất đồng bộ và in chúng ra
    async function printStream(stream) {
    	for await (let chunk of stream) {
    		console.log(chunk);
    	}
    }
    ```
    

### 5.4.5 for/in

- Vòng lặp for in trông rất giống vòng lặp for of, với từ khoá `of` thay bằng `in`. Trong khi vòng lặp for/of yêu cầu một object có thể lặp lại sau of thì vòng lặp for/in hoạt động với bất kỳ object nào sau `in`. Vòng lặp for of là mới trong ES6 nhưng for in đã là một phần của JS ngay từ đầu (đó là lý do tại sao nó có cú pháp nghe tự nhiên hơn)
- Câu lệnh for in lặp qua tên thuộc tính của một object được chỉ định
    
    ```jsx
    for (variable in object)
    statement
    ```
    
- `variable` thường đặt tên cho một biến, nhưng nó có thể là một khai báo biến hoặc bất kỳ thứ gì phù hợp làm vế trái của một biểu thức gán. `object` là một biểu thức ước lượng thành một đối tượng. Như thường lệ, statement là câu lệnh hoặc khối câu lệnh đóng vai trò là phần thân của vòng lặp
- Và bạn có thể sử dụng vòng lặp for/in như thế này
    
    ```jsx
    for(let p in o) { // Gán tên thuộc tính của o cho biến p
    	console.log(o[p]); // In giá trị của mỗi thuộc tính
    }
    ```
    
- Để thực thi câu lệnh for/in, trình thông dịch Js trước tiên ước lượng biểu thức `object`. Nếu nó ước lượng thành null hoặc undefined, trình thông dịch sẽ bỏ qua vòng lặp và chuyển sang câu lệnh tiếp theo. Trình thông dịch bây giờ thực thi phần thân của vòng lặp một lần cho mỗi property có thể liệt kê (enumerable property) của object. Tuy nhiên, trước mỗi lần lặp, trình thông dịch ước lượng biểu thức `varibale` và gán tên thuộc tính (một giá trị chuỗi) cho nó
- Lưu ý rằng biến trong vòng lặp for/in có thể là một biểu thức tuỳ ý, miễn là nó ước lượng thành một cái gì đó phù hợp với vế trái của phép gán. Biểu thức này ước lượng mỗi lần lặp qua vòng lặp, có nghĩa là nó có thể ước lượng khác nhau mỗi lần. Ví dụ: bạn có thể sử dụng code như sau để sao chép tên của tất cả các thuộc tính object vào một mảng
    
    ```jsx
    let o = { x: 1, y: 2, z: 3 };
    let a = [], i = 0;
    for(a[i++] in o) /* empty */; 
    ```
    
- Mảng Js chỉ đơn giản là một loại object đặc biệt và index mảng là các object property có thể được liệt kê bằng vòng lặp for in. Ví dụ: theo sau code trước đó với dòng này liệt kê các index mảng 0, 1 và 2
    
    ```jsx
    for(let i in a) console.log(i);
    ```
    
- Tôi thấy rằng một nguồn lỗi phổ biến trong code của riêng tôi là việc vô tình sử dụng for in với mảng khi tôi định sử dụng for of. Khi làm việc với mảng, bạn hầu như luôn muốn sử dụng for of thay vì for in
- Vòng lặp for in không thực sự liên kết tất cả các property của một object. Nó không liệt kê các property có ký hiệu (symbols). Và trong số các property có tên là chuỗi, nó chỉ lặp qua các thuộc tính có thể liệt kê (xem 14.1). Các phương thức tích hợp sẵn khác nhau được chỉ định bởi Js cốt lõi không thể liệt kê. Ví dụ, tất cả các object đều có method `toString()`, nhưng vòng lặp for in không liệt kê thuộc tính toString này. Ngoài các method tích hợp sẵn, nhiều property của các object được tích hợp sẵn không thể liệt kê. Tất cả các object và method được định nghĩa bởi code của bạn đều có thể liệt kê theo mặc định (Bạn có thể làm cho chúng không thể liệt kê được bằng cách sử dụng các kỹ thuật được giải thích trong 14.1)
- Các property được kế thừa có thể liệt kê (xem 6.3.2) cũng được liệt kê bởi vòng lặp for in. Điều này có nghĩa là nếu bạn sử dụng vòng lặp for in và cũng sử dụng code định nghĩa các property được kế thừa bởi tất cả các object, thì vòng lặp của bạn có thể không hoạt động theo cách mà bạn mong đợi. Vì lý do này nhiều lập trình viên thích sử dụng vòng lặp for of với `Object.keys()` hơn là với vòng lặp for in
- Nếu phần thân của vòng lặp for/in xóa một thuộc tính chưa được liệt kê, thì thuộc tính đó sẽ không được liệt kê. Nếu phần thân của vòng lặp định nghĩa các thuộc tính mới trên đối tượng, thì các thuộc tính đó có thể được liệt kê hoặc không. Xem §6.6.1 để biết thêm thông tin về thứ tự mà for/in liệt kê các thuộc tính của một đối tượng.

## **5.5 Jumps**

- Một loại câu lệnh Js khác là jump. Đúng như tên gọi chúng khiến trình thông dịch Js nhảy đến một vị trí mới trong mã nguồn. Câu lệnh break làm cho câu lệnh nhảy đến cuối vòng lặp hoặc câu lệnh khác. `continue` làm cho trình thông dịch bỏ qua phần còn lại của phần thân vòng lặp và nhảy trở lại đầu vòng lặp để bắt đầu một lần lặp mới. Js cho phép các câu lệnh được đặt tên hoặc gán label, và `break` và `continue` có thể xác định vòng lặp đích hoặc label câu lệnh khác
- Câu lệnh return làm cho trình thông dịch nhảy từ một lệnh gọi hàm trở lại code đã gọi nó và cung cấp giá trị cho lệnh gọi. Câu lệnh `throw` là một loại trả về tạm thời từ hàm tạo (generator function). Câu lệnh `throw` đưa ra hoặc ném ra 1 ngoại lệ (exception) và được thiết kế để hoạt động với câu lệnh `try/catch/finally`, thiết lập 1 block code để xử lý ngoại lệ. Đây là một câu lệnh nhảy phức tạp: Khi một ngoại lệ được ném ra, trình thông dịch nhảy đến trình xử lý ngoại lệ gần nhất, có thể nằm trong cùng một hàm hoặc lên ngăn xếp cuộc gọi trong một hàm gọi
- Chi tiết về từng câu lệnh Jumps có trong các phần sau

### **5.5.1 Labeled Statements**

- Bất kỳ câu lệnh nào cũng có thể được gán label bằng cách đặt trước nó một mã định danh (identifier) và dấu hai chấm
    
    ```jsx
    identifier: statement
    ```
    
- Bằng cách gán label cho một câu lệnh, bạn đặt cho nó một cái tên mà bạn có thể sử dụng để tham chiếu đến nó ở một nơi khác trong chương trình của mình. Bạn có thể gán label cho bất kỳ câu lệnh nào, mặc dù hữu ích khi gắn nhãn cho các câu lệnh có phần thân chẳng hạn như vòng lặp và điều kiện. Bằng cách đặt tên cho một vòng lặp, bạn có thể sử dụng các câu lệnh break và continue là các câu lệnh duy nhất sử dụng label câu lệnh; chúng được đề cập trong các phần phụ sau. Dưới đây là ví dụ về vòng lặp while có label và câu lệnh continue sử dụng label
    
    ```jsx
    mainloop: while(token !== null) {
    // Mã bị bỏ qua...
    continue mainloop; // Nhảy đến lần lặp tiếp theo của vòng lặp được đặt tên
    // Mã bị bỏ qua thêm...
    }
    ```
    
- Mã định danh bạn sử dụng để gán label cho một câu lệnh có thể là bất kỳ mã định danh Js hợp pháp nào không phải là từ dành riêng. Không gian tên cho label khác với không gian tên cho biến và hàm, vì vậy bạn có thể sử dụng cùng một mã định danh làm label câu lệnh và làm tên biến hoặc hàm. Label câu lệnh chỉ được định nghĩa trong câu lệnh mà chúng áp dụng (và tất nhiên là trong các câu lệnh con của nó). Một câu lệnh có thể không cùng label với câu lệnh chứa nó, nhưng 2 câu lệnh có thể có cùng label miễn là không có câu lệnh nào được lồng vào câu lệnh kia. Các câu lệnh có label có thể tự được gán label. Trên thực tế, điều này có nghĩa là bất kỳ câu lệnh nào cũng có thể có nhiều label

### 5.5.2 break

- Câu lệnh break, được sử dụng một mình, làm cho vòng lặp hoặc câu lệnh switch gần nhất thoát ngay lập tức. Cú pháp của nó rất đơn giản
    
    ```jsx
    break;
    ```
    
- Vì nó làm cho câu lệnh switch thoát ra, nên dạng câu lệnh break này chỉ hợp pháp nếu nó xuất hiện bên trong một trong các câu lệnh này
- Bạn đã thấy các ví dụ về break trong switch. Trong vòng lặp, nó thường sử dụng để thoát ra sớm khi, vì bất kỳ lý do gì, không còn cần phải hoàn thành vòng lặp nữa. Khi một vòng lặp có các điều kiện kết thúc phức tạp thường dễ dàng hơn để triển khai một số điều kiện này bằng các câu lệnh break hơn là cố gắng biểu thị tất cả chúng trong một biểu thức vòng lặp duy nhất. Code sau tìm kiếm các phần tử của một mảng cho một giá trị cụ thể. Vòng lặp kết thúc theo các thông thường khi nó đến cuối mảng; nó kết thúc bằng câu lệnh break nếu nó tìm thấy những gì nó đang tìm kiếm trong mảng
    
    ```jsx
    for(let i = 0; i < a.length; i++) {
    	if (a[i] === target) break;
    }
    ```
    
- Js cũng cho phép từ khoá break được theo sau bởi một label câu lệnh (chỉ là mã định danh, không có dấu hai chấm)
    
    ```jsx
    break labelname;
    ```
    
- Khi break được sử dụng với một label, nó sẽ nhảy đến cuối hoặc kết thúc câu lệnh bao quanh có label được chỉ định. Đó là lỗi cú pháp khi sử dụng break ở dạng này nếu không có câu lệnh bao quanh nào có label được chỉ định. Với dạng câu lệnh break này, câu lệnh được đặt tên không nhất thiết phải là vòng lặp hay `switch`: `break` có thể thoát ra khỏi bất kỳ câu lệnh bao quanh nào. Câu lệnh này thậm chí có thể là một khối câu lệnh được nhóm trong dấu ngoặc nhọn chỉ với mục đích đặt tên cho khối bằng 1 label
- Không được phép xuống dòng giữa từ khoá break và labelname. Đây là kết quả của việc Js tự động chèn dấu chấm phẩy bị bỏ qua: nếu bạn đặt dấu kết thúc dòng giữa từ khoá break và label theo sau, Js sẽ giả định rằng bạn muốn sử dụng kiểu đơn giản, không có label của câu lệnh và coi dấu kết thúc dòng là ; (xem 2.6)
- Bạn cần dạng có label của câu lệnh break khi bạn muốn thoát khỏi một câu lệnh không phải là vòng lặp gần nhất hoặc switch
    
    ```jsx
    let matrix = getData(); // Lấy một mảng số 2D từ đâu đó
    // Bây giờ hãy tính tổng tất cả các số trong ma trận.
    let sum = 0, success = false;
    // Bắt đầu với một câu lệnh có nhãn mà chúng ta có thể thoát ra nếu xảy ra lỗi
    computeSum: if (matrix) {
    	for(let x = 0; x < matrix.length; x++) {
    		let row = matrix[x];
    		if (!row) break computeSum;
    		for(let y = 0; y < row.length; y++) {
    			let cell = row[y];
    			if (isNaN(cell)) break computeSum;
    			sum += cell;
    		}
    	}
    	success = true;
    }
    // Các câu lệnh break nhảy đến đây. Nếu chúng ta đến đây với success == false
    // thì có điều gì đó không ổn với ma trận mà chúng ta đã được cung cấp.
    // Nếu không, sum chứa tổng của tất cả các ô của ma trận.
    ```
    
- Cuối cùng, lưu ý rằng câu lệnh break, có hoặc không có label, không thể chuyển quyền điều khiển qua ranh giới hàm. Ví dụ, bạn không thể gán label cho một câu lệnh định nghĩa hàm và sau đó sử dụng label đó bên trong hàm

### **5.5.3 continue**

- Câu lệnh `continue` tương tự như câu lệnh break. Tuy nhiên khi thoát khỏi vòng lặp, continue khởi động lại vòng lặp ở lần lặp tiếp theo. Cú pháp câu lệnh continue cũng đơn giản như cú pháp break
    
    ```jsx
    continue;
    ```
    
- Câu lệnh continue cũng có thể được sử dụng với 1 label
    
    ```jsx
    continue labelname;
    ```
    
- Câu lệnh continue, ở cả dạng có nhãn và không nhãn, chỉ có thể được sử dụng ở phần thân của vòng lặp. Sử dụng nó ở bất kỳ nơi nào khác sẽ gây ra lỗi cú pháp
- Khi continue được thực thi, lần lặp hiện tại của vòng lặp bao quanh bị chấm dứt và lần lặp tiếp theo bắt đầu. Điều này có nghĩa là những điều khác nhau cho các loại vòng lặp khác nhau
    - Trong vòng lặp while, biểu thức được chỉ định ở đầu vòng lặp được kiểm tra lại và nếu nó đúng, phần thân vòng lặp sẽ được thực thi bắt đầu từ đầu
    - Trong vòng lặp do while, việc thực thi sẽ bỏ qua phần cuối cùng của vòng lặp, nơi điều kiện vòng lặp được kiểm tra lại trước khi khởi động lại vòng lặp ở đầu
    - Trong vòng lặp for, biểu thức tăng được ước lượng và biểu thức kiểm tra được kiểm tra lại để xác định xem có nên thức hiện lần lặp khác không
    - Trong vòng lặp for of hoặc for in, vòng lặp bắt đầu lại với giá trị lặp tiếp theo hoặc tên thuộc tính tiếp theo được gán cho biến được chỉ định
- Lưu ý sự khác biệt về hành vi của câu lệnh continue trong vòng lặp while và for: vòng lặp while trả về trực tiếp điều kiện của nó, nhưng vòng lặp for trước tiên ước lượng biểu thức tăng của nó và sau đó trả về điều kiện của nó. Trước đó, chúng tôi đã xem xét hành vi của vòng lặp for theo thuật ngữ của một vòng lặp while “tương đương”. Tuy nhiên vì câu lệnh continue hoạt động khác nhau đối với 2 vòng lặp này, nên thực sự không thể mô phỏng hoàn hảo vòng lặp for chỉ bằng vòng lặp while
- Ví dụ sau đây cho thấy một câu lệnh continue không có label được sử dụng để bỏ qua phần còn lại của lần lặp hiện tại của vòng lặp khi xảy ra lỗi
    
    ```jsx
    for(let i = 0; i < data.length; i++) {
    	if (!data[i]) continue; // Không thể tiếp tục với data không xác định
    	total += data[i];
    }
    ```
    
- Giống như câu lệnh break, continue có thể được sử dụng ở dạng label trong các vòng lặp lồng nhau khi vòng lặp cần khởi động lại không phải là vòng lặp bao quanh ngay lập tức. Ngoài ra cũng như break, không được phép xuống dòng giữa câu lệnh continue và label name của nó

### **5.5.4 return**

- Hãy nhớ lại các lệnh gọi hàm là biểu thức và tất cả các biểu thức đó đều có giá trị. Câu lệnh return trong 1 hàm chỉ định giá trị của các lệnh gọi của hàm đó. Dưới đây là cú pháp
    
    ```jsx
    return expression;
    ```
    
- Câu lệnh return chỉ có thể xuất hiện trong phần thân của hàm. Nó là một lỗi cú pháp nếu nó xuất hiện ở bất cứ nơi nào khác. Khi lệnh return được thực thi, hàm chứa nó sẽ trả về giá trị expression cho hàm gọi nó
    
    ```jsx
    function square(x) { return x*x; } // Một hàm có câu lệnh return
    square(2) // => 4
    ```
    
- Không có câu lệnh return, một lệnh gọi hàm chỉ đơn giản thực thi từng câu lệnh trong phần thân hàm lần lượt cho đến khi nó đến cuối hàm và sau đó trả về cho hàm gọi nó. Trong trường hợp này, biểu thức gọi được ước lượng thành undefined. Câu lệnh return thường xuất hiện dưới dạng câu lệnh cuối cùng trong hàm, nhưng nó không nhất thiết phải là câu lệnh cuối cùng: hàm trả về cho hàm gọi nó khi câu lệnh return được thực thi, ngay cả khi có các câu lệnh khác còn lại trong phần thân hàm
- Câu lệnh return cũng có thể được sử dụng mà không có biểu thức để hàm trả về undefined cho hàm gọi nó
    
    ```jsx
    function displayObject(o) {
    	// Trả về ngay lập tức nếu đối số là null hoặc không xác định.
    	if (!o) return;
    	// Phần còn lại của hàm nằm ở đây...
    }
    ```
    
- Do Js tự động chèn dấu ;, bạn không thể xuống dòng giữa từ khoá return và biểu thức theo sau nó

### **5.5.5 yield**

- Câu lệnh yield rất giống câu lệnh return nhưng chỉ được sử dụng trong các hàm tạo ES6 (xem 12.3) để tạo ra các giá trị tiếp theo trong chuỗi giá trị được tạo mà không thực sự trả về
    
    ```jsx
    // Một hàm tạo tạo ra một phạm vi số nguyên
    function* range(from, to) {
    	for(let i = from; i <= to; i++) {
    		yield i;
    	}
    }
    ```
    
- Để hiểu yield, bạn phải hiểu trình vòng lặp (iterators) và hàm tạo (generators), những thứ sẽ không được đề cập cho đến chương 12. Tuy nhiên, yield được bao gồm ở đây để đầy đủ. (Về mặt kỹ thuật, yield là một toán tử hơn là một câu lệnh, như được giải thích trong 12.4.2)

### **5.5.6 throw**

- Ngoại lệ (exception) là tín hiệu cho biết rằng một số loại điều kiện hoặc lỗi ngoại lệ đã xảy ra. Ném ra một ngoại lệ là báo hiệu một lỗi hoặc điều kiện ngoại lệ như vậy. Bắt một ngoại lệ xử lý nó - thực hiện bất kỳ hành động nào cần thiết hoặc phù hợp để khôi phục sau ngoại lệ. Trong Js, ngoại lệ được ném ra bất cứ khi nào xảy ra lỗi thời gian chạy và bất cứ khi nào chương trình ném ra một ngoại lệ một cách rõ ràng bằng cách sử dụng câu lệnh throw. Ngoại lệ được bắt bằng câu lệnh `try/catch/finally` được mô tả trong phần tiếp theo
    
    ```jsx
    throw expression;
    ```
    
- `expression` có thể ước lượng thành một giá trị thuộc bất kỳ kiểu nào. Bạn có thể ném ra một số đại diện cho mã lỗi hoặc một chuỗi chứa thông báo lỗi mà con người có thể đọc được. Class Error và các class con của nó được sử dụng khi chính trình thông dịch Js ném ra lỗi và bạn có thể sử dụng chúng. Một object Error có property name chỉ định loại lỗi và property `message` chứa chuỗi được truyền vào cho hàm tạo. Dưới đây là ví dụ về một hàm ném ra một object Error khi được gọi với một đối số không hợp lệ
    
    ```jsx
    function factorial(x) {
    	// Nếu đối số đầu vào không hợp lệ, hãy ném ra một ngoại lệ!
    	if (x < 0) throw new Error("x không được âm");
    	// Nếu không, hãy tính toán một giá trị và trả về bình thường
    	let f;
    	for(f = 1; x > 1; f *= x, x--) /* empty */ ;
    	return f;
    }
    factorial(4) // => 24
    ```
    
- Khi một ngoại lệ được ném ra, trình thông dịch Js sẽ ngay lập tức dừng thực thi chương trình bình thường và nhảy đến trình xử lý ngoại lệ gần nhất. Trình xử lý ngoại lệ được viết bằng cách sử dụng mệnh đề `catch` của câu lệnh `try/catch/finally`, được mô tả trong phần tiếp theo. Nếu block code mà ngoại lệ ném ra không có mệnh đề catch được liên kết, trình thông dịch sẽ kiểm tra block code bao quanh cao hơn tiếp theo để xem liệu nó có xử lý ngoại lệ nào được liên kết với nó hay không. Điều này tiếp tục cho đến khi tìm thấy một trình xử lý. Nếu một ngoại lệ được ném ra trong một hàm không chứa câu lệnh `try/catch/finally` để xử lý nó, thì ngoại lệ sẽ lan truyền lên code đã gọi hàm. Theo cách này, ngoại lệ được lan truyền lên thông qua cấu trúc từ vựng của các method Js và lên ngăn xếp cuộc gọi. Nếu không tìm thấy trình xử lý ngoại lệ nào, ngoại lệ sẽ được coi là lỗi và được báo cho người dùng

### **5.5.7 try/catch/finally**

- Câu lệnh `try/catch/finally` là cơ chế xử lý ngoại lệ của Js. Mệnh đề try của câu lệnh này chỉ đơn giản là định nghĩa block code mà ngoại lệ sẽ được xử lý. Khối try được theo sau bởi mệnh đề catch, là một khối lệnh được gọi khi ngoại lệ xảy ra ở bất kỳ đâu trong khối try. Mệnh đề `catch` được theo sau bởi khối finally chứa code dọn dẹp được đảm bảo sẽ thực thi, bất kỳ điều gì xảy ra trong khối try. Cả khối catch và finally đều là tuỳ chọn, nhưng khối try phải đi kèm với ít nhất một trong các khối này. Tất cả các khối try, catch và finally đều bắt đầu và kết thúc bằng dấu ngoặc nhọn. Các dấu ngoặc nhọn này là một phần bắt buộc của cú pháp và không thể bỏ qua, ngay cả khi một mệnh đề chỉ chứa một câu lệnh duy nhất
    
    ```jsx
    try {
    	// Thông thường, mã này chạy từ đầu khối đến cuối
    	// mà không gặp vấn đề gì. Nhưng đôi khi nó có thể ném ra một ngoại lệ,
    	// trực tiếp, với câu lệnh throw, hoặc gián tiếp, bằng cách gọi
    	// một phương thức ném ra ngoại lệ.
    	
    	
    }
    catch(e) {
    	// Các câu lệnh trong khối này được thực thi nếu, và chỉ nếu, khối try
    	// ném ra ngoại lệ. Các câu lệnh này có thể sử dụng biến cục bộ
    	// e để tham chiếu đến đối tượng Error hoặc giá trị khác đã bị ném ra
    	// Khối này có thể xử lý ngoại lệ bằng cách nào đó, có thể bỏ qua
    	// ngoại lệ bằng cách không làm gì hoặc có thể ném lại ngoại lệ bằng throw.
    }
    finally {
    	// Khối này chứa các câu lệnh luôn được thực thi, bất kể
    	// điều gì xảy ra trong khối try. Chúng được thực thi cho dù khối try
    	// kết thúc:
    	// 1) bình thường, sau khi đến cuối khối
    	// 2) do câu lệnh break, continue hoặc return
    	// 3) với một ngoại lệ được xử lý bởi mệnh đề catch ở trên
    	// 4) với một ngoại lệ chưa được bắt vẫn đang lan truyền
    }
    ```
    
- Lưu ý rằng từ khoá catch thường được theo sau bởi một mã định danh trong dấu ngoặc đơn. Mã định danh này giống như một tham số hàm. Khi một ngoại lệ bị bắt, giá trị được liên kết với ngoại lệ (Ví dụ object Error) được gán cho tham số này. Mã định danh được liên kết với mệnh đề catch có phạm vi khối - nó chỉ được định nghĩa trong khối catch
- Dưới đây là một ví dụ thực tế về try catch. Nó sử dụng method `fatorial()` được định nghĩa trong phần trước và các method Js phía client `prompt()` và `alert()` để nhập và xuất
    
    ```jsx
    try {
    	// Yêu cầu người dùng nhập một số
    	let n = Number(prompt("Vui lòng nhập một số nguyên dương", ""));
    	// Tính giai thừa của số, giả sử đầu vào hợp lệ
    	let f = factorial(n);
    	// Hiển thị kết quả
    	alert(n + "! = " + f);
    }
    catch(ex) { // Nếu đầu vào của người dùng không hợp lệ, chúng ta sẽ đến đây
    	alert(ex); // Cho người dùng biết lỗi là gì
    }
    ```
    
- Ví dụ này là một câu lệnh try/catch không có mệnh đề finally. Mặc dù finally không được sử dụng thường xuyên như mệnh đề catch, nhưng nó có thể hữu ích. Tuy nhiên, hành vi của nó yêu cầu giải thích thêm. Mệnh đề finally được đảm bảo sẽ được thực thi nếu bất kỳ phần nào của khối try được thực thi, bất kể code trong khối try hoàn thành như thế nào. Nó thường được sử dụng để dọn dẹp sau code trong mệnh đề try
- Trong trường hợp bình thường, trình thông dịch Js đến cuối khối try và sau đó tiến hành đến khối finally, khối này thực hiện bất kỳ thao tác dọn dẹp cần thiết nào. Nếu trình thông dịch rời khỏi khối try do câu lệnh return, continue hoặc break, thì khối finally sẽ được thực thi trước khi trình thông dịch nhảy đến đích mới của nó
- Nếu một ngoại lệ xảy ra trong khối try và có một khối catch được liên kết để xử lý ngoại lệ, thì trình thông dịch trước tiên sẽ thực thi khối catch sau đó đến finally. Nếu không có khối catch cục bộ nào để xử lý ngoại lệ, trình thông dịch trước tiên sẽ thực thi khối finally và sau đó nhảy đến mệnh đề chứa catch gần nhất
- Nếu bản thân khối finally gây ra một bước nhảy với câu lệnh return, continue, break hoặc throw bằng cách gọi 1 method ném ra ngoại lệ, trình thông dịch sẽ từ bỏ bất kỳ bước nhảy nào đang chờ xử lý và thực hiện bước nhảy mới. Ví dụ nếu mệnh đề finally ném ra một ngoại lệ, thì ngoại lệ đó sẽ thay thế bất kỳ ngoại lệ nào đang trong quá trình ném ra. Nếu mệnh đề finally đưa ra câu lệnh return, thì phương thức sẽ trả về bình thường, ngay cả khi ngoại lệ đã được ném ra và chưa được xử lý
- try và finally có thể được sử dụng cùng nhau mà không có mệnh đề catch. Trong trường hợp này, finally chỉ đơn giản là code dọn dẹp đảm bảo được thực thi, bất kể điều gì xảy ra trong khối try, bất kỳ điều gì xảy ra trong khối try. Hãy nhớ rằng chúng ta không thể hoàn toàn mô phỏng vòng lặp for bằng vòng lặp while vì câu lệnh continue hoạt động khác nhau đối với 2 vòng lặp. Nếu chúng ta thêm câu lệnh try/finally, chúng ta có thể viết vòng lặp while hoạt động như vòng lặp for và xử lý continue một cách chính xác
    
    ```jsx
    // Mô phỏng for(initialize ; test ;increment ) body;
    initialize ;
    while( test ) {
    try { body ; }
    finally { increment ; }
    }
    ```
    
- Tuy nhiên lưu ý rằng phần thân có chứa câu lệnh break hoạt động hơi khác một chút (gây ra một lần tăng thêm trước khi thoát) trong vòng lặp while so với vòng lặp for, vì vậy ngay cả với mệnh đề finally, không thể mô phỏng hoàn toàn vòng lặp for bằng while

### BARE CATCH CLAUSES

- Đôi khi bạn thấy mình đang sử dụng mệnh đề catch chỉ để phát hiện và dừng sự lan truyền của ngoại lệ, ngay cả khi bạn không quan tâm đến loại hoặc giá trị của ngoại lệ. Trong ES2019 trở lên, bạn có thể bỏ qua dấu ngoặc đơn và mã định danh và sử dụng từ khoá catch trống trong trường hợp này
    
    ```jsx
    // Giống như JSON.parse(), nhưng trả về undefined thay vì đưa ra lỗi
    function parseJSON(s) {
    	try {
    		return JSON.parse(s);
    	} catch {
    		// Có gì đó không ổn nhưng chúng tôi không quan tâm đó là gì
    		return undefined;
    	}
    }
    ```

## **5.6 Miscellaneous Statements**

- Phần này mô tả 3 câu lệnh Js còn lại - with, debugger và “use strict”

### **5.6.1 with**

- Câu lệnh with chạy một block code như thể các property của một object được chỉ định là các biến trong phạm vi code đó
    
    ```jsx
    with (object)
      statement 
    ```
    
- Câu lệnh này tạo ra một phạm vi tạm thời với các thuộc tính của object như các biến và sau đó thực thi statement  trong phạm vi đó
- Câu lệnh with bị cấm trong chế độ strict (5.6.3) và nên được coi là không khuyến khích trong chế độ non-strict: tránh sử dụng nó bất cứ khi nào có thể. Code sử dụng with rất khó để tối ưu hoá và có khả năng chạy chậm hơn đáng kể so với code tương đương được viết mà không có câu lệnh with
- Việc sử dụng phổ biến của câu lệnh with là để làm cho việc làm việc với các hệ thống phân cấp đối tượng lồng nhau sâu dễ dàng hơn. Ví dụ, trong Js phía máy khách, bạn có thể phải nhập các biểu thức như thế này để truy cập các phần tử của form HTML
    
    ```jsx
    document.forms[0].address.value
    ```
    
- Nếu bạn cần viết các biểu thức như thế này nhiều lần, bạn có thể sử dụng câu lệnh with để coi các property của object form như các biến
    
    ```jsx
    with(document.forms[0]) {
      // Truy cập trực tiếp các phần tử biểu mẫu ở đây. Ví dụ:
      name.value = "";
      address.value = "";
      email.value = "";
    }
    ```
    
- Điều này làm giảm lượng gõ bạn phải làm: bạn không còn cần phải thêm tiền tố cho mỗi tên thuộc tính form bằng `document.forms[0]`. Tất nhiên, cũng đơn giản là tránh câu lệnh with và viết code trước đó như thế này
    
    ```jsx
    let f = document.forms[0];
    f.name.value = "";
    f.address.value = "";
    f.email.value = "";
    ```
    
- Lưu ý rằng nếu bạn sử dụng const hoặc let hoặc var để khai báo một biến hoặc hằng số trong phần thân của câu lệnh with, nó sẽ tạo ra một biến thông thường và không định nghĩa một thuộc tính mới trong object được chỉ định

### **5.6.2 debugger**

- Câu lệnh debugger thường không làm gì cả. Tuy nhiên, nếu có sẵn một chương trình debugger và đang chạy, thì việc triển khai có thể (nhưng không bắt buộc) thực hiện một số hành động gỡ lỗi. Trong thực tế, câu lệnh này hoạt động giống như một điểm dừng: việc thực thi code Js dừng lại và bạn có thể dùng trình gỡ lỗi để in ra giá trị của các biến, kiểm tra ngăn xếp cuộc gọi,… Ví dụ giả sử bạn đang gặp ngoại lệ trong hàm `f()` của mình vì nó đang được gọi với một đối số không xác định và bạn không thể tìm ra nơi cuộc gọi này đến từ đâu. Để giúp bạn gỡ lỗi sự cố này, bạn có thể thay đổi `f()` để nó bắt đầu như thế này
    
    ```jsx
    function f(o) {
      if (o === undefined) debugger; // Dòng tạm thời cho mục đích gỡ lỗi
      ... // Phần còn lại của hàm nằm ở đây.
    }
    ```
    
- Bây giờ khi `f()` được gọi mà không có đối số, việc thực thi sẽ dừng lại và bạn có thể sử dụng trình gỡ lỗi để kiểm tra ngăn xếp cuộc gọi và tìm ra nơi cuộc gọi không chính xác này đến từ đâu
- Lưu ý rằng việc có sẵn trình gỡ lỗi là chưa đủ: câu lệnh debugger sẽ không khởi động trình gỡ lỗi của bạn. Tuy nhiên nếu bạn đang sử dụng trình duyệt web và đã mở devtool, câu lệnh này sẽ gây ra điểm dừng

### **5.6.3 "use strict"**

- “use strict” là một chỉ thị được giới thiệu trong ES5. Các chỉ thị không phải là câu lệnh (nhưng đủ để “use strict” được ghi lại ở đây). Có 2 điểm khác biệt quan trọng giữa chỉ thị “use strict” và các câu lệnh thông thường
    - Nó không bao gồm bất kỳ từ khoá ngôn ngữ nào: chỉ thị là một câu lệnh biểu thức bao gồm một chuỗi ký tự đặc biệt (trong dấu ngoặc đơn hoặc ngoặc kép)
    - Nó chỉ có thể xuất hiện ở đầu tệp hoặc ở đầu phần thân hàm, trước khi bấ kỳ câu lệnh thực nào xuất hiện
- Mục đích của chỉ thị “use strict” là để chỉ ra rằng code sau (trong tập lệnh hoặc hàm) là code strict. Mã cấp cao nhất (phi hàm) của tập lệnh là mã strict nếu tập lệnh có chỉ thị “use strict”. Phần thân hàm là mã strict nếu nó được định nghĩa trong mã strict hoặc nếu nó có chỉ thị “use strict”. Mã được chuyển đến method eval() là mã strict nếu eval() được gọi từ mã strict hoặc bao gồm chuỗi trên. Ngoài mã được khai báo rõ ràng là strict, bất kỳ mã nào trong phần thân class (chương 9) hoặc module ES6 (10.3) sẽ tự động là mã strict. Điều này có nghĩa là tất cả các code của bạn được viết dưới dạng module, thì tất cả chúng sẽ tự động là strict và bạn sẽ không bao giờ cần sử dụng chỉ thị “use strict” rõ ràng
- Strict code được thực thi trong chế độ strict. Chế độ strict là một tập hợp con bị hạn chế của ngôn ngữ, khắc phục những thiết sót quan trọng của ngôn ngữ và cung cấp khả năng kiểm tra lỗi mạnh mẽ hơn và tăng cường bảo mật. Vì chế độ strict không phải là mặc định, code Js cũ vẫn sử dụng được các tính năng kế thừa thiếu sót của ngôn ngữ sẽ tiếp tục chạy chính xác. Sự khác biệt giữa chế độ strict và chế độ non-strict như sau (ba điểm đầu tiên đặc biệt quan trọng)
    - Câu lệnh with không được phép trong chế độ strict
    - Trong chế độ strict, tất cả các biến phải được khai báo: ReferenceError được ném ra nếu bạn gán một giá trị cho một định danh không phải là biến, hàm, tham số hàm, tham số mệnh đề catch hoặc thuộc tính của đối tượng toàn cục đã khai báo. (Trong chế độ non-strict, điều này ngầm định khai báo một biến toàn cục bằng cách thêm một property mới vào đối tượng toàn cục)
    - Trong chế độ strict, các hàm được gọi như hàm (chứ không phải như method) có giá trị this là undefined. (Trong chế độ non-strict, các hàm được gọi như hàm luôn được chuyển đổi thành global object làm giá trị `this` của chúng). Ngoài ra, trong chế độ strict, khi một hàm được gọi bằng `call()` hoặc `apply()` (8.7.4), giá trị this chính xác là giá trị được chuyển làm đối số đầu tiên cho call() hoặc apply(). (Trong chế độ non-strict, các giá trị null và undefined được thay thế bằng global object và các giá trị không phải là object được chuyển thành object)
    - Trong chế độ strict, các phép gán cho các thuộc tính không thể ghi và các nỗ lực tạo thuộc tính mới trên các object không thể mở rộng sẽ ném ra TypeError. (Trong chế độ non-strict, những nỗ lực này sẽ thất bại trong im lặng)
    - Trong chế độ strict, code được chuyển đến eval() không thể khai báo các biến hoặc định nghĩa các hàm trong phạm vi của người gọi như trong chế độ non-strict. Thay vào đó, các định nghĩa biến và hàm nằm trong cùng một phạm vi mới được tạo cho eval(). Phạm vi này bị loại bỏ khi eval() trả về
    - Trong chế độ strict, object **Agruments**(8.3.3) trong 1 hàm chứa một bản sao tĩnh của các giá trị được chuyển đến hàm. Trong chế độ non-strict, object Agruments có hành vi “ma thuật” trong đó các phần tử của mảng và các tham số hàm được đặt tên đều tham chiếu đến cùng một giá trị
    - Trong strict, SyntaxError được ném ra nếu toán tử delete được theo sau bởi một định danh không đủ điều kiện như biến, hàm hoặc tham số hàm. (Trong chế độ non-strict, biểu thức delete như vậy không làm gì cả và đánh giá là false)
    - Trong chế độ strict, đó là lỗi cú pháp đối với một object literal để định nghĩa hai hoặc nhiều thuộc tính bằng cùng một tên. (Trong chế độ non-strict, không có lỗi nào xảy ra.)
    - Trong chế độ strict, đó là lỗi cú pháp đối với khai báo hàm có hai hoặc nhiều tham số cùng tên. (Trong chế độ non-strict, không có lỗi nào xảy ra.)
    - Trong chế độ strict, octal integer literals (bắt đầu bằng số 0 không được theo sau bởi x) không được phép. (Trong chế độ non-strict, một số triển khai cho phép octal literals .)
    - Trong chế độ strict, các định danh **eval** và **arguments** được coi như các từ khóa và bạn không được phép thay đổi giá trị của chúng. Bạn không thể gán giá trị cho các định danh này, khai báo chúng như biến, sử dụng chúng như tên hàm, sử dụng chúng như tên tham số hàm hoặc sử dụng chúng như định danh của khối **catch**.
    - Trong chế độ strict, khả năng kiểm tra ngăn xếp cuộc gọi bị hạn chế. **arguments.caller** và **arguments.callee** đều ném ra **TypeError** trong một hàm chế độ strict. Các hàm chế độ strict cũng có các thuộc tính **caller** và **arguments** ném ra **TypeError** khi đọc. (Một số triển khai định nghĩa các thuộc tính không chuẩn này trên các hàm non-strict.)

## **5.7 Declarations**

- Các từ khoá const, let, var, function, class, import và export về mặt kỹ thuật không phải là câu lệnh, nhưng chúng rất giống câu lệnh và cuốn sách này gọi chúng một cách không chính thức là câu lệnh, vì vậy chúng đang được đề cập đến trong chương này
- Các từ khoá này được mô tả chính xác hơn là khai báo hơn là câu lệnh. Chúng ta đã nói ở đầu chương này rằng các câu lệnh “làm cho điều gì đó xảy ra”. Khai báo phục vụ để xác định các giá trị mới và đặt tên cho chúng để chúng ta có thể sử dụng để tham chiếu đến các giá trị đó. Bản thân chúng không làm cho nhiều điều xảy ra, nhưng bằng cách cung cấp tên cho các giá trị, theo một nghĩa quan trọng, chúng xác định ý nghĩa của các câu lệnh khác trong chương trình của bạn
- Khi một chương trình chạy, đó là các biểu thức của chương trình đang được đánh giá và các câu lệnh của chương trình đang được thực thi. Các khai báo trong một chương trình không chạy theo cùng một cách: thay vào đó, chúng xác định cấu trúc của chính chương trình. Nói một cách lỏng lẻo, bạn có thể nghĩ về các khai báo là các phần của chương trình được xử lý trước khi code bắt đầu chạy
- Các khai báo Js được sử dụng để xác định hằng số, biến, hàm và class để import và export các giá trị giữa các module. Các phần phụ tiếp theo đưa ra các ví dụ về tất cả các khai báo này. Tất cả chúng đều được đề cập chi tiết hơn ở những nơi khác trong cuốn sách này

### 5.7.1 const, let và var

Các khai báo **const**, **let** và **var** được đề cập trong §3.10. Trong ES6 trở lên, **const** khai báo hằng số và **let** khai báo biến. Trước ES6, từ khóa **var** là cách duy nhất để khai báo biến và không có cách nào để khai báo hằng số. Các biến được khai báo bằng **var** được giới hạn phạm vi trong hàm chứa chứ không phải khối chứa. Điều này có thể là một nguồn gây ra lỗi và trong JavaScript hiện đại, thực sự không có lý do gì để sử dụng **var** thay vì **let**.

```jsx
const TAU = 2*Math.PI;
let radius = 3;
var circumference = TAU * radius;
```

### 5.7.2 function

Khai báo hàm được sử dụng để định nghĩa các hàm, được đề cập chi tiết trong Chương 8. (Chúng ta cũng đã thấy **function** trong §4.3, nơi nó được sử dụng như một phần của biểu thức hàm chứ không phải khai báo hàm.) Khai báo hàm trông như thế này:

```jsx
function area(radius) {
  return Math.PI * radius * radius;
}
```

Khai báo hàm tạo một đối tượng hàm và gán nó cho tên được chỉ định - **area** trong ví dụ này. Ở những nơi khác trong chương trình của chúng ta, chúng ta có thể tham chiếu đến hàm — và chạy mã bên trong nó — bằng cách sử dụng tên này. Các khai báo hàm trong bất kỳ khối mã JavaScript nào được xử lý trước khi mã đó chạy và các tên hàm được liên kết với các đối tượng hàm trong toàn bộ khối. Chúng tôi nói rằng các khai báo hàm được “nâng lên” (hoisted) bởi vì nó giống như thể tất cả chúng đã được di chuyển lên đầu bất kỳ phạm vi nào mà chúng được xác định bên trong. Kết quả là mã gọi một hàm có thể tồn tại trong chương trình của bạn trước mã khai báo hàm.

§12.3 mô tả một loại hàm đặc biệt được gọi là trình tạo (generator). Khai báo trình tạo sử dụng từ khóa **function** nhưng theo sau nó là dấu hoa thị. §13.3 mô tả các hàm không đồng bộ (asynchronous), cũng được khai báo bằng cách sử dụng từ khóa **function** nhưng được thêm tiền tố bằng từ khóa **async**.

### 5.7.3 class

Trong ES6 trở lên, khai báo **class** tạo ra một lớp mới và đặt tên cho nó để chúng ta có thể sử dụng để tham chiếu đến nó. Các lớp được mô tả chi tiết trong Chương 9. Khai báo lớp đơn giản có thể trông như thế này:

```jsx
class Circle {
  constructor(radius) { this.r = radius; }
  area() { return Math.PI * this.r * this.r; }
  circumference() { return 2 * Math.PI * this.r; }
}
```

Không giống như các hàm, khai báo lớp không được nâng lên và bạn không thể sử dụng lớp được khai báo theo cách này trong mã xuất hiện trước khai báo.

### 5.7.4 import và export

Các khai báo **import** và **export** được sử dụng cùng nhau để làm cho các giá trị được xác định trong một mô-đun mã JavaScript có sẵn trong một mô-đun khác. Mô-đun là một tệp mã JavaScript có không gian tên toàn cục riêng, hoàn toàn độc lập với tất cả các mô-đun khác. Cách duy nhất để một giá trị (chẳng hạn như hàm hoặc lớp) được xác định trong một mô-đun có thể được sử dụng trong một mô-đun khác là nếu mô-đun xác định xuất nó với **export** và mô-đun sử dụng nhập nó với **import**. Các mô-đun là chủ đề của Chương 10 và **import** và **export** được đề cập chi tiết trong §10.3.

Các chỉ thị **import** được sử dụng để nhập một hoặc nhiều giá trị từ một tệp mã JavaScript khác và đặt tên cho chúng trong mô-đun hiện tại. Các chỉ thị **import** có một số dạng khác nhau. Dưới đây là một số ví dụ:

```jsx
import Circle from './geometry/circle.js';
import { PI, TAU } from './geometry/constants.js';
import { magnitude as hypotenuse } from './vectors/utils.js';
```

Các giá trị trong một mô-đun JavaScript là riêng tư và không thể được nhập vào các mô-đun khác trừ khi chúng đã được xuất rõ ràng. Chỉ thị **export** thực hiện điều này: nó khai báo rằng một hoặc nhiều giá trị được xác định trong mô-đun hiện tại được xuất và do đó có sẵn để nhập bởi các mô-đun khác. Chỉ thị **export** có nhiều biến thể hơn chỉ thị **import**. Đây là một trong số đó:

```jsx
// geometry/constants.js
const PI = Math.PI;
const TAU = 2 * PI;
export { PI, TAU };
```

Từ khóa **export** đôi khi được sử dụng như một bộ điều chỉnh trên các khai báo khác, dẫn đến một loại khai báo phức hợp xác định một hằng số, biến, hàm hoặc lớp và xuất nó cùng một lúc. Và khi một mô-đun chỉ xuất một giá trị duy nhất, điều này thường được thực hiện với dạng đặc biệt **export default**:

```jsx
export const TAU = 2 * Math.PI;
export function magnitude(x,y) { return Math.sqrt(x*x + y*y); } 
export default class Circle { /* định nghĩa lớp được bỏ qua ở đây */ }
```

## Summary

- Chương này đã giới thiệu từng câu lệnh của ngôn ngữ Js, được tóm tắt trong bảng 5-1

**Bảng 5-1. Cú pháp câu lệnh JavaScript**

| **Câu lệnh** | **Mục đích** |
| --- | --- |
| **break** | Thoát khỏi vòng lặp hoặc **switch** trong cùng hoặc khỏi câu lệnh bao quanh được đặt tên |
| **case** | Gắn nhãn một câu lệnh trong **switch** |
| **class** | Khai báo một lớp |
| **const** | Khai báo và khởi tạo một hoặc nhiều hằng số |
| **continue** | Bắt đầu lần lặp tiếp theo của vòng lặp trong cùng hoặc vòng lặp được đặt tên |
| **debugger** | Điểm dừng trình gỡ lỗi |
| **default** | Gắn nhãn câu lệnh mặc định trong **switch** |
| **do/while** | Một lựa chọn thay thế cho vòng lặp **while** |
| **export** | Khai báo các giá trị có thể được nhập vào các mô-đun khác |
| **for** | Vòng lặp dễ sử dụng |
| **for/await** | Lặp lại không đồng bộ các giá trị của một trình vòng lặp không đồng bộ |
| **for/in** | Liệt kê các tên thuộc tính của một đối tượng |
| **for/of** | Liệt kê các giá trị của một đối tượng có thể lặp lại chẳng hạn như một mảng |
| **function** | Khai báo một hàm |
| **if/else** | Thực thi câu lệnh này hay câu lệnh khác tùy thuộc vào điều kiện |
| **import** | Khai báo tên cho các giá trị được xác định trong các mô-đun khác |
| **label** | Đặt tên cho câu lệnh để sử dụng với **break** và **continue** |
| **let** | Khai báo và khởi tạo một hoặc nhiều biến có phạm vi khối (cú pháp mới) |
| **return** | Trả về một giá trị từ một hàm |
| **switch** | Phân nhánh đa hướng đến **case** hoặc **default**: nhãn |
| **throw** | Ném ra một ngoại lệ |
| **try/catch/finally** | Xử lý ngoại lệ và dọn dẹp mã |
| **"use strict"** | Áp dụng các hạn chế chế độ strict cho tập lệnh hoặc hàm |
| **var** | Khai báo và khởi tạo một hoặc nhiều biến (cú pháp cũ) |
| **while** | Cấu trúc vòng lặp cơ bản |
| **with** | Mở rộng chuỗi phạm vi (không được dùng nữa và bị cấm trong chế độ strict) |
| **yield** | Cung cấp một giá trị để được lặp lại; chỉ được sử dụng trong các hàm trình tạo |
