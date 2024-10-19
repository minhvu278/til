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
