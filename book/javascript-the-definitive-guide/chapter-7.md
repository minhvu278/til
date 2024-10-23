# Arrays

- Chương này mô tả về array, một kiểu dữ liệu cơ bản trong Js và hầu hết các ngôn ngữ lập trình khác. Array là một tập hợp có thứ tự của các giá trị. Mỗi giá trị được gọi là một phần tử (element), và mỗi phần tử có một ví trị số trong mảng được gọi là chỉ số (index)
- Array Js là không xác định kiểu (untyped): một phần tử mảng có thể thuộc bất kỳ kiểu nào và các phần tử khác nhau của cùng một mảng có thể thuộc các kiểu khác nhau. Các phần tử mảng thậm chí có thể là object hoặc các array khác, cho phép bạn tạo các cấu trúc dữ liệu phức tạp chẳng hạn như array các object và array các array
- Array Js bắt đầu từ o (zero-based) và sử dụng chỉ số 32-bit: index của phần tử đầu tiên là 0 và index cao nhất có thể là 4294967294 (2<sup>32</sup> - 2), với kích thước mảng tối đa là 4.294.967.295 phần tử.
- Array Js là động (dynamic) : Chúng phát triển hoặc thu hẹp khi cần và không cần khai báo kích thước cố định cho mảng khi bạn tạo nó hoặc cấp phát lại khi kích thước thay đổi. Array Js có thể thưa thớt (sparse): các phần tử không cần phải có index liền kề và có khoảng trống
- Mỗi array js đề có property `length`. Đổi với array không thưa thớt, property này chỉ định số lượng phần tử trong mảng. Đối với array thưa thớt, length lớn hơn index cao nhất của bất kỳ phần tử nào
- Array Js là một dạng đặc biệt của object Js, và index array thực sự chỉ là tên property là số nguyên. Chúng ta sẽ nói thêm về các đặc điểm chuyển biệt của mảng ở những phần khác trong chương này. Việc triển khai thường tối ưu hoá array để truy cập vào các phần tử array được đánh index bằng số thường nhanh hơn đáng kể so với việc truy cập vào các property object thông thường
- Array kế thừa các property từ `Array.prototype`, nơi định nghĩa một tập hợp phong phú các method các thao tác array được đề cập trong 7.8. Hầu hết các method này đều là chung chung (generic), có nghĩa là chúng hoạt động chính xác không chỉ cho array thực mà còn cho bất kỳ object nào giống array nào. Chúng ta sẽ thảo luận về các object giống mảng trong 7.9. Cuối cùng, chuỗi Js hoạt động giống như mảng các ký tự và chúng ta sẽ thảo luận điều này trong 7.10
- ES6 giới thiệu một tập hợp các class array được gọi chung là typed arrays. Không giống như array js thông thường, typed array có độ dài cố định và kiểu phần tử số cố định. Chúng cung cấp mức byte vào dữ liệu nhị phân và được đề cập trong 11.2

## **7.1 Tạo Mảng**

- Có một số cách để tạo mảng. Các phần sau sẽ giải thích cách tạo mảng bằng
    - Array literals (Lịch sử mảng)
    - Toán tử spread `...` trên một object có thể lặp lại (iterable object)
    - Hàm tạo Array()
    - Các method factory `Array.of()` và `Array.form()`

### **7.1.1 Array literals**

- Cho đến nay, cách đơn giản nhất để tạo mảng là sử dụng array literals, đơn giản là các phần tử mảng được phân tách bởi dấu phẩy trong dấu ngoặc vuông
    
    ```jsx
    let empty = []; // Một mảng không có phần tử
    let primes = [2, 3, 5, 7, 11]; // Một mảng có 5 phần tử số
    let misc = [ 1.1, true, "a", ]; // 3 phần tử thuộc nhiều kiểu khác nhau + dấu phẩy ở cuối
    ```
    
- Các giá trị trong array literals không cần phải là hằng số, chúng có thể là biểu thức tuỳ ý
    
    ```jsx
    let base = 1024;
    let table = [base, base+1, base+2, base+3];
    ```
    
- Array literal có thể chứa object literal hoặc array literal khác
    
    ```jsx
    let b = [[1, {x: 1, y: 2}], [2, {x: 3, y: 4}]];
    ```
    
- Nếu một array literal chứa nhiều dấu chấm phẩy liên tiếp, không có giá trị nào ở giữa, thì mảng đó là mảng thưa thớt (xem 7.3). Các phần tử mảng mà giá trị bị bỏ qua sẽ không tồn tại nhưng có vẻ là undefined nếu bạn truy vấn chúng
    
    ```jsx
    let count = [1,,3]; // Phần tử tại chỉ số 0 và 2. Không có phần tử tại chỉ số 1
    let undefs = [,,]; // Một mảng không có phần tử nhưng có độ dài là 2
    ```
    
- Cú pháp array literal cho phép  dấu chấm phẩy ở cuối là tuỳ chọn, vì vậy `[, ,]` có độ dài là 2 chứ không phải 3

### **7.1.2 Toán tử Spread**

- Trong ES6 trở lên, bạn có thể sử dụng toán tử spread `...` để đưa các phần tử của một mảng vào trong một array literal
    
    ```jsx
    let a = [1, 2, 3];
    let b = [0, ...a, 4]; // b == [0, 1, 2, 3, 4]
    ```
    
- Dấu 3 chấm “lan truyền” mảng a để các phần tử của nó trở thành phần tử trong array literal đang được tạo. Nó giống như thể `...a` được thay thế bởi các phần tử của mảng a, được liệt kê theo nghĩa đen như một phần của array literal bao quanh. (Lưu ý rằng, mặc dù chúng gọi ba dấu chấm này là toán tử spread, nhưng đây không phải là toán tử thực sự vì nó có thể được sử dụng trong array literal và, như chúng ta đã thấy trong cuốn sách, các lệnh gọi hàm)
- Toán tử spread là một cách thuận tiện để tạo bản sao (nông) của một mảng
    
    ```jsx
    let original = [1,2,3];
    let copy = [...original];
    copy[0] = 0; // Sửa đổi bản sao không làm thay đổi bản gốc
    original[0] // => 1
    ```
    
- Toán tử spread hoạt động trên bất kỳ object có thể lặp lại nào. (Object có thể lặp lại những gì vòng lặp for of lặp lại; chúng ta lần đầu tiên thấy chúng trong  5.4.4 và chúng ta sẽ thấy nhiều hơn trong chương 12). Chuỗi có thể lặp lại, vì vậy bạn có thể sử dụng toán tử spread để biến bất kỳ chuỗi nào thành một mảng các chuỗi ký tự đơn
    
    ```jsx
    let digits = [..."0123456789ABCDEF"];
    digits // => ["0","1","2","3","4","5","6","7","8","9","A","B","C","D","E","F"]
    ```
    

### **7.1.3 Hàm tạo Array()**

- Một cách khác đề tạo mảng là sử dụng hàm tạo Array(). Bạn có thể gọi hàm tạo này theo 3 cách khác biệt
    - **Gọi mà không có đối số**
    
    ```jsx
    let a = new Array();
    ```
    
    - Method này tạo một mảng rỗng không có phần tử và tương đương với array literal `[]`
    - **Gọi với một đối số duy nhất, chỉ định độ dài**
    
    ```jsx
    let a = new Array(10);
    ```
    
    - Kỹ thuật này tạo một mảng với độ dài được chỉ định. Hình thức này của hàm tạo Array có thể được sử dụng để phân bổ trước một mảng khi bạn biết trước cần bao nhiêu phần tử. Lưu ý rằng không có giá trị nào được lưu trữ trong mảng và các property index mảng “0”, “1”,… thậm chí không được xác định cho mảng
    - **Chỉ định rõ ràng hai hoặc nhiều phần tử của mảng hoặc một phần tử không phải là số duy nhất cho mảng**
    
    ```jsx
    let a = new Array(5, 4, 3, 2, 1, "testing, testing");
    ```
    
    - Ở dạng này, các đối số của hàm tạo trở thành các phần tử của mảng mới. Sử dụng array literal hầu như luôn đơn giản hơn với việc sử dụng hàm tạo `Array()` này

### **7.1.4 Array.of()**

- Khi hàm tạo `Array()` được gọi với một đối số, nó sẽ sử dụng đối số đó làm độ dài của mảng. Nhưng khi được gọi với nhiều hơn một đối số, nó sẽ coi các đối số đó là phần tử cho mảng sẽ được tạo. Điều này có nghĩa là hàm tạo `Array()` không thể được sử dụng để tạo một mảng với một phần tử số duy nhất
- Trong ES6, hàm `Array.of()` giải quyết vấn đề này: nó là một method factory tạo và trả về một mảng mới, sử dụng các giá trị của đối số của nó (bất kể có bao nhiêu giá trị trong đối số đó) làm phần tử của mảng
    
    ```jsx
    Array.of() // => []; trả về mảng rỗng không có đối số
    Array.of(10) // => [10]; có thể tạo mảng với một đối số số duy nhất
    Array.of(1,2,3) // => [1, 2, 3]
    ```
    

### **7.1.5 Array.from()**

- Là một factory method array khác được giới thiệu trong ES6. Nó mong đợi một object có thể lặp lại hoặc giống mảng làm đối số đầu tiên và trả về một mảng mới chứa các phần tử của object đó. Với một đối số có thể lặp lại, `Array.form(iterable)` hoạt động giống như toán tử spread `[...iterable]` hoạt động. Nó cũng là một cách đơn giản để tạo một bản sao của một mảng
    
    ```jsx
    let copy = Array.from(original);
    ```
    
- `Array.from()` cũng rất quan trọng vì nó xác định cách tạo bản sao mảng thực sự của một object giống mảng. Object giống mảng là các object. Object giống mảng là các object không phải là mảng có property độ dài số và có các giá trị được lưu trữ với các property mà tên của chúng tình cờ là số nguyên. Khi làm việc với Js phía client, giá trị trả về của một số method trình duyệt web là giống mảng và bạn có thể dễ dàng làm việc với chúng hơn nếu bạn chuyển đổi thành mảng thực sự trước
    
    ```jsx
    let truearray = Array.from(arraylike);
    ```
    
- Array.from() cũng chấp nhận một đối số thứ 2 tuỳ chọn. Nếu bạn chuyển một hàm làm đối số thứ 2, thì khi mảng mới đang được xây dựng, mỗi phần tử từ object nguồn sẽ được chuyển đến hàm bạn chỉ định và giá trị trả về của hàm sẽ được lưu trữ trong mảng thay vì  giá trị ban đầu. (Điều này giống với method map() của mảng sẽ được giới thiệu sau trong chương này, nhưng sẽ hiệu quả hơn khi thực hiện ánh xạ trong khi mảng đang được xây dựng so với việc xây dựng mảng sau đó ánh xạ nó thành một mảng mới khác)

## **7.2 Đọc và Ghi Phần tử Mảng**

- Bạn truy cập phần tử mảng bằng cách sử dụng toán tử `[]`. Một tham chiếu đến mảng sẽ xuất hiện bên trái của dấu ngoặc vuông. Một biểu thức tuỳ ý có giá trị số nguyên không âm sẽ nằm trong dấu ngoặc vuông. Bạn có thể sử dụng cú pháp này để đọc ghi các giá trị của một phần tử của mảng. Do đó, những điều sau đây đều là các câu lệnh Js hợp lệ
    
    ```jsx
    let a = ["world"]; // Bắt đầu với mảng một phần tử
    let value = a[0]; // Đọc phần tử 0
    a[1] = 3.14; // Ghi phần tử 1
    let i = 2;
    a[i] = 3; // Ghi phần tử 2
    a[i + 1] = "hello"; // Ghi phần tử 3
    a[a[i]] = a[0]; // Đọc phần tử 0 và 2, ghi phần tử 3
    ```
    
- Điều đặc biệt về mảng là khi bạn sử dụng tên property là số nguyên âm nhỏ hơn 2<sup>32</sup> - 1, mảng sẽ tự động duy trì giá trị của property length cho bạn. Ví dụ: trong ví dụ trước, chúng ta đã tạo một mảng a với một phần tử duy nhất. Sau đó chúng ta gán giá trị tại số 1, 2 và 3. Thuộc tính length của mảng đã thay đổi khi chúng ta thực hiện, vì vậy
    
    ```jsx
    a.length // => 4
    ```
    
- Hãy nhớ rằng mảng là một dạng đặc biệt của object. Dấu ngoặc vuông được sử dụng để truy cập các phần tử mảng hoạt động giống như dấu ngoặc vuông được sử dụng để truy cập các property của object. Js chuyển đổi index mảng số mà bạn chỉ định thành một chuỗi - index số 1 trở thành string “1” - sau đó sử dụng chuỗi đó làm tên property. Không có gì đặc biệt về việc chuyển đổi index từ số sang chuỗi: Bạn cũng có thể làm điều đó với các object thông thường
    
    ```jsx
    let o = {}; // Tạo một đối tượng đơn giản
    o[1] = "one"; // Chỉ mục nó bằng một số nguyên
    o["1"] // => "one"; tên thuộc tính số và chuỗi là giống nhau
    ```
- Sẽ rất hữu ích khi phân biệt rõ ràng index mảng với tên property object. Tất cả các index đều là tên property, nhưng chỉ các tên property là số nguyên từ 0 đến 2<sup>32</sup> - 2 mới là index. Tất cả các mảng đều là object và bạn có thể tạo object với bất kỳ tên nào trên chúng. Tuy nhiên, nếu bạn sử dụng các property là index mảng, mảng sẽ có hành vi đặc biệt là cập nhật thuộc tính length của chúng khi cần thiết
- Lưu ý rằng bạn có thể lập index mảng bằng cách sử dụng các số âm hoặc không phải số nguyên. Khi bạn làm điều này, số đó sẽ được chuyển đổi thành một chuỗi và chuỗi đó được sử dụng làm tên property. Vì tên không phải là số nguyên không âm, nó được coi là property object thông thường, không phải là index mảng. Ngoài ra, nếu bạn lập index một mảng bằng một chuỗi tình cờ là một số nguyên không âm, nó sẽ hoạt động như một index mảng, không phải là property object. Điều này cũng đúng nếu bạn sử dụng một dấu phẩy động giống như một số nguyên
    
    ```jsx
    a[-1.23] = true; // Điều này tạo ra một thuộc tính có tên "-1.23"
    a["1000"] = 0; // Đây là phần tử thứ 1001 của mảng
    a[1.000] = 1; // Chỉ mục mảng 1. Giống như a[1] = 1;
    ```
    
- Thực tế là index mảng chỉ đơn giản là một loại tên property object đặc biệt có nghĩa là mảng Js không có khái niệm về lỗi “ngoài giới hạn” (out of bounds). Khi bạn cố gắng truy vấn một property không tồn tại của bất kỳ object nào, bạn sẽ không nhận được lỗi; bạn chỉ đơn giản là nhận được undefined. Điều này cũng đúng với mảng như đối với các object
    
    ```jsx
    let a = [true, false]; // Mảng này có các phần tử tại chỉ số 0 và 1
    a[2] // => undefined; không có phần tử nào tại chỉ mục này.
    a[-1] // => undefined; không có thuộc tính nào có tên này.
    ```
    

## **7.3 Mảng Thưa Thớt - Sparce Array**

- Là mảng mà các phần tử không có index liên tiếp bắt đầu từ 0. Thông thường, property length của mảng chỉ định số lượng phần tử trong mảng. Nếu mảng là thưa thớt, giá trị của property length sẽ lớn hơn số lượng phần tử
- Mảng thưa thớt có thể được tạo bằng hàm tạo `Array()` hoặc đơn giản bằng cách gán một index mảng lớn hơn độ dài mảng hiện tại
    
    ```jsx
    let a = new Array(5); // Không có phần tử, nhưng a.length là 5.
    a = []; // Tạo một mảng không có phần tử và length = 0.
    a[1000] = 0; // Việc gán thêm một phần tử nhưng đặt length thành 1001.
    ```
    
- Chúng ta sẽ thấy sau này bạn cũng có thể tạo một mảng thưa thớt bằng toán tử delete
- Các mảng đủ thưa thớt được triển khai theo cách chậm hơn, sử dụng bộ nhớ hiệu quả hơn so với các mảng dày đặc và việc tra cứu các phần tử trong một mảng như vậy sẽ mất khoảng thời gian tương tự như tra cứu property thông thường
- Lưu ý rằng khi bạn bỏ qua một giá trị trong array literal (sử dụng dấu phẩy lặp lại như trong [1,,3]), nảg kết quả sẽ là thưa thớt và các phần tử bị bỏ qua sẽ đơn giản là không tồn tại
    
    ```jsx
    let a1 = [,]; // Mảng này không có phần tử và length là 1
    let a2 = [undefined]; // Mảng này có một phần tử undefined
    0 in a1 // => false: a1 không có phần tử nào có chỉ số 0
    0 in a2 // => true: a2 có giá trị undefined tại chỉ số 0
    ```
    
- Hiểu về mảng thưa thớt là một phần quan trọng để hiểu bản chất thực sự của mảng Js. Tuy nhiên, trong thực tế, hầu hết các mảng Js mà bạn sẽ làm việc sẽ không phải là mảng thưa thớt. Và nếu bạn phải làm việc với một mảng thưa thớt, code của bạn có thể sẽ coi nó giống như các nó xử lý một mảng không thưa thớt với các phần tử undefined

## **7.4 Độ Dài Mảng**

- Mọi mảng đều có property `length` và chính property này tạo nên sự khác biệt của mảng so với object Js thông thường. Đối với mảng dày đặc (nghĩa là không thưa thớt), property length chỉ định số lượng phần tử trong mảng. Giá trị của nó lớn hơn 1 so với index cao nhất trong mảng
    
    ```jsx
    [].length // => 0: mảng không có phần tử
    ["a","b","c"].length // => 3: chỉ số cao nhất là 2, length là 3
    ```
    
- Khi một mảng là thưa thớt, property length sẽ lớn hơn số lượng phần tử và tất cả những gì chúng ta có thể nói về nó là `length` được đảm bảo lớn hơn index của mọi phần tử trong mảng. Hoặc nói cách khác, một mảng (thưa thớt hoặc không) sẽ không bao giờ có một phần tử có index lớn hơn hoặc bằng length của nó. Để duy trì tính bất biến này, mảng có 2 hành vi đặc biệt. Điều đầu tiên chúng tôi đã mô tả ở trên: nếu bạn gán một giá trị cho một phần tử mảng có index `i` lớn hơn hoặc bằng length hiện tại của mảng, thì giá trị của property length sẽ được đặt là `i + 1`
- Hành vi đặc biệt thứ 2 mà mảng thực hiện để duy trì tính bất biến của length là nếu bạn đặt property length thành một số nguyên `n` không âm nhỏ hơn giá trị hiện tại của nó, thì bất kỳ phần tử mảng nào có index lớn hơn hoặc bằng `n` sẽ bị xoá khỏi mảng
    
    ```jsx
    a = [1,2,3,4,5]; // Bắt đầu với một mảng 5 phần tử.
    a.length = 3; // a bây giờ là [1,2,3].
    a.length = 0; // Xóa tất cả các phần tử. a là [].
    a.length = 5; // Length là 5, nhưng không có phần tử, giống như new Array(5)
    ```
    
- Bạn có thể đặt property length của mảng thành một giá trị lớn hơn giá trị hiện tại của nó. Làm điều này không thực sự thêm bất kỳ phần tử mới nào vào mảng; nó chỉ đơn giản là tạo ra một vùng thưa thớt ở cuối mảng

## **7.5 Thêm và Xóa Phần tử Mảng**

- Chúng ta đã thấy cách đơn giản nhất để thêm phần tử vào mảng: chỉ cần gán giá trị cho các index mới
    
    ```jsx
    let a = []; // Bắt đầu với một mảng rỗng.
    a[0] = "zero"; // Và thêm các phần tử vào nó.
    a[1] = "one"; 
    ```
    
- Bạn cũng có thể áp dụng method `push()` để thêm một hoặc nhiều value vào cuối mảng
    
    ```jsx
    let a = []; // Bắt đầu với một mảng rỗng
    a.push("zero"); // Thêm một giá trị vào cuối. a = ["zero"]
    a.push("one", "two"); // Thêm hai giá trị nữa. a = ["zero", "one", "two"]
    ```
    
- Đẩy một value vào mảng a cũng giống như gán giá trị đó cho `a[a.length]`. Bạn có thể sử dụng method `unshift()` (được mô tả trong 7.8) để chèn một giá trị vào đầu mảng, dịch chuyển các phần tử mảng hiện có sang các index cao hơn. Method `pop()` là ngược lại với `push()`: nó loại bỏ phần tử cuối cùng của mảng và trả về nó, giảm độ dài của mảng đi 1. Tương tự, method `shift()` loại bỏ và trả về method đầu tiên của mảng, giảm độ dài đi 1 và dịch chuyển tất cả các phần tử xuống một index thấp hơn index hiện tại của chúng. Xem 7.8  để biết thêm chi tiết về các method này
- Bạn có thể xoá method trong array bằng toán tử delete , giống như bạn có thể xoá các property của object
    
    ```jsx
    let a = [1,2,3];
    delete a[2]; // a bây giờ không có phần tử nào tại chỉ số 2
    2 in a // => false: không có chỉ số mảng 2 nào được xác định
    a.length // => 3: delete không ảnh hưởng đến độ dài mảng
    ```
    
- Xoá một phần tử mảng tương tự như (nhưng khác biệt một chút so với) việc gán `undefined` cho method đó. Lưu ý rằng việc sử dụng `delete` trên một phần tử mảng không làm thay đổi property length và không dịch chuyển các phần tử có index cao hơn xuống để lấp đầy khoảng trống do property đã xoá để lại. Nếu bạn xoá một phần tử khỏi mảng, mảng đó sẽ trở thành mảng thưa thớt
- Như chúng ta đã thấy ở trên, bạn cũng có thể xoá các phần tử cuối mảng bằng cách đặt property length thành độ dài mong muốn mới
- Cuối cùng, `splice()` là method mục đích chung để chèn, xoá hoặc thay thế các phần tử mảng. Nó thay đổi property length và dịch chuyển các phần tử mảng sang các index cao hơn hoặc thấp hơn khi cần thiết

## **7.6 Lặp qua Mảng**

- Kể từ ES6, cách dễ nhất để lặp qua từng phần tử của mảng (hoặc bất kỳ object có thể lặp lại nào) là sử dụng vòng lặp for of, đã được đề cập trong 5.4.4
    
    ```jsx
    let letters = [..."Hello world"]; // Một mảng các chữ cái
    let string = "";
    for(let letter of letters) {
      string += letter;
    }
    string // => "Hello world"; chúng ta đã tập hợp lại văn bản gốc
    ```
    
- Trình lặp mảng tích hợp mà vòng lặp `for/of` sử dụng trả về các phần tử của mảng theo thứ tự tăng dần. Nó không có hành vi đặc biệt nào đối với mảng thưa thớt và chỉ đơn giản là trả về `undefined` cho bất kỳ phần tử mảng nào không tồn tại
- Nếu bạn muốn sử dụng vòng lặp `for/of` cho một mảng và cần biết index của mỗi phần tử mảng, hãy sử dụng method `entries()` của mảng, cùng với phép gán phân rã như thế này
    
    ```jsx
    let everyother = "";
    for(let [index, letter] of letters.entries()) {
      if (index % 2 === 0) everyother += letter; // chữ cái tại các chỉ mục chẵn
    }
    everyother // => "Hlowrd"
    ```
    
- Một cách tốt khác để lặp qua mảng là với forEach(). Đây không phải là dạng mới của vòng lặp for, mà là một method mảng cung cấp cách tiếp cận hàm cho việc lặp mảng. Bạn chuyển một hàm cho `forEach()` method của mảng và forEach() gọi hàm của bạn một lần trên mỗi phần tử của mảng
    
    ```jsx
    let uppercase = "";
    letters.forEach(letter => { // Lưu ý cú pháp hàm mũi tên ở đây
      uppercase += letter.toUpperCase();
    });
    uppercase // => "HELLO WORLD"
    ```
    
- Như bạn mong đợi, `forEach()` lặp qua mảng theo thứ tự và nó thực sự chuyển index mảng cho hàm của bạn làm đối số thứ 2, điều này đôi khi hữu ích. Không giống như vòng lặp `for of`, `forEach()` nhận biết các mảng thưa thớt và không gọi hàm của bạn cho các phần tử không có ở đó
- 7.8.1 ghi lại method `forEach()` chi tiết hơn. Phần đó cũng đề cập đến method liên quan map() và filter() thực hiện các loại lặp mảng chuyên biệt
- Bạn cũng có thể lặp qua các phần tử của mảng bằng vòng lặp for cổ điển
    
    ```jsx
    let vowels = "";
    for(let i = 0; i < letters.length; i++) { // Đối với mỗi chỉ mục trong mảng
      let letter = letters[i]; // Lấy phần tử tại chỉ mục đó
      if (/[aeiou]/.test(letter)) { // Sử dụng kiểm tra biểu thức chính quy
        vowels += letter; // Nếu nó là một nguyên âm, hãy ghi nhớ nó
      }
    }
    vowels // => "eoo"
    ```
    
- Trong các vòng lặp lồng nhau hoặc ngữ cảnh khác mà hiệu suất là rất quan trọng, đôi khi bạn có thể thấy vòng lặp lặp mảng cơ bản này được viết sao cho độ dài mảng chỉ được tra cứu một lần thay vì trên mỗi lần lặp. Cả 2 dạng vòng lặp for sau đây đều là thành ngữ, mặc dù không phổ biến đặc biệt và với các trình thông dịch Js hiện đại, không rõ ràng lắm liệu chúng có tác động đến hiệu suất hay không
    
    ```jsx
    // Lưu độ dài mảng vào một biến cục bộ
    for(let i = 0, len = letters.length; i < len; i++) {
      // thân vòng lặp vẫn giữ nguyên
    }
    // Lặp ngược từ cuối mảng đến đầu
    for(let i = letters.length-1; i >= 0; i--) {
      // thân vòng lặp vẫn giữ nguyên
    }
    ```
    
- Các ví dụ này giả định rằng mảng là dày đặc và tất cả các phần tử đều chứa dữ liệu hợp lệ. Nếu không phải như vậy, bạn nên kiểm tra các phần tử mảng trước khi sử dụng chúng. Nếu bạn muốn bỏ qua các phần tử undefined và không tồn tại, bạn có thể viết
    
    ```jsx
    for(let i = 0; i < a.length; i++) {
      if (a[i] === undefined) continue; // Bỏ qua các phần tử undefined + không tồn tại
      // thân vòng lặp ở đây
    }
    ```
## **7.7 Mảng Đa chiều**

- Js không hỗ trợ mảng đa chiều thực sự, nhưng bạn có thể mô phỏng chúng bằng mảng các mảng. Để truy cập một giá trị trong một mảng các mảng, chỉ cần sử dụng toán tử `[]` hai lần. Ví dụ: giả sử biến `matrix` là một mảng các mảng số. Mọi phần tử trong `matrix[x]` là một mảng số. Để truy cập một số cụ thể trong mảng này, bạn sẽ viết `matrix[x][y]`. Dưới đây là một ví dụ cụ thể sử dụng mảng 2 chiều để làm bảng cửu chương
    
    ```jsx
    // Tạo một mảng đa chiều
    let table = new Array(10); // 10 hàng của bảng
    for(let i = 0; i < table.length; i++) {
      table[i] = new Array(10); // Mỗi hàng có 10 cột
    }
    // Khởi tạo mảng
    for(let row = 0; row < table.length; row++) {
      for(let col = 0; col < table[row].length; col++) {
        table[row][col] = row * col;
      }
    }
    // Sử dụng mảng đa chiều để tính 5 * 7
    table[5][7] // => 35
    ```
    
- **Giải thích**
    - **Tạo mảng 2 chiều:** Đầu tiên chúng ta tạo một mảng `table` có 10 phần tử, mỗi phần tử đại diện cho một hàng trong bảng. Sau đó, chúng ta lặp qua từng phần tử của table và gán cho nó một mảng mới co 10 phần tử đại diện cho 10 cột. Kết quả sau đó là mảng 2 chiều 10 x 10.
    - **Khởi tạo mảng:** Chúng ta sử dụng 2 vòng lặp for lồng nhau để duyệt qua từng phần tử của mảng `table`. Với mỗi phần tử `table[row][col]` chúng ta gán giá trị là tích của row và col, tương ứng với phép nhân trong bảng cửu chương
    - **Truy cập phần tử:** Để lấy kết quả cho phép nhân 5 * 7, chúng ta truy cập phần tử `table[5][7]`, trả về giá trị 35
- Lưu ý, mảng đa chiều trong Js chỉ là mảng của mảng, không phải kiểu dữ liệu riêng biệt như một số ngôn ngữ lập trình khác

## **7.8 Phương thức Mảng**

- Các phần trước tập chung vào cú pháp Js cơ bản để làm việc với mảng. Tuy nhiên, nói chung, chính các method được định nghĩa bởi class `Array` mới là mạnh mẽ nhất. Các phần tiếp theo ghi lại các method này
- Trong khi đọc về các method này, hãy nhớ rằng một số method sửa đổi mảng mà chúng được gọi và một số method khác để nguyên mảng. Một số method trả về một mảng: đôi khi, đây là một mảng mới và bản gốc không bị thay đổi. Trong các trường hợp khác, một method sẽ sửa đổi mảng tại chỗ và cũng sẽ trả về tham chiếu đến mảng đã sửa đổi
- Một phần nhỏ sau đây đề cập đến một nhóm các method mảng có liên quan
    - Method trình lặp (Iterator methods) lặp qua các phần tử của mảng, thường gọi một hàm mà bạn chỉ định trên mỗi phần tử đó
    - Method ngăn xếp và hàng đợi (Stack and queue methods) thêm và xoá các phần tử mảng vào và tử đầu đến cuối mảng
    - Method mảng con (Subarray methods) dùng để trích xuất, xoá, chèn, điền và sao chép các vùng liền kề của một mảng lớn hơn
    - Method tìm kiếm và sắp xếp (Searching and sorting methods) dùng để xác định vị trí các phần tử trong mảng và để sắp xếp các phần tử của mảng
- Các phần nhỏ sau đây cũng đề cập đến các method tĩnh của class `Array` và một số method linh tinh để nối các mảng và chuyển đổi mảng thành chuỗi

### **7.8.1 Phương thức Trình lặp Mảng**

- Các method được mô tả trong phần này lặp lại các mảng bằng cách chuyển các phần tử mảng, theo thứ tự, cho một hàm mà bạn cung cấp và chúng cung cấp các cách thuận tiện để lặp, ánh xạ, lọc, kiểm tra và giảm mảng
- Tuy nhiên, trước khi chúng ta giải thích chi tiết về các method, điều đáng giá là phải khái quát một số điều về chúng. Đầu tiên, tất cả các method này đều chấp nhận một hàm làm đối số đầu tiên của chúng và gọi hàm đó một lần cho mỗi phần tử (hoặc một số phần tử) của mảng. Nếu mảng là thưa thớt, hàm bạn truyền vào sẽ không được gọi cho các phần tử không tồn tại. Trong hầu hết các trường hợp, hàm bạn cung cấp được gọi với ba đối số: giá trị của phần tử mảng, index của phần tử mảng và chính mảng đó. Thông thường, bạn chỉ cần giá trị đầu tiên của các giá trị đối số này và bạn có thể bỏ qua giá trị thứ 2 và thứ 3
- Hầu hết các method trình lặp được mô tả trong các phần nhỏ sau đây đều chấp nhận một đối số thứ 2 tuỳ chọn. Nếu được chỉ định, hàm sẽ được gọi như thể nó là một method của đối số thứ hai này. Nghĩa là, đối số thứ 2 mà bạn chuyển vào sẽ trở thành giá trị của từ khoá `this` bên trong hàm mà bạn chuyển làm đối số đầu tiên. Giá trị trả về của hàm bạn truyền thường rất quan trọng, nhưng các method khác nhau xử lý các giá trị trả về theo những cách khác nhau. Không có method nào được mô tả ở đây sửa đổi mảng mà chúng đươc gọi (mặc dù hàm bạn truyền có thể sửa đổi mảng)

- Mỗi hàm này được gọi với một hàm làm đối số đầu tiên của nó và rất phổ biến để xác định hàm đó nội tuyến như một phần của biểu thức gọi method thay vì sử dụng một hàm hiện có được xác định ở một nơi khác. Cú pháp arrow function (8.1.3) hoạt động đặc biệt tốt với các method này và chúng ta sẽ sử dụng nó trong các ví dụ sau đây
- `forEach()` method lặp qua một mảng, gọi một hàm mà bạn chỉ định cho mỗi phần tử. Như đã mô tả, bạn truyền hàm làm đối số đầu tiên cho `forEach()`. `forEach()` sau đó gọi hàm của bạn với 3 đối số: value của phần tử mảng, index của mảng và chính mảng đó. Nếu bạn chỉ quan tâm đến value của phần tử của mảng, bạn có thể viết một hàm chỉ có một tham số - các đối số bổ sung sẽ bị bỏ qua
    
    ```jsx
    let data = [1,2,3,4,5], sum = 0;
    // Tính tổng các phần tử của mảng
    data.forEach(value => { sum += value; }); // sum == 15
    // Bây giờ tăng mỗi phần tử mảng lên 1
    data.forEach(function(v, i, a) { a[i] = v + 1; }); // data == [2,3,4,5,6]
    ```
    
- Lưu ý rằng `forEach()` không cung cấp cách để chấm dứt lặp lại trước khi tất cả các phần tử được chuyển đến hàm. Tức là không có câu lệnh **break** tương đương mà bạn có thể sử dụng trong vòng lặp `for` thông thường
- `map()` method chuyển từng phần của mảng mà nó được gọi đến hàm bạn chỉ định và trả về một mảng chứa các giá trị được trả về bởi hàm của bạn. Ví dụ
    
    ```jsx
    let a = [1, 2, 3];
    a.map(x => x*x) // => [1, 4, 9]: hàm nhận đầu vào x và trả về x*x
    ```
    
- Hàm bạn truyền cho `map()` được gọi theo cách tương tự hàm được truyền cho `forEach()`. Tuy nhiên, đối với method `map()`, bạn truyền vào phải trả về một giá trị. Lưu ý rằng `map()` trả về một mảng mới: nó không sử đổi mảng mà nó được gọi. Nếu mảng là mảng thưa thớt, hàm sẽ không được gọi cho các phần tử bị thiếu, nhưng mảng trả về sẽ thưa thớt giống như mảng ban đầu: nó sẽ có cùng độ dài và cùng các phần tử bị thiếu
- `filter()` method trả về một mảng chứa một tập hợp con các phần tử của mảng mà nó được gọi. Hàm bạn truyền cho nó phải là một vị ngữ: một hàm trả về true hoặc false. Vị ngữ được gọi giống như đối với `forEach()` và `map()`. Nếu giá trị trả về là true hoặc một giá trị chuyển đổi thành true, thì phần tử được truyền cho vị ngữ là một thành viên của tập hợp con và được thêm vào mảng sẽ trở thành giá trị trả về
    
    ```jsx
    let a = [5, 4, 3, 2, 1];
    a.filter(x => x < 3) // => [2, 1]; các giá trị nhỏ hơn 3
    a.filter((x,i) => i%2 === 0) // => [5, 3, 1]; cách giá trị khác
    ```
    
- **Lưu ý rằng**: `filter()` bỏ qua các phần tử bị thiếu trong mảng thưa thớt  và trả về giá trị của nó luôn dày đặc. Để đóng các khoảng trống trong một mảng thưa thớt, bạn có thể làm như sau
    
    ```jsx
    let dense = sparse.filter(() => true);
    ```
    
- Và để đóng các khoảng trống và loại bỏ các phần tử **undefined và null**, bạn có thể sử dụng
    
    ```jsx
    a = a.filter(x => x !== undefined && x !== null);
    ```
    
- Các method `find()` và `findIndex()` giống như `filter()` ở chỗ chúng lặp lại mảng của bạn để tìm kiếm các phần tử mà hàm vị ngữ của bạn trả về truthy. Tuy nhiên, không giống như `filter()`, hai method này ngừng lặp lại lần đầu tiên vị ngữ tìm thấy một phần tử. Khi điều đó xảy ra, `find()` trả về phần tử phù hợp và `findIndex()` trả về index của phần tử phù hợp. Nếu không tìm thấy phần tử phù hợp, `find()` trả về undefined và `findIndex()` trả về -1
    
    ```jsx
    let a = [1,2,3,4,5];
    a.findIndex(x => x === 3) // => 2; giá trị 3 xuất hiện ở chỉ mục 2
    a.findIndex(x => x < 0) // => -1; không có số âm nào trong mảng
    a.find(x => x % 5 === 0) // => 5: đây là bội số của 5
    a.find(x => x % 7 === 0) // => undefined: không có bội số của 7 trong mảng
    ```
    
- Các method `every()` và `some()` là các vị ngữ mảng: chúng áp dụng một hàm vị ngữ mà bạn chỉ định cho các phần tử của mảng, sau đó trả về true hoặc false
- `every()` method giống như lượng từ “cho tất cả” trong toán học ∀: nó trả về true nếu và chỉ khi hàm vị ngữ của bạn trả về true cho tất cả các phần tử trong mảng
    
    ```jsx
    let a = [1,2,3,4,5];
    a.every(x => x < 10) // => true: tất cả các giá trị đều < 10.
    a.every(x => x % 2 === 0) // => false: không phải tất cả các giá trị đều chẵn.
    ```
    
- `some()` method giống như lượng tử “tồn tại” trong toán học ∃: Nó trả về true nếu ít nhất một phần tử trong mảng mà vị ngữ trả về true và trả về false nếu và chỉ khi giá trị vị ngữ trả về false cho tất cả các phần tử trong mảng
    
    ```jsx
    let a = [1,2,3,4,5];
    a.some(x => x%2===0) // => true; a có một số số chẵn.
    a.some(isNaN) // => false; a không có số không phải là số.
    ```
    
- Lưu ý rằng cả `every() và some()` đều ngừng lặp lại các phần tử trong mảng ngay khi chúng biết giá trị nào sẽ trả về. `some()` trả về true lần đầu tiên vị ngữ của bạn trả về `true` và chỉ lặp lại toàn bộ mảng nếu vị ngữ của bạn luôn trả về false. `every()` thì ngược lại: nó trả về false lần đầu tiên vị ngữ của bạn trả về false và chỉ lặp lại các phần tử nếu vị ngữ của bạn luôn trả về true
- Cũng lưu ý rằng, theo quy ước toán học, `every()` trả về true và `some()` trả về false khi được gọi trên một mảng rỗng

### reduce() & reduceRight()

- Các method `reduce()` và `reduceRight()` kết hợp các phần tử của một mảng, sử dụng hàm mà bạn chỉ định để tạo ra một giá trị duy nhất. Đây là một thao tác phổ biến trong lập trình hàm và còn được gọi với cái tên là “inject” và “fold”. Các ví dụ minh hoạt cho cách thức hoạt động của nó
    
    ```jsx
    let a = [1,2,3,4,5];
    a.reduce((x,y) => x+y, 0) // => 15; tổng của các giá trị
    a.reduce((x,y) => x*y, 1) // => 120; tích của các giá trị
    a.reduce((x,y) => (x > y) ? x : y) // => 5; giá trị lớn nhất của các giá trị
    ```
    
- `reduce()` nhận 2 đối số. Đầu tiên là hàm thực hiện theo tác giảm. Nhiệm vụ của hàm giảm này là bằng cách nào đó kết hợp hoặc giảm hai giá trị thành một giá trị duy nhất và trả về giá trị đã giảm đó. Trong các ví dụ chúng ta đã trình bày ở đây, các hàm kết hợp 2 giá trị bằng cách cộng chúng, nhân và chọn giá trị lớn nhất. Đối số thứ 2 (optional) là giá trị ban đầu được truyền cho hàm
- Các hàm được sử dụng với `reduce()` khác với các hàm được sử dụng với `forEach()` và `map()`. Các giá trị quen thuộc là `value, index, array` được truyền dưới dạng đối số thứ 2, thứ 3 và 4. Đối số đầu tiên là kết quả tích luỹ của việc giảm cho đến nay. Trong lần gọi đầu tiên đến hàm, đối số đầu tiên này là giá trị ban đầu mà bạn đã truyền làm đối số thứ 2 cho `reduce()`. Trong các lần gọi tiếp theo, nó là giá trị được trả về bởi lần gọi trước đó của hàm. Trong ví dụ đầu tiên, hàm giảm đầu tiên được gọi với các đối số 0 và 1. Nó cộng chúng lại và trả về 1. Sau đó nó được gọi lại với các đối số 1 và 2 và trả về 3, tiếp theo nó tính 3 + 3 = 6, sau đó 6 + 4 = 10 và cuối cùng là 10 + 5 = 15. Giá trị cuối cùng này, 15, sẽ trở thành giá trị trả về của `reduce()`
- Bạn có thể nhận thấy rằng lần gọi thứ 3 đến `reduce()` trong ví dụ này chỉ có một đối số duy nhất, không có giá trị ban đầu nào được chỉ định. Khi bạn gọi `reduce()` như thế này mà không có giá trị ban đầu, nó sẽ sử dụng phần tử đầu tiên của mảng làm giá trị ban đầu. Điều này có nghĩa là lần gọi đầu tiên đến hàm giảm sẽ có phần tử mảng thứ 1 và thứ 2 làm đối số thứ 1 và thứ 2 của nó. Trong các ví dụ về tổng và tích chúng ta có thể bỏ qua đối số giá trị ban đầu
- Việc gọi `reduce()` trên một mảng rỗng mà không có đối số giá trị ban đầu sẽ gây ra `TypeError`. Nếu bạn gọi nó chỉ với một giá trị - một mảng có 1 phần tử và không có giá trị ban đầu hoặc một mảng rỗng và một giá trị ban đầu - nó sẽ chỉ trả về một giá trị đó mà không bao giờ gọi hàm giảm
- `reduceRight()` hoạt động giống như `reduce()`, ngoại trừ việc nó xử lý mảng tử index cao nhất đến thấp nhất (từ phải sang trái) thay vì từ thấp đến cao. Bạn có thể muốn làm điều này nếu thao tác giảm có tính kết hợp từ phải sang trái
    
    ```jsx
    // Tính 2 ^ (3 ^ 4). Lũy thừa có độ ưu tiên từ phải sang trái
    let a = [2, 3, 4];
    a.reduceRight((acc,val) => Math.pow(val,acc)) // => 2.4178516392292583e+24
    ```
    
- Lưu ý rằng cả `reduce()` và `reduceRight()` đều không chấp nhận một đối số tuỳ chọn chỉ định giá trị `this` mà hàm giảm sẽ được gọi. Đối số giá trị ban đầu tuỳ chọn sẽ thay thế vị trí của nó. Xem method `Function.bind()` (8.7.5) nếu bạn cần hàm giảm của mình được gọi như một method của một object cụ thể
- Các ví dụ được hiển thị cho đến nay là số để cho đơn giản, nhưng `reduce()` và `reduceRight()` không chỉ dành riêng cho các phép tính toán học. Bất kỳ hàm nào có thể kết hợp 2 giá trị (chẳng hạn như 2 object) thành một giá trị cùng loại đều có thể sử dụng làm hàm giảm
- Mặt khác, thuật toán được biểu thị bằng cách sử dụng giảm mảng có thể nhanh chóng trở phức tạp và khó hiểu và bạn có thể thấy rằng sẽ dễ đọc, viết và lý luận code của mình hơn nếu bạn sử dụng các cấu trúc lặp thông thường để xử lý mảng của mình

### **7.8.2 Làm phẳng mảng với flat() và flatMap()**

- Trong ES2019, `flat()` method tạo và trả về một mảng mới chứa các phần tử giống với mảng mà nó được gọi, ngoại trừ bất kỳ phần tử nào là mảng sẽ được “làm phẳng” (“flattened”) thành mảng được trả về
    
    ```jsx
    [1, [2, 3]].flat() // => [1, 2, 3]
    [1, [2, [3]]].flat() // => [1, 2, [3]]
    ```
    
- Khi được gọi mà không có đối số, `flat()` làm phẳng một cấp độ lồng nhau. Các phần tử  của mảng ban đầu là mảng sẽ được làm phẳng, nhưng các phần tử của các mảng đó sẽ không được làm phẳng. Nếu bạn muốn làm phẳng nhiều cấp độ hơn, hãy truyền một số vào `flat()`
    
    ```jsx
    let a = [1, [2, [3, [4]]]];
    a.flat(1) // => [1, 2, [3, [4]]]
    a.flat(2) // => [1, 2, 3, [4]]
    a.flat(3) // => [1, 2, 3, 4]
    a.flat(4) // => [1, 2, 3, 4]
    ```
    
- `flatMap()` method hoạt động giống như `map()` method ngoại trừ việc mảng trả về sẽ tự động làm phẳng như thể được truyền cho `flat()`. Có nghĩa là gọi `a.flatMap(f)` cũng giống như (nhưng hiệu quả hơn) `a.map(f).flat()`
    
    ```jsx
    let phrases = ["hello world", "the definitive guide"];
    let words = phrases.flatMap(phrase => phrase.split(" "));
    words // => ["hello", "world", "the", "definitive", "guide"];
    ```
    
- Bạn có thể gọi `flatMap()` như một dạng tổng quan của `map()` cho phép mỗi phần tử của mảng đầu vào ánh xạ tới bất kỳ số lượng phần tử nào của mảng đầu ra. Cụ thể, `flatMap()` cho phép bạn ánh xạ các phần tử đầu vào tới một mảng rỗng, mảng này sẽ được làm phẳng thành không có gì trong mảng đầu ra
    
    ```jsx
    // Ánh xạ các số không âm thành căn bậc hai của chúng
    [-2, -1, 1, 2].flatMap(x => x < 0 ? [] : Math.sqrt(x)) // => [1, 2**0.5]
    ```
    

### **7.8.3 Thêm mảng với concat()**

- `concat()` method tạo và trả về một mảng mới chứa các phần tử của mảng ban đầu mà `concat()` được gọi, theo sau là mỗi đối số của `concat()`. Nếu bất kỳ đối số nào trong số này là một mảng, thì chính các phần tử mảng sẽ được nối, chứ không phải bản thân mảng đó. Tuy nhiên, lưu ý rằng `concat()` không làm phẳng đệ quy các mảng của mảng. `concat()` không sửa đổi mảng mà nó được gọi
    
    ```jsx
    let a = [1,2,3];
    a.concat(4, 5) // => [1,2,3,4,5]
    a.concat([4,5],[6,7]) // => [1,2,3,4,5,6,7]; mảng được làm phẳng
    a.concat(4, [5,[6,7]]) // => [1,2,3,4,5,[6,7]]; nhưng không phải mảng lồng nhau
    a // => [1,2,3]; mảng ban đầu không bị sửa đổi
    ```
    
- Lưu ý rằng `concat()` tạo một bản  sao mới của mảng mà nó được gọi. Trong nhiều trường hợp, đây là điều nên làm, nhưng đó là một thao tác tốn kém. Nếu bạn đang viết code là `a = a.concat(x)`, thì bạn nên nghĩ đến việc sửa đổi mảng của mình tại chỗ bằng cách sử dụng `push()` hoặc `splice()` thay vì tạo một mảng mới

### **7.8.4 Ngăn xếp và Hàng đợi với push(), pop(), shift() và unshift()**

- Các method `push() và pop()` cho phép bạn làm việc với mảng như chúng là ngăn xếp. `push()` method cho phép nối thêm một hoặc nhiều phần tử vào cuối mảng và trả về độ dài mới của mảng. Không giống như `concat()`, `push()` không làm phẳng các đối số của mảng. `pop()` thực hiện điều ngược lại: nó xoá phần tử cuối cùng của mảng, giảm độ dài mảng và trả về giá trị mà nó đã xoá. Lưu ý rằng cả 2 method đều sửa đổi mảng tại chỗ. Sự kết hợp của `push() và pop()` cho phép bạn sử dụng mảng Js để triển khai ngăn xếp và trước, ra sau (First-In, Last-out)
    
    ```jsx
    let stack = []; // stack == []
    stack.push(1,2); // stack == [1,2];
    stack.pop(); // stack == [1]; trả về 2
    stack.push(3); // stack == [1,3]
    stack.pop(); // stack == [1]; trả về 3
    stack.push([4,5]); // stack == [1,[4,5]]
    stack.pop() // stack == [1]; trả về [4,5]
    stack.pop(); // stack == []; trả về 1
    ```
    
- `push()` method không làm phẳng mảng mà bạn truyền vào cho nó, nhưng nếu bạn muốn đẩy tất cả các phần tử từ mảng này sang mảng khác, bạn có thể sử dụng toán tử spread (8.3.4) để làm phẳng nó một cách rõ ràng
    
    ```jsx
    a.push(...values);
    ```
    
- Các method `unshift() và shift()` hoạt động rất giống `push() và pop()`, ngoại trừ việc chúng chèn và xoá các phần tử từ đầu mảng chứ không phải ở cuối. `unshift()` thêm một hoặc các phần tử vào đầu mảng, dịch chuyển các phần tử mảng hiện có lên các index cao hơn để nhường chỗ và trả về đội dài mới của mảng. `shift()` loại bỏ và trả về phần tử đầu tiên của mảng, dịch chuyển tất cả các phần tử tiếp theo xuống một vị trí để chiếm không gian trống ở đầu mảng
- Bạn có thể sử dụng `unshift() và shift()` để triển khai ngăn xếp, nhưng nó sẽ kém hiệu quả hơn so với việc sử dụng `push() và pop()` vì các phần tử mảng cần được dịch chuyển lên hoặc xuống mỗi khi phần tử được thêm hoặc xoá khỏi đầu mảng
- Thay vào đó, bạn có thể triền khai cấu trúc dữ liệu hàng đợi (queue) bằng cách sử dụng push() để thêm vào cuối mảng và `shift()` để xoá chúng khỏi đầu mảng
    
    ```jsx
    let q = []; // q == []
    q.push(1,2); // q == [1,2]
    q.shift(); // q == [2]; trả về 1
    q.push(3) // q == [2, 3]
    q.shift() // q == [3]; trả về 2
    q.shift() // q == []; trả về 3
    ```
    

### **7.8.5 Mảng con với slice(), splice(), fill() và copyWithin()**

- Mảng xác định một số method hoạt động trên các vùng liền kề hoặc mảng con hoặc “cắt lát” của một mảng. Các phần sau đây mô tả các method để trích xuất, thay thế, điền và sao chép các lát cắt
- `slice()` method trả về một lát cắt hoặc một mảng con của mảng được chỉ định. Hai đối số của nó chỉ định điểm đầu và điểm cuối của lát cắt cần trả về. Mảng được trả về chứa phần tử được chỉ định bởi đối số đầu tiên và cho đến các phần tử tiếp theo, nhưng không bao gồm, phần tử được chỉ định bởi tham số thứ 2
- Nếu chỉ định một đối số, mảng được trả về chứa tất cả các phần tử từ vị trí bắt đầu đến cuối mảng. Nếu một trong 2 đối số là âm, nó sẽ chỉ định một phần tử liên quan đến độ dài mảng. Ví dụ: đối số -1 chỉ định phần tử cuối cùng của mảng và đối số -2 chỉ định phần tử trước đó. Lưu ý rằng, `slice()` không sửa đổi mảng mà nó được gọi
    
    ```jsx
    let a = [1,2,3,4,5];
    a.slice(0,3); // Trả về [1,2,3]
    a.slice(3); // Trả về [4,5]
    a.slice(1,-1); // Trả về [2,3,4]
    a.slice(-3,-2); // Trả về [3]
    ```
    
- `splice()` là một method đa năng để chèn hoặc xoá phần tử khỏi mảng. Không giống như `slice() và concat()`, `splice()` sửa đổi mảng mà nó được gọi. Lưu ý rằng `slice()` và `splice()` có tên rất giống nhau nhưng thực hiện các hoạt động khác nhau đáng kể
- `splice()` có thể xoá phần tử khỏi mảng, chèn các phần tử mới vào mảng hoặc thực hiện đồng thời cả 2 thao tác. Các phần tử của mảng xuất hiện sau điểm chèn hoặc xoá có index được tăng hoặc giảm khi cần thiết để chúng vẫn liền kề với các phần còn lại của mảng
- Đối số đầu tiên của `splice()` chỉ định vị trí mảng mà tại đó việc chèn và / hoặc xoá sẽ bắt đầu. Đối số thứ 2 chỉ định số lượng phần tử cần được xoá (bị loại bỏ)khỏi mảng. (Lưu ý rằng đây là điểm khác biệt giữa 2 method này. Đối số thứ 2 cho `slice()` là vị trí kết thúc. Đối số thứ 2 của `splice()` là độ dài.) Nếu đối số thứ 2 này bị bỏ qua, tất cả các phần tử mảng từ phần tử bắt đầu đến cuối mảng sẽ bị loại bỏ. `splice()` trả về một mảng  các phần tử đã xoá hoặc một mảng rỗng nếu không có phần tử nào bị xoá
    
    ```jsx
    let a = [1,2,3,4,5,6,7,8];
    a.splice(4) // => [5,6,7,8]; a bây giờ là [1,2,3,4]
    a.splice(1,2) // => [2,3]; a bây giờ là [1,4]
    a.splice(1,1) // => [4]; a bây giờ là [1]
    ```
    
- Hai đối số đầu tiên cho `splice()` chỉ định phần tử mảng nào sẽ bị xoá. Các đối số này có thể được theo sau bởi bất kỳ số lượng đối số bổ sung nào được chỉ định các phần tử được chèn vào mảng, bắt đầu từ vị trí được chỉ định bởi đối số đầu tiên
    
    ```jsx
    let a = [1,2,3,4,5];
    a.splice(2,0,"a","b") // => []; a bây giờ là [1,2,"a","b",3,4,5]
    a.splice(2,2,[1,2],3) // => ["a","b"]; a bây giờ là [1,2,[1,2],3,3,4,5]
    ```
    
- Lưu ý rằng, không giống như `concat()` , `splice()` chèn chính các mảng, chứ không phải các phần tử của mảng đó
- `fill()` method đặt các phần tử của mảng hoặc một lát cắt của mảng thành giá trị được chỉ định. Nó thay đổi mảng mà nó được gọi và cũng trả về mảng đã sửa đổi
    
    ```jsx
    let a = new Array(5); // Bắt đầu với không có phần tử và length là 5
    a.fill(0) // => [0,0,0,0,0]; điền vào mảng bằng các số 0
    a.fill(9, 1) // => [0,9,9,9,9]; điền bằng 9 bắt đầu từ chỉ mục 1
    a.fill(8, 2, -1) // => [0,9,8,8,9]; điền bằng 8 tại chỉ mục 2, 3
    ```
    
- Đối số đầu tiên cho `fill()` là giá trị được đặt cho các phần tử mảng. Đối số thứ 2 tuỳ chọn chỉ định index bắt đầu. Nếu bị bỏ qua, việc điền sẽ bắt đầu ở index 0. Đối số thứ 3 tuỳ chọn chỉ định mục kết thúc - các phần tử mảng cho đến, nhưng không bao gồm, index này sẽ được điền. Nếu đối số này bị bỏ qua, thì mảng được điền từ index bắt đầu đến cuối. Bạn có thể chỉ định các index liên quan đến phần cuối của mảng bằng cách chuyển đổi các số âm, giống như bạn có thể làm với `slice()`
- `copyWithin()` sao chép một lát cắt của mảng đến một vị trí mới trong mảng. Nó sửa đổi mảng tại chỗ và trả về mảng đã sửa đổi, nhưng nó không thay đổi độ dài của mảng
- Đối số đầu tiên chỉ định index đến mà phần tử đầu tiên được sao chép đến đó. Đối số thứ 2 chỉ định index của phần tử đầu tiên được sao chép. Nếu đối số thứ 2 bị bỏ qua, 0 sẽ được sử dụng. Đối số thứ 3 chỉ định phần cuối của lát cắt các phần tử được sao chép. Nếu bị bỏ qua, độ dài của mảng sẽ được sử dụng. Các phần tử từ index bắt đầu đến, nhưng không bao gồm, index kết thúc sẽ được sao chép. Bạn có thể chỉ định các index liên quan đến phần cuối của mảng bằng cách chuyển các số âm giống như bạn có thể làm đối với `slice()`
    
    ```jsx
    let a = [1,2,3,4,5];
    a.copyWithin(1) // => [1,1,2,3,4]: sao chép các phần tử mảng lên một
    a.copyWithin(2, 3, 5) // => [1,1,3,4,4]: sao chép 2 phần tử cuối cùng đến chỉ mục 2
    a.copyWithin(0, -2) // => [4,4,3,4,4]: các offset âm cũng hoạt động
    ```
    
- `copyWithin()` được thiết kế như một method hiệu suất cao, đặc biệt hữu ích với mảng được nhập (11.2). Nó được mô hình hoá theo hàm `memmove()` từ thư viện chuẩn C. Lưu ý rằng việc sao chép sẽ hoạt động chính xác ngay cả khi có sự chồng chéo giữa vùng nguồn và vùng đích

### **7.8.6 Phương thức Tìm kiếm và Sắp xếp Mảng**

- Mảng triển khai các method `indexOf()`, `lastIndexOf()` và `includes()` tương tự như các method cùng tên của chuỗi. Ngoài ra còn có các method `sort()` và `reverse()` để sắp xếp lại các phần tử của mảng. Các method được mô tả trong các phần nhỏ sau đây
- `indexOf() và lastIndexOf()` tìm kiếm một mảng cho mỗi phần tử có giá trị được chỉ định và trả về index của phần tử đầu tiên được tìm thấy như vậy hoặc -1 nếu không tìm thấy phần tử nào. `indexOf()` tìm kiếm mảng từ đầu đến cuối và `lastIndexOf()` tìm kiếm từ cuối lên đầu
    
    ```jsx
    let a = [0,1,2,1,0];
    a.indexOf(1) // => 1: a[1] là 1
    a.lastIndexOf(1) // => 3: a[3] là 1
    a.indexOf(3) // => -1: không có phần tử nào có giá trị 3
    ```
    
- `indexOf() và lastIndexOf()` so sánh đối số của chúng với phần tử mảng bằng cách sử dụng toán tử `===`. Nếu phần tử của bạn chứa các object thay vì giá trị nguyên thuỷ, thì các method này sẽ kiểm tra xem hai tham chiếu có cùng tham chiếu chính xác đến một object hay không. Nếu bạn thực sự muốn xem xét nội dung của một object, hãy thử sử dụng method find() với hàm vị ngữ tuỳ chỉnh của riêng bạn
- `indexOf và lastIndexOf()` nhận một đối số thứ 2 là tuỳ chọn chỉ định index mảng để bắt đầu tìm kiếm. Nếu đối số này bị bỏ qua, indexOf bắt đầu tử đầu và lastIndexOf bắt đầu từ cuối. Các giá trị âm được phép cho đối số thứ 2 và được coi là một offset từ cuối mảng, như đối với method `slice()`: ví dụ -1 chỉ định giá trị cuối của mảng
- Hàm sau khi tìm kiếm một mảng cho một giá trị được chỉ định và trả về một mảng của tất cả các index phù hợp. Điều này cho thấy cách đối số thứ 2  cho `indexOf()` có thể được sử dụng để tìm các kết quả khớp ngoài kết quả khớp đầu tiên
    
    ```jsx
    // Tìm tất cả các lần xuất hiện của giá trị x trong mảng a và trả về một mảng
    // của các chỉ mục phù hợp
    function findall(a, x) {
      let results = [], // Mảng các chỉ mục mà chúng ta sẽ trả về
      len = a.length, // Độ dài của mảng cần tìm kiếm
      pos = 0; // Vị trí để tìm kiếm từ đó
      while(pos < len) { // Trong khi còn nhiều phần tử để tìm kiếm ...
        pos = a.indexOf(x, pos); // Tìm kiếm
        if (pos === -1) break; // Nếu không tìm thấy gì, chúng ta đã xong.
        results.push(pos); // Nếu không, hãy lưu trữ chỉ mục trong mảng
        pos = pos + 1; // Và bắt đầu tìm kiếm tiếp theo ở phần tử tiếp theo
      }
      return results; // Trả về mảng các chỉ mục
    }
    ```
    
- Lưu ý rằng chuỗi có các method indexOf() và lastIndexOf() hoạt động giống như các method mảng này, ngoài trừ đối số thứ 2 âm được gọi là 0
- `includes()` method của ES2016 nhận một đối số duy nhất và trả về `true` nếu mảng chứa giá trị đó hoặc `false` nếu ngược lại. Nó không cho bạn biết index của giá trị, chỉ cho biết nó có tồn tại hay không. `includes()` method có hiệu quả là một bài kiểm tra tư cách thành viên tập hợp cho các mảng. Tuy nhiên, lưu ý rằng mảng không phải là một đại diện hiệu quả cho tập hợp và nếu bạn đang làm việc với nhiều hơn một vài phần tử, bạn nên sử dụng object `Set` thực (11.1)
- `includes()` method hơi khác so với method `indexOf()` theo một cách quan trọng. `indexOf()` kiểm tra sự bằng nhau bằng cách sử dụng  cùng một thuật toán mà toán tử `===` thực hiện và thuật toán bằng nhau đó coi giá trị not-a-number (NaN) là khác với mọi giá trị khác, bao gồm cả chính nó. `includes()` sử dụng một phiên bản bằng nhau hơi khác một chút, coi `NaN` bằng chính nó. Điều này có nghĩa là `indexOf()` sẽ không phát hiện giá trị `NaN` trong mảng, nhưng `includes()` sẽ
    
    ```jsx
    let a = [1,true,3,NaN];
    a.includes(true) // => true
    a.includes(2) // => false
    a.includes(NaN) // => true
    a.indexOf(NaN) // => -1; indexOf không thể tìm thấy NaN
    ```
    
- `sort()` sắp xếp các phần tử của mảng tại chỗ và trả về mảng đã sắp xếp. Khi `sort()` được gọi mà không có đối số, nó sẽ sắp xếp các phần tử mảng theo thứ tự bảng chữ cái (tạm thời chuyển đổi chúng thành chuỗi để thực hiện so sánh, nếu cần)
    
    ```jsx
    let a = ["banana", "cherry", "apple"];
    a.sort(); // a == ["apple", "banana", "cherry"]
    ```
    
- Nếu một mảng chứa các phần tử `undefined`, chúng sẽ được sắp xếp đến cuối mảng
- Để sắp xếp một mảng theo một thứ tự nào đó khác với thứ tự bảng chữ cái, bạn phải chuyển một hàm so sánh làm đối số cho `sort()`. Hàm này quyết định xem hai đối số nào của nó sẽ xuất hiện trước trong mảng đã sắp xếp. Nếu đối số đầu tiên xuất hiện trước đối số thứ 2, thì hàm so sánh trả về một số nhỏ hơn 0. Nếu đối số đầu tiên xuất hiện sau đối số thứ 2 trong mảng đã sắp xếp, thì hàm sẽ trả về một số lớn hơn 0. Và nếu hai giá trị tương đương ( tức là nếu thứ tự của chúng không liên quan), thì hàm so sánh sẽ trả về 0
- Vì vậy, ví dụ: để sắp xếp các phần tử mảng theo thứ tự số thay vì thứ tự bảng chữ cái, bạn có thể làm như sau
    
    ```jsx
    let a = [33, 4, 1111, 222];
    a.sort(); // a == [1111, 222, 33, 4]; thứ tự bảng chữ cái
    a.sort(function(a,b) { // Truyền hàm so sánh
      return a-b; // Trả về <0, 0 hoặc> 0, tùy thuộc vào thứ tự
    }); // a == [4, 33, 222, 1111]; thứ tự số
    a.sort((a,b) => b-a); // a == [1111, 222, 33, 4]; đảo ngược thứ tự số
    ```
    
- Ví dụ khác về việc sắp xếp các mục mảng, bạn có thể thực hiện sắp xếp theo thứ tự bảng chữ cái không phân biệt hoa thường trên một mảng chuỗi bằng cách chuyển một hàm so sánh chuyển đổi cả 2 đối số của nó thành chữ thường (với `toLowerCase()` ) trước khi so sánh chúng
    
    ```jsx
    let a = ["ant", "Bug", "cat", "Dog"];
    a.sort(); // a == ["Bug","Dog","ant","cat"]; sắp xếp phân biệt chữ hoa chữ thường
    a.sort(function(s,t) {
      let a = s.toLowerCase();
      let b = t.toLowerCase();
      if (a < b) return -1;
      if (a > b) return 1;
      return 0;
    }); // a == ["ant","Bug","cat","Dog"]; sắp xếp không phân biệt chữ hoa chữ thường
    ```
    
- `reverse()` method đảo ngược thứ tự của các phần tử mảng và trả về mảng đảo ngược. Nó làm điều này tại chỗ; nói cách khác, nó không tạo ra một mảng mới với các phần tử được sắp xếp lại mà thay vào đó sắp xếp lại chúng trong mảng đã tồn tại
    
    ```jsx
    let a = [1,2,3];
    a.reverse(); // a == [3,2,1]
    ```
    

### **7.8.7 Chuyển đổi Mảng thành Chuỗi**

- Class `Array` định nghĩa 3 method có thể chuyển đổi mảng thành chuỗi, thường là điều bạn có thể làm khi tạo log và thông báo lỗi. (Nếu bạn muốn lưu nội dung của mảng ở dạng văn bản để sử dụng lại sau này, hãy tuần tự hoá mảng bằng `JSON.stringify()` thay vì sử dụng các method được mô tả trước đây)
- Method `join()` chuyển đổi tất cả các phần tử của mảng thành chuỗi và nối chúng lại với nhau, trả về chuỗi kết quả. Bạn có thể định nghĩa một chuỗi tuỳ chọn để phân tách các phần tử trong chuỗi kết quả. Nếu không có chuỗi phân cách nào được chỉ định, dấu phẩy sẽ được sử dụng
    
    ```jsx
    let a = [1, 2, 3];
    a.join() // => "1,2,3"
    a.join(" ") // => "1 2 3"
    a.join("") // => "123"
    let b = new Array(10); // Một mảng có độ dài 10 không có phần tử
    b.join("-") // => "---------": một chuỗi gồm 9 dấu gạch nối
    ```
    
- `join()` method là nghịch đảo của `String.split()` method, method tại ra một mảng bằng cách chia một chuỗi thành các phần
- Mảng, giông như tất cả các object Js, đều có method `toString()`. Đối với một mảng, method này hoạt động như `join()` method mà không có đối số
    
    ```jsx
    [1,2,3].toString() // => "1,2,3"
    ["a", "b", "c"].toString() // => "a,b,c"
    [1, [2,"c"]].toString() // => "1,2,c"
    ```
    
- Lưu ý rằng đầu ra không bao gồm dấu ngoặc vuông hoặc bất kỳ loại dấu phân cách nào khác xung quanh giá trị mảng
- `toLocaleString()` là phiên bản địa hoá của `toString()`. Nó chuyển đổi mỗi phần tử mảng thành chuỗi bằng cách gọi `toLocaleString()` method của phần tử, sau đó nối các chuỗi kết quả bằng cách sử dụng chuỗi phân tách cụ thể theo miền địa phương (và được xác định bởi triển khai)

### **7.8.8 Hàm Mảng Tĩnh**

- Ngoài các method mảng mà chúng ta đã ghi lại, class `Array` cũng định nghĩa 3 hàm tĩnh mà bạn có thể gọi thông qua hàm tạo `Array` chứ không phải trên các mảng. `Array.of()` và `Array.from()` là các method factory để tạo mảng mới. Chúng đã được ghi lại trong 7.1.4 và 7.1.5
- Hàm mảng tĩnh còn lại là `Array.isArray()`, rất hữu ích để xác định xem một giá trị chưa biết có phải là mảng không
    
    ```jsx
    Array.isArray([]) // => true
    Array.isArray({}) // => false
    ```

