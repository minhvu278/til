# Types, Values, and Variables
- Các chương trình máy tính hoạt động bằng cách thao tác các **values**, chẳng hạn như số 3.14 hay string “Hello World”. Các loại value có thể được biểu diễn và thao tác trong một ngôn ngữ lập trình được gọi là **types**, và một trong những đặc điểm cơ bản nhất trong ngôn ngữ lập trình là tập hợp các `types` mà nó hỗ trợ. Khi 1 chương trình cần lưu giữ 1 value để có thể sử dụng trong tương lai, nó sẽ gán value đó cho 1 **variables**, Variable có tên và chúng cho phép sử dụng các tên đó trong chương trình của chúng ta để tham chiếu đến **values**. Cách thức hoạt động của **variables** là một đặc điểm cơ bản khác của bất kỳ ngôn ngữ lập trình nào. Chương này sẽ giải thích các `types, values và variables` trong Js. Nó bắt đầu bằng 1 cái nhìn tổng quan và một số định nghĩa

## 3.1 Overview and Definitions

- Các types của Js được chia làm 2 loại: `primitive type` (kiểu nguyên thuỷ) và `object type`
- Các **primitive types** của JavaScript bao gồm **numbers** (số), **strings of text** (chuỗi văn bản) (được gọi là **strings**) và **Boolean truth values** (giá trị đúng/sai Boolean) (được gọi là **booleans**).
- Một phần đáng kể của chương này dành riêng để giải thích chi tiết về các **types** số (§3.2) và chuỗi (§3.3) trong JavaScript. **Booleans** được đề cập trong §3.4.
- Các **values** đặt biệt của js là `null` và `undefined` là **primitive value,** nhưng chúng không phải là number hoặc string hay boolean. Mỗi **value** thường được coi là thành viên duy nhất của `type` đặc biệt của riêng nó.
- ES6 bổ sung 1 `type` đặc biệt mới, được gọi là `Symbol` cho phép định nghĩa các phần mở rộng ngôn ngữ mà không ảnh hưởng đến khả năng tương thích ngược
- Bất kỳ value nào không phải là number, string, boolean, symbol, null hoặc undefined thì đều la `object` . `Object` là tập hợp các `properties` và mỗi `property` có một tên và 1 value (là primitive value hoặc 1 object khác). Một object rất đặc biệt, `global object` được đề cập trong 3.7, nhưng phạm vi được bao quát chung hơn và chi tiết hơn về Object nằm trong chương 6
- `Object` Js thông thường là một tập hợp các values đặt tên không có thứ tự. Ngôn ngữ cũng định nghĩa 1 loại object đặc biệt, được gọi là arrays, đại diện cho 1 tập hợp các values được đánh số thứ tự. Js bao gồm cú pháp đặc biệt để làm việc với arrays và array có 1 số hành vi đặc biệt phân biệt chúng với object thông thường. Arrays là chủ đề của chương 7
- Ngoài object và array cơ bản, Js định nghĩa 1 số object types hữu ích khác. **Object** `Set` đại diện cho một tập hợp các values. **Object** `Map` đại diện cho 1 ánh xạ từ key đến values. Các types “mảng được nhập” khác nhau tạo điều kiện cho các hoạt động trên mảng byte và dữ liệu nhị phân khác. Type `RegExp` đại diện cho mẫu văn bản và cho phép các thao tác khớp, tìm kiếm và thay thế phức tạp trên string. `Error` và các **subtypes** của nó đại diện cho các lỗi có thể phát sinh trong khi thực thi code Js. Tất cả các type được đề cập trong chương 11
- Js khác với các ngôn ngữ lập trình khác ở chỗ functions và classes không chỉ là một phần của cú pháp ngôn ngữ: Bản thân chúng là values có thể được thao tác bởi các chương trình Js. Giống như bất ký value Js nào không phải là **primitive value, functions và classes** là một loại object đặc biệt. Chúng được đề cập chi tiết trong chương 8 và 9
- Trình thông dịch Js thực hiện **automatic garbage collection** (thu gom rác tự động) để quản lý bộ nhớ. Điều này có nghĩa là 1 dev Js thường không cần phải lo lắng về huỷ hoặc giải phóng objects hoặc các values khác. Khi 1 value không còn reachable (có thể truy cập) - Khi 1 chương trình không còn cách nào để tham chiếu đến nó - trình thông dịch biết rằng nó không bao giờ có thể được sử dụng lại và tự động thu hồi bộ nhớ mà nó đang chiếm dụng
- Js hỗ trợ phong cách lập trình OOP. Nói 1 cách dễ hiểu, điều này có nghĩa là thay vì các functions được định nghĩa chung để hoạt động trên values của type khác nhau, bản thân type sẽ định nghĩa 1 method để làm việc với values. Ví dụ để sắp xếp các element của mảng a, chúng ta không truyền a cho function `sort()` . Thay vào đó, chúng ta gọi method `sort()` của `a`
    
    ```jsx
    a.sort(); // Phiên bản hướng đối tượng của sort(a).
    ```
    
- Định nghĩa method được đề cập trong chương 9. Về mặt kỹ thuật, chỉ các `object` Js mới có `methods`. Nhưng **numbers, strings, booleans** và **values** **symbol** hoạt động như thể chúng có **methods**. Trong JavaScript, null và undefined là những **values** duy nhất mà **methods** không thể được gọi trên đó.
- Các object types của js là `mutable` (có thể thay đổi) và các primitive types của nó là immutable (không thể thay đổi). Value của type mutable có thể thay đổi: chương trình Js có thể thay đổi value của properties của object và element của mảng. **Numbers, booleans, symbols, null** và undefined là **immutable** — thậm chí không có ý nghĩa gì khi nói về việc thay đổi **value** của một **number**, chẳng hạn. **Strings** có thể được coi như mảng ký tự và bạn có thể mong đợi chúng là mutable. Tuy nhiên trong Js, string là immutable: bạn có thể truy cập văn bản tại bất kỳ index nào của string, nhưng js không cung cấp cách nào để thay đổi văn bản của string hiện có. Sự khác biệt được khám phá trong 3.8
- Các quy tắc chuyển đổi value tự do của Js ảnh hưởng đến định nghĩa về `equality` (bằng nhau) của nó. Và toán tử bằng (==) thực hiện chuyển đổi type được mô tả trong 3.9.1 (Tuy nhiên trong thực tế, toán tử == không còn được dùng nữa mà thay vào đó bằng toán tử nghiệm ngặt ===)
- **Constant và variables** cho phép bạn sử dụng tên để tham chiếu đến values trong chương trình của mình. Constant được khai báo là `const` và variables được khai báo là `let` (hoặc `var` trong các chương trình Js cũ hơn). Constant và variables là `untyped` (không có kiểu) khai báo không chỉ định loại values nào sẽ được gán
- Như bạn có thể thấy từ phần giới thiệu dài này, đây là 1 chương trình bày rộng rãi, giải thích nhiều chi tiết cơ bản về dữ liệu được biểu diễn và thao tác trong JS. Chúng ta hãy bắt đầu bằng cách đi sâu vào chi tiết về number và text của Js
## 3.2 Numbers

- Type number chính của Js, **Number**, được sử dụng để biểu diễn số nguyên và xấp xỉ số thực. Js biểu diễn số bằng cách sử dụng định dạng dấu phẩy động 64-bit được định nghĩa bởi tiêu chuẩn IEEE 7, có nghĩa là nó có thể biểu diễn các số lớn tới ±1.7976931348623157 × 10<sup>308</sup> và nhỏ tới ±5 × 10<sup>-324</sup>.
- Định dạng số Js cho phép bạn biểu diễn chính xác tất cả các số nguyên trong khoảng từ −9.007.199.254.740.992 (−2<sup>53</sup>) đến 9.007.199.254.740.992 (2<sup>53</sup>), bao gồm cả 2. Nếu bạn sử dụng các giá trị số nguyên lớn hơn mức này, bạn có thể mất độ chính xác trong các chữ số ở cuối. Tuy nhiên lưu ý rằng một phép toán nhất định trong Js (chẳng hạn như lập index của mảng và các toán tử bit được mô tả trong chương 4). Được thực hiện với số nguyên 32-bit
- Khi một số xuất hiện trực tiếp trong chương trình Js, nó được gọi là `numeric literal` (giá trị ký tự số). Js hỗ trợ numeric literal ở một số định dạng, như được mô tả trong các phần sau. Lưu ý rằng bất kỳ numeric literal nào cũng có thể được đặt trước bởi dấu trừ để làm cho số âm

### 3.2.1. Integer Literals

- Trong Js, số nguyên cơ số 10 được viết dưới dạng một chuỗi các chữ số. VD
    
    ```jsx
    0
    3
    10000000
    ```
    
- Ngoài integer literals cơ số 10, Js còn nhận ra các giá trị thập lục phân (cơ số 16). Literal thập lục phân bắt đầu bằng 0x hoặc 0X, theo sau là một chuỗi các chữ số thập lục phân. Các chữ số thập lục phân là một trong các chữ số từ 0 đến 9 hoặc các chữ cái từ a (hoặc A) đến f (hoặc F), đại diện cho các giá trị từ 10 đến 15. Dưới đây là ví dụ về integer literal thập lục phân
    
    ```jsx
    0xff // => 255: (15*16 + 15)
    0xBADCAFE // => 195939070
    ```
    
- Trong ES6 trở lên, bạn cũng có thể biểu thị số nguyên ở dạng nhị phân(cơ số 2) hoặc bát phân (cơ số 8) bằng cách sử dụng tiền tố 0b và 0o (hoặc 0B và 0O) thay vì 0x
    
    ```jsx
    0b10101 // => 21: (1*16 + 0*8 + 1*4 + 0*2 + 1*1)
    0o377 // => 255: (3*64 + 7*8 + 7*1)
    ```
    

### 3.2.2 Floating-Point Literals

- `Floating-point literals` cũng có thể được biểu diễn bằng ký tự mũ: Một số thực theo sau là chữ `e` (hoặc `E`), theo sau dấu cộng, trừ tuỳ chọn, theo sau là số mũ nguyên. Ký hiệu này biểu thị số thực nhân với 10 mũ số mũ
- Nói 1 cách ngắn gọn hơn, cú pháp sẽ là
    
    ```jsx
    [digits][.digits][(E|e)[(+|-)]digits]
    ```
    
- Ví dụ
    
    ```jsx
    3.14
    2345.6789
    .333333333333333333
    6.02e23 // 6.02 × 10²³
    1.4738223E-32 // 1.4738223 × 10⁻³²
    ```
    

### SEPARATORS IN NUMERIC LITERALS

- Bạn có thể sử dụng dấu gạch dưới trong numeric literals để chia các literals dài thành các phần nhỏ dễ đọc hơn

```jsx
let billion = 1_000_000_000; // Dấu gạch dưới làm dấu phân cách hàng nghìn.
let bytes = 0x89_AB_CD_EF; // Làm dấu phân cách byte.
let bits = 0b0001_1101_0111; // Làm dấu phân cách nibble.
let fraction = 0.123_456_789; // Cũng hoạt động trong phần phân số.
```

- Tại thời điểm viết bài này vào năm 2020, dấu gạch dưới trong `numeric literals` vẫn chưa được chính thức tiêu chuẩn hoá như 1 phần của Js. Nhưng chúng đang trong giai đoạn nâng cao của quá trình tiêu chuẩn hoá và được triển khai bởi tất cả các trình duyệt chính và bởi Node

### 3.2.3 Arithmetic in JavaScript

- Các chương trình Js làm việc với số bằng cách sử dụng các toán tử số học mà chúng cung cấp. Chúng sử dụng +-*/. ES6 bổ sung thêm `**` cho phép luỹ thừa, chi tiết đầy đủ sẽ được viết trong chương 4
- Ngoài các toán tử số học cơ bản này, Js hỗ trợ các phép toán phức tạp hơn thông qua một tập hợp các hàm và được hằng số định nghĩa là `properties` của object Math
    
    ```jsx
    Math.pow(2,53) // => 9007199254740992: 2 mũ 53
    Math.round(.6) // => 1.0: làm tròn đến số nguyên gần nhất
    Math.ceil(.6) // => 1.0: làm tròn lên đến số nguyên
    Math.floor(.6) // => 0.0: làm tròn xuống đến số nguyên
    Math.abs(-5) // => 5: giá trị tuyệt đối
    Math.max(x,y,z) // Trả về đối số lớn nhất
    Math.min(x,y,z) // Trả về đối số nhỏ nhất
    Math.random() // Số giả ngẫu nhiên x trong đó 0 <= x < 1.0
    Math.PI // π: chu vi của hình tròn / đường kính
    Math.E // e: Cơ số của logarit tự nhiên
    Math.sqrt(3) // => 3**0.5: căn bậc hai của 3
    Math.pow(3, 1/3) // => 3**(1/3): căn bậc ba của 3
    Math.sin(0) // Lượng giác: cũng có Math.cos, Math.atan, v.v.
    Math.log(10) // Logarit tự nhiên của 10
    Math.log(100)/Math.LN10 // Logarit cơ số 10 của 100
    Math.log(512)/Math.LN2 // Logarit cơ số 2 của 512
    Math.exp(3) // Math.E mũ 3
    ```
    
- ES6 định nghĩa các hàm trên object Math
    
    ```jsx
    Math.cbrt(27) // => 3: căn bậc ba
    Math.hypot(3, 4) // => 5: căn bậc hai của tổng bình phương của tất cả các đối số
    Math.log10(100) // => 2: Logarit cơ số 10
    Math.log2(1024) // => 10: Logarit cơ số 2
    Math.log1p(x) // Logarit tự nhiên của (1+x); chính xác cho x rất nhỏ
    Math.expm1(x) // Math.exp(x)-1; nghịch đảo của Math.log1p()
    Math.sign(x) // -1, 0 hoặc 1 cho các đối số <, == hoặc > 0
    Math.imul(2,3) // => 6: phép nhân được tối ưu hóa của các số nguyên 32-bit
    Math.clz32(0xf) // => 28: số bit 0 đứng đầu trong số nguyên 32-bit
    Math.trunc(3.9) // => 3: chuyển đổi thành số nguyên bằng cách cắt bớt phần phân số
    Math.fround(x) // Làm tròn đến số dấu phẩy động 32-bit gần nhất
    Math.sinh(x) // Sin hyperbolic. Cũng có Math.cosh(), Math.tanh()
    Math.asinh(x) // Arcsin hyperbolic. Cũng có Math.acosh(), Math.atanh()
    ```
    
- Số học trong Js không gây ra lỗi trong trường hợp tràn số, thiếu số hoặc chia cho 0. Khi kết quả của phép toán số lớn hơn số biểu diễn được lớn nhất (tràn số), kết quả là giá trị vô cùng đặc biệt, `Infinity`. Tương tự khi giá trị tuyệt đối của của giá trị âm trở nên lớn hơn giá trị tuyệt đối của số âm biểu diễn được lớn nhất, kết quả là âm vô cùng, `-Infinity` . Các giá trị vô cùng hoạt động như bạn mong đợi: +-*/` chúng sẽ dẫn đến giá trị vô cùng (có thể với dấu bị đảo ngược)
- Thiếu số xảy ra khi kết quả của phép toán gần với số 0 hơn số biểu diễn được nhỏ nhất. Trong trường hợp này, Js trả về 0. Nếu thiếu số xảy ra từ số âm, Js trả về 1 giá trị đặc biệt được gọi là `số 0 âm` . Giá trị này gần như hoàn toàn không thể phân biệt được với số 0 thông thường và các dev hiếm khi cần phát hiện nó
- Chia cho 0 không phải là lỗi trong Js: nó chỉ đơn giản là trả về `Infinity` hoặc `-Infinity` . Tuy nhiên có 1 ngoại lệ: 0 chia cho 0 không có giá trị được xác định rõ và kết quả của phép toán này là giá trị `not-a-number` (không phải là số) đặc biệt, `NaN`. `NaN` cũng phát sinh khi bạn cố chia vô cùng cho vô cùng, lấy căn bậc 2 của số âm hoặc sử dụng toán tử số học với toán hạng không phải số mà không thể chuyển đổi thành số
- Js định nghĩa trước các hằng số toàn cụ `Infinity` và `NaN` để giữ giá trị dương vô cùng và giá trị not-a-number và các giá trị này cũng có sẵn dưới dạng `properties` của object `Number`
    
    ```jsx
    Infinity // Số dương quá lớn để biểu diễn
    Number.POSITIVE_INFINITY // Cùng giá trị
    1/0 // => Infinity
    Number.MAX_VALUE * 2 // => Infinity; tràn số
    -Infinity // Số âm quá lớn để biểu diễn
    Number.NEGATIVE_INFINITY // Cùng giá trị
    -1/0 // => -Infinity
    -Number.MAX_VALUE * 2 // => -Infinity
    NaN // Giá trị not-a-number
    Number.NaN // Cùng giá trị, viết theo cách khác
    0/0 // => NaN
    Infinity/Infinity // => NaN
    Number.MIN_VALUE/2 // => 0: thiếu số
    -Number.MIN_VALUE/2 // => -0: số 0 âm
    -1/Infinity // -> -0: cũng là số 0 âm
    -0
    // Các thuộc tính Number sau được định nghĩa trong ES6
    Number.parseInt() // Giống như hàm parseInt() toàn cục
    Number.parseFloat() // Giống như hàm parseFloat() toàn cục
    Number.isNaN(x) // x có phải là giá trị NaN không?
    Number.isFinite(x) // x có phải là số và hữu hạn không?
    Number.isInteger(x) // x có phải là số nguyên không?
    Number.isSafeInteger(x) // x có phải là số nguyên -(2**53) < x < 2**53 không?
    Number.MIN_SAFE_INTEGER // => -(2**53 - 1)
    Number.MAX_SAFE_INTEGER // => 2**53 - 1
    Number.EPSILON // => 2**-52: chênh lệch nhỏ nhất giữa các số
    ```
    
- Giá trị not-a-number có 1 tính năng bất thường trong Js: nó không bằng bất kỳ giá trị nào khác, kể cả chính nó. Điều này có nghĩa là bạn không thể viết `x = NaN` để xác định xem biến x có phải là NaN không. Thay vào đó, bạn phải viết `x != x` hoặc `Number.isNaN(x)` . Các biểu thức đó sẽ là true nếu và chỉ khi x có giá trị với hằng số global NaN
- Function toàn cục `isNaN()`  tương tự như `Number.isNaN()` . Nó trả về true nếu đối số của nó là NaN hoặc nếu đối số của nó là giá trị không phải số mà không thể chuyển đổi thành số. Function liên quan `Number.isFinite()` trả về true nếu đối số của nó là số khác với `NaN, Infinity hoặc -Infinity` . Function global `isFinite()` trả về true nếu đối số của nó là hoặc có thể được chuyển đổi thành số hữu hạn
- Giá trị số âm 0 cũng hơi bất thường. Nó so sánh bằng (ngay cả khi sử dụng kiểm tra nghiệm ngặt của Js) với số 0 dương, có nghĩa là cả 2 giá trị đều gần như không thể phân biệt được, ngoại trừ khi sử dụng làm số chia
    
    ```jsx
    let zero = 0; // Số 0 thông thường
    let negz = -0; // Số 0 âm
    zero === negz // => true: số 0 và số 0 âm bằng nhau
    1/zero === 1/negz // => false: Infinity và -Infinity không bằng nhau
    ```
    

### 3.2.4 Binary Floating-Point and Rounding Errors

- Có vô số số thực, nhưng chỉ có một số hữu hạn trong số chúng (chính xác là 18.437.736.874.454.810.627) có thể được biểu diễn chính xác bằng dạng dấu chấm phẩy động của Js. Điều này có nghĩa là khi bạn làm việc với số thực trong Js, biểu diễn của số thường là một xấp xỉ của số thực tế
- Biểu diễn dấu chấm phẩy động IEEE-754 được sử dụng bởi Js (và hầu hết mọi ngôn ngữ lập trình khác) là biểu diễn nhị phân, có thể biểu diễn chính xác các phân số như 1/2, 1/8 và 1/1024. Thật không may, các phân số mà chúng ta sử dụng phổ biến nhất (đặt biệt là khi sử dụng các phép toán tài chính) là phân số thập phân 1/10, 1/100,… Biểu diễn dấu chấm phẩy động nhị phân không thể biểu diễn chính xác số đơn giản như 0.1
- Số Js có độ chính xác cao và có thể xấp xỉ 0.1 rất gần. Nhưng thực tế, con số này không được biểu diễn chính xác có thể dẫn đến các vấn đề. Hãy xem xét ví dụ này
    
    ```jsx
    let x = .3 - .2; // ba mươi xu trừ hai mươi xu
    let y = .2 - .1; // hai mươi xu trừ mười xu
    x === y // => false: hai giá trị không giống nhau!
    x === .1 // => false: .3-.2 không bằng .1
    y === .1 // => true: .2-.1 bằng .1
    ```
    
- Do lỗi làm tròn, chênh lệch giữa các xấp xỉ 0.3 và 0.2 không hoàn toàn giống nhau với các xấp xỉ của 0.2 và 0.1. Điều quan trọng là phải hiểu vấn đề này không phải đặc thù của Js: nó ảnh hưởng đến bất kỳ ngôn ngữ lập trình nào sử dụng dấu chấm phẩy động nhị phân. Ngoài ra, lưu ý rằng các giá trị `x` và `y` trong code được hiển thị ở đây rất gần nhau và với giá trị chính xác. Các giá trị được tính toán là đủ cho hầu hết các mục đích; vấn đề chỉ là phát sinh khi chúng ta cùng cố gắng so sánh các giá trị để kiểm tra `equality`
- Nếu những xấp xỉ dấu phẩy động này có vấn đề đối với chương trình của bạn, hãy cân nhắc sử dụng số nguyên được chia theo tỉ lệ. Ví dụ bạn có thể thao tác các giá trị tiền tệ dưới dạng số nguyên thay vì đô la phân số

### 3.2.5 Arbitrary Precision Integers with BigInt

- Một trong những tính năng mới nhất của Js, được định nghĩa trong ES2020, là 1 type mới được gọi là `BigInt` . Tính năng đến đầu 2020, nó được triển khai trong Chrome, Firefox, Edge và Node và có một bản triển khai đang được tiến hành trong Safari. Như tên gọi của nó, Bigint là một số type có giá trị là số nguyên. Type này đã được thêm vào Js chủ yếu để cho phép biểu diễn các số nguyên 64 bit, điều này được yêu cầu để tương thích với nhiều ngôn ngữ lập trình API khác. Nhưng giá trị Bigint này có thể có hàng nghìn hoặc thậm chí hàng triệu chữ số, nếu bạn cần làm việc với những con số lớn như vậy. (Tuy nhiên lưu ý rằng các triển khai BigInt không phù hợp cho mật mã vì chúng không cố ngăn chặn các cuộc tấn công định thời)
- `Literal BigInt` được viết dưới dạng một chuỗi các chữ số theo sau là chữ `n` viết thường. Theo mặc định, chúng ở cơ số 10, nhưng bạn có thể sử dụng tiền tố `0b, 0o, 0x` cho `BigInt` nhị phân, bát phân và thập lục phân
    
    ```jsx
    1234n // Một literal BigInt không quá lớn
    0b111111n // Một BigInt nhị phân
    0o7777n // Một BigInt bát phân
    0x8000000000000000n // => 2n**63n: Một số nguyên 64-bit
    ```
    
- Bạn có thể sử dụng `BigInt()` như 1 hàm để chuyển đổi số hoặc chuỗi Js thông thường thành giá trị `BigInt`
    
    ```jsx
    BigInt(Number.MAX_SAFE_INTEGER) // => 9007199254740991n
    let string = "1" + "0".repeat(100); // 1 theo sau bởi 100 số 0.
    BigInt(string) // => 10n**100n: một googol
    ```
    
- Số học với các giá trị BigInt hoạt động giống như các số Js thông thường, ngoại trừ việc chia sẻ bỏ bất kỳ phần dư nào và làm tròn xuống (về phía 0)
    
    ```jsx
    1000n + 2000n // => 3000n
    3000n - 2000n // => 1000n
    2000n * 3000n // => 6000000n
    3000n / 997n // => 3n: thương số là 3
    3000n % 997n // => 9n: và phần dư là 9
    (2n ** 131071n) - 1n // Số nguyên tố Mersenne có 39457 chữ số thập phân
    ```
    
- Mặc dù các toán tử +, -, *, /, % và ** tiêu chuẩn hoạt động với **BigInt**, nhưng điều quan trọng là bạn cần phải hiểu rằng không được phép trộn toán hạng `BigInt` với toán hạng thông thường. Điều này, thoạt đầu nghe có vẻ khó hiểu, nhưng có 1 lý do chính đáng cho nó. Nếu 1 type số tổng quát hơn type kia, thì sẽ dễ dàng định nghĩa số học trên các toán hạng hỗn hợp để chỉ đơn giản là trả về giá trị của type tổng quát hơn. Nhưng không có type nào tổng quát hơn type kia: BigInt có thể biểu diễn các giá trị cực kỳ lớn, làm cho nó tổng quát hơn so với các số thông thường. Nhưng `BigInt` chỉ có thể biểu diễn số nguyên, làm cho type số Js thông thường tổng quát hơn. Không có cách nào để giải quyết vấn đề này, vì vậy Js né tránh nó bằng cách đơn giản là không cho phép các toán hạng hỗn hợp cho các toán tử số học
- Ngược lại với các toán tử so sánh hoạt động với các type hỗn hợp
    
    ```jsx
    1 < 2n // => true
    2 > 1n // => true
    0 == 0n // => true
    0 === 0n // => false: === cũng kiểm tra equality kiểu
    ```
    
- Các toán tử bit thường được hoạt động với các toán hạng BigInt. Tuy nhiên, không có hàm nào của object Math chấp nhận toán hạng BigInt

### 3.2.6 Dates and Times

- Js định nghĩa class `Date` đơn giản để biểu diễn và thao tác các số đại diện cho ngày và giờ. `Date` của Js là object, nhưng chúng cũng có biểu diễn số dưới dạng timestamp chỉ số mili giây đã trôi qua kể từ ngày 1/1/1970
    
    ```jsx
    let timestamp = Date.now(); // Thời gian hiện tại dưới dạng timestamp (một số).
    let now = new Date(); // Thời gian hiện tại dưới dạng object Date.
    let ms = now.getTime(); // Chuyển đổi thành timestamp mili giây.
    let iso = now.toISOString(); // Chuyển đổi thành chuỗi ở định dạng tiêu chuẩn.
    ```
    
- Class `Date` và các methods của nó được đề cập chi tiết trong 11.4 . Nhưng chúng ta sẽ thấy object Date một lần nữa trong 3.9.3 khi mà chúng ta xem xét về các chuyển đổi type của Js

## 3.3. Text
- Kiểu dữ liệu trong Js để biểu diễn văn bản là string. String là các chuỗi ký tự 16bit bất biến có thứ tự, mỗi giá trị thường đại diện cho một ký tự Unicode. Độ dài của string là số lượng giá trị 16-bit mà nó chứa. String (và array - mảng) của Js sử dụng index dựa trên 0: Giá trị 16-bit đầu tiên ở vị trí 0, giá trị thứ 2 ở vị trí 1,… **Empty string** là string có độ dài là 0
- Js không có type đặc biệt nào đại diện cho 1 phần tử duy nhất của string. Để biểu diễn giá trị 16-bit duy nhất, chỉ cần sử dụng string có độ dài là 1

### CHARACTERS, CODEPOINTS, AND JAVASCRIPT STRINGS

- Js sử dụng mã hoá UTF-16 của bộ ký tự và string Js là chuỗi các giá trị 16-bit không dấu. Các ký tự Unicode được sử dụng phổ biến nhất (những ký tự từ “mặt phẳng đa ngôn ngữ cơ bản”) có các điểm mã phù hợp với 16-bit có thể được biểu diễn bằng một phần tử của string. Các ký tự Unicode có điểm mã không phù hợp với 16 bit được mã hoá theo quy tắc UTF16 - dưới dạng 1 chuỗi (được gọi là “cặp thay thế”) gồm 2 giá trị 16 bit. Điều này có nghĩa là string Js có độ dài 2 (giá trị 16bit) có thể chỉ đại diện cho một ký tự Unicode duy nhất
    
    ```jsx
    let euro = "€";
    let love = "❤";
    euro.length // => 1: ký tự này có một phần tử 16-bit
    love.length // => 2: mã hóa UTF-16 của ❤ là "\ud83d\udc99"
    ```
    
- Hầu hết các methods thao tác chuỗi được tạo ra bởi Js hoạt động trên các giá trị 16-bit, không phải ký tự. Chúng không xử lý cặp thay thế 1 cách đặc biệt, chúng không thực hiện chuẩn hoá string và thậm chí không đảm bảo rằng string UTF-16 được định dạng tốt
- Tuy nhiên, trong ES6, strings có thể lặp lại được và nếu bạn sử dụng vòng lặp `for/of` hoặc toán tử `...` với string, nó sẽ lặp lại các ký tự thực tế của string, không phải các giá trị 16-bit

### 3.3.1 String Literals

- Để bao gồm string trong chương trình Js, chỉ cần đặt giá trị string trong cặp dấu nháy đơn, nháy kép hoặc dấu bách tích phù hợp (’ hoặc “ hoặc `). Các ký tự dấu nháy kép và bách tích có thể chứa trong string được phân định bằng dấu nháy kép và dấu bách tích
    
    ```jsx
    "" // Chuỗi rỗng: nó có 0 ký tự
    'testing'
    "3.14"
    'name="myform"'
    "Wouldn't you prefer O'Reilly's book?"
    "τ is the ratio of a circle's circumference to its radius"
    `"She said 'hi'", he said.`
    ```
    
- String được phân định bằng dấu bách tích là 1 tính năng của ES6, cho phép các expression được nhúng trong (hoặc nội suy vào) string literal. Cú pháp nội suy expression này được đề cập trong 3.3.4
- Các phiên bản ban đầu của JS yêu cầu string literal được viết trên 1 dòng duy nhất và người ta thường thấy code Js tạo string dài bằng cách nối các string 1 dòng bằng toán tử +. Tuy nhiên từ ES5 bạn đã có thể ngắt string thành nhiều dòng bằng cách kết thúc mỗi dòng nhưng dòng cuối cùng bằng dấu (\). Cả dấu gạch chéo ngược và ký tự kết thúc dòng theo sau nó đều không phải là một phần của string literal. Nếu bạn cần bao gồm ký tự xuống dòng trong **string literal** được đặt trong dấu nháy đơn hoặc dấu nháy kép, hãy sử dụng chuỗi ký tự \n (được ghi lại trong phần tiếp theo)
- Cú pháp dấu bách tích ES6 cho phép strings được ngắt thành nhiều dòng, và trong trường hợp này, các ký tự kết thúc dòng là một phần của string literal
- Lưu ý rằng, khi bạn sử dụng dấu nháy đơn để phân định string của mình, bạn phải cẩn thận với các từ viết tắt và sở hữu cách tiếng Anh. Chẳng hạn như `can't`. Vì dấu nháy đơn trông giống với ký tự dấu nháy đơn, bạn phải dùng ký tự \  để “thoát” khỏi bất kỳ dấu nháy nào xuất hiện trong string được đặt trong dấu nháy đơn (escape squences) - chuỗi thoát được giải thích trong phần tiếp theo)
- Trong lập trình phía máy khách, code Js có thể chứa strings code HTML và code HTML có thể chứa string của Js. Giống như Js, HTML sử dụng dấu nháy đơn hoặc nháy kép để phân định string của nó. Do đó, khi kết hợp Js và HTML, bạn nên sử dụng 1 kiểu dấu nháy cho Js và kiểu còn lại cho HTML. Trong ví dụ sau, string “Thank you” được đặt trong dấu nháy đơn trong expression Js, sau đó được đặt trong dấu nháy kép trong thuộc tính trình xử lý sự kiện Js
    
    ```jsx
    <button onclick="alert('Thank you')">Click Me</button>
    ```
    

### 3.3.2 Escape Sequences in String Literals

- Ký tự \ có mục đích đặc biệt trong string Js. Kết hợp với 1 ký tự theo sau nó, nó đại diện cho 1 ký tự không thể biểu diễn được trong string. Ví dụ \n là đại diện cho ký tự xuống dòng
- Một ví dụ khác, đã đề cập trước đó, là escape sequence (\’) đại diện cho 1 ký tự dấu nháy đơn (hoặc dấu nháy). Escape sequences này hữu ích khi bạn bao gồm dấu nháy đơn trong string literal được chứa trong dấu nháy đơn. Bạn có thể thấy tại sao chúng được gọi là **escape sequences**: dấu gạch chéo ngược cho phép bạn thoát khỏi cách hiểu thông thường của ký tự nháy đơn. Thay vì sử dụng nó để đánh dấu kết thúc string, bạn sử dụng nó như 1 dấu nháy đơn
    
    ```jsx
    'You\'re right, it can\'t be a quote'
    ```
    
- Bảng 3-1 liệt kê các **escape sequences** của JavaScript và các ký tự mà chúng đại diện. Ba **escape sequences** là chung chung và có thể được sử dụng để đại diện cho bất kỳ ký tự nào bằng cách chỉ định mã ký tự Unicode của nó dưới dạng số thập lục phân. Ví dụ: chuỗi \xA9 đại diện cho ký hiệu bản quyền, có mã hóa Unicode được cung cấp bởi số thập lục phân A9. Tương tự, **escape sequence** \u đại diện cho ký tự Unicode tùy ý được chỉ định bởi bốn chữ số thập lục phân hoặc từ một đến năm chữ số khi các chữ số được bao bọc trong dấu ngoặc nhọn: \u03c0 đại diện cho ký tự π, ví dụ và \u{1f600} đại diện cho biểu tượng cảm xúc "mặt cười toe toét".
    
    ```jsx
    Chuỗi	Ký tự được biểu diễn
    \0	Ký tự NUL (\u0000)
    \b	Backspace (\u0008)
    \t	Tab ngang (\u0009)
    \n	Xuống dòng (\u000A)
    \v	Tab dọc (\u000B)
    \f	Form feed (\u000C)
    \r	Trả về đầu dòng (\u000D)
    \"	Dấu nháy kép (\u0022)
    \'	Dấu nháy đơn (\u0027)
    \\	Dấu gạch chéo ngược (\u005C)
    \xnn	Ký tự Unicode được chỉ định bởi hai chữ số thập lục phân nn
    \unnnn	Ký tự Unicode được chỉ định bởi bốn chữ số thập lục phân nnnn
    \u{n}	Ký tự Unicode được chỉ định bởi điểm mã n, trong đó n là từ một đến sáu chữ số thập lục phân từ 0 đến 10FFFF (ES6)
    ```
    
- Nếu ký tự \ đứng trước bất kỳ ký tự nào khác ngoài những ký tự được hiển thị trong Bảng trên, thì dấu gạch chéo ngược sẽ bị bỏ qua (mặc dù các phiên bản tương lai của ngôn ngữ có thể định nghĩa các **escape sequences** mới). Ví dụ: \# giống như #. Cuối cùng, như đã lưu ý trước đó, ES5 cho phép dấu gạch chéo ngược trước dấu xuống dòng để ngắt **string literal** thành nhiều dòng.

### 3.3.3 Working with Strings

- Một trong những tính năng tích hợp của Js là khả năng nối các strings(chuỗi). Nếu bạn sử dụng toán tử + với số, nó sẽ cộng chúng. Nhưng nếu bạn sử dụng nó với string, nó sẽ nối chúng bằng cách thêm chuỗi thứ 2 vào chuỗi thứ 1
    
    ```jsx
    let msg = "Hello, " + "world"; // Tạo ra chuỗi "Hello, world"
    let greeting = "Welcome to my blog," + " " + name;
    ```
    
- **Strings** có thể được so sánh với các toán tử so sánh bằng `===` và toán tử so sánh khác `!==` tiêu chuẩn: hai strings bằng nhau nếu và chỉ khi chúng bao gồm chính xác cùng một chuỗi các giá trị 16-bit. (Để so sánh và sắp xếp chuỗi theo ngôn ngữ mạnh mẽ hơn)
- Ngoài thuộc tính length này, Js cung cấp một API phong phú để làm việc với strings
    
    ```jsx
    let s = "Hello, world"; // Bắt đầu với một số văn bản.
    // Lấy các phần của chuỗi
    s.substring(1,4) // => "ell": ký tự thứ 2, thứ 3 và thứ 4.
    s.slice(1,4) // => "ell": giống nhau
    s.slice(-3) // => "rld": 3 ký tự cuối cùng
    s.split(", ") // => ["Hello", "world"]: tách tại chuỗi phân cách
    // Tìm kiếm trong chuỗi
    s.indexOf("l") // => 2: vị trí của chữ cái 'l' đầu tiên
    s.indexOf("l", 3) // => 3: vị trí của chữ cái 'l' đầu tiên tại hoặc sau vị trí 3
    s.indexOf("zz") // => -1: s không bao gồm chuỗi con "zz"
    s.lastIndexOf("l") // => 10: vị trí của chữ cái 'l' cuối cùng
    // Các hàm tìm kiếm Boolean trong ES6 trở lên
    s.startsWith("Hell") // => true: chuỗi bắt đầu bằng các ký tự này
    s.endsWith("!") // => false: s không kết thúc bằng ký tự đó
    s.includes("or") // => true: s bao gồm chuỗi con "or"
    // Tạo các phiên bản đã sửa đổi của chuỗi
    s.replace("llo", "ya") // => "Heya, world"
    s.toLowerCase() // => "hello, world"
    s.toUpperCase() // => "HELLO, WORLD"
    s.normalize() // Chuẩn hóa Unicode NFC: ES6
    s.normalize("NFD") // Chuẩn hóa NFD. Cũng có "NFKC", "NFKD"
    // Kiểm tra các ký tự riêng lẻ (16-bit) của chuỗi
    s.charAt(0) // => "H": ký tự đầu tiên
    s.charAt(s.length-1) // => "d": ký tự cuối cùng
    s.charCodeAt(0) // => 72: số 16-bit tại vị trí được chỉ định
    s.codePointAt(0) // => 72: ES6, hoạt động cho các điểm mã > 16 bit
    // Các hàm padding chuỗi trong ES2017
    "x".padStart(3) // => "  x": thêm khoảng trắng ở bên trái đến độ dài 3
    "x".padEnd(3) // => "x  ": thêm khoảng trắng ở bên phải đến độ dài 3
    "x".padStart(3, "*") // => "**x": thêm dấu sao ở bên trái đến độ dài 3
    "x".padEnd(3, "-") // => "x--": thêm dấu gạch ngang ở bên phải đến độ dài 3
    // Các hàm cắt bỏ khoảng trắng. trim() là ES5; các hàm khác là ES2019
    " test ".trim() // => "test": xóa khoảng trắng ở đầu và cuối
    " test ".trimStart() // => "test ": xóa khoảng trắng ở bên trái. Còn có trimLeft
    " test ".trimEnd() // => " test": xóa khoảng trắng ở bên phải. Còn có trimRight
    // Các phương thức chuỗi linh tinh
    s.concat("!") // => "Hello, world!": chỉ cần sử dụng toán tử + thay thế
    "<>".repeat(5) // => "<><><><><>": nối n bản sao. ES6
    ```
    
- Hãy nhớ rằng strings là bất biến trong Js. Các methods như replace() và toUpperCase() trả về string mới: Chúng không sửa đổi string mà chúng được gọi
- Strings cũng được coi là array chỉ đọc và bạn có thể truy cập các ký tự riêng lẻ (giá trị 16-bit) từ string bằng cách sử dụng dấu ngoặc vuông thay vì methods `charAt()`
    
    ```jsx
    let s = "hello, world";
    s[0] // => "h"
    s[s.length-1] // => "d"
    ```
    

### 3.3.4 Template Literals

- Trong ES6 trở lên, string literal có thể được phân định bởi dấu huyền
    
    ```jsx
    let s = `hello world`;
    ```
    
- Tuy nhiên, đây không chỉ là một cú pháp string literal khác, bởi vì template literals (chuỗi mẫu) này có thể bao gồm các expression Js tuỳ ý. Giá trị cuối cùng của string literal trong dấu huyền được tính toán bằng cách đánh giá bất kỳ expression nào được bao gồm, chuyển đổi values của các expressions đó thành string và kết hợp các strings được tính toán đó với các ký tự literal trong dấu huyền
    
    ```jsx
    let name = "Bill";
    let greeting = `Hello ${ name }.`; // greeting == "Hello Bill."
    ```
    
- Mọi thứ giữa `${ }` phù hợp được hiểu là expression Js. Mọi thứ bên ngoài dấu ngoặc nhọn là văn bản string literal thông thường. Expression bên trong dấu ngoặc nhọn được đánh giá và sau đó được chuyển thành string và chèn vào mẫu, thay thế dấu $, dấu ngoặc nhọn và mọi thứ ở giữa chúng
- Template literal có thể bao gồm bất kỳ số lượng expression nào. Nó có thể sử dụng bất kỳ escape character nào mà string thông thường có thể sử dụng và nó có thể kéo dài bất kỳ số dòng nào mà không cần thoát đặc biệt. Template literal bao gồm 4 expression Js, một escape sequence Unicode và ít nhất 4 dấu xuống dòng
    
    ```jsx
    let errorMessage = `\
    \u2718 Test failure at ${filename}:${linenumber}:
    ${exception.message}
    Stack trace:
    ${exception.stack}
    `;
    ```
    
- Dấu \ ở cuối dòng đầu tiên ở đây thoát khỏi dấu xuống dòng ban đầu để string kết quả bắt đầu bằng ký tự Unicode ✘ (\u2718) thay vì dấu xuống dòng.

### **TAGGED TEMPLATE LITERALS**

- Một tính năng mạnh mẽ nhưng ít được sử dụng hơn của template literals là nếu tên hàm (hoặc “thẻ”) đứng ngay trước dấu huyền mở, thì văn bản và values của các expressions trong template literal sẽ được chuyển đến hàm. Giá trị của “tagged template literal” này là giá trị trả về của hàm. Ví dụ điều này có thể được sử dụng để áp dụng thoát HTML hoặc SQL cho các giá trị trước khi thay thế chúng vào văn bản
- ES6 có một hàm thẻ tích hợp sẵn: `String.raw()`. Nó trả về văn bản trong dấu huyền mà không cần xử lý bất kỳ escape sequences dấu gạch chéo ngược nào
    
    ```jsx
    `\n`.length // => 1: chuỗi có một ký tự xuống dòng duy nhất
    String.raw`\n`.length // => 2: một ký tự dấu gạch chéo ngược và chữ cái n
    ```
    
- Lưu ý rằng mặc dù phần thẻ của tagged template literal là một hàm, nhưng không có dấu ngoặc đơn nào được sử dụng trong lời gọi của nó. Trong trường hợp rất cụ thể này, các ký tự dấu huyền thay thế dấu ngoăc đơn mở và đóng
- Khả năng định nghĩa các hàm thẻ mẫu của riêng bạn là một tính năng mạnh mẽ của JS. Các hàm này không cần trả về strings và chúng có thể được sử dụng như các hàm tạo, như thể định nghĩa cú pháp literal mới cho ngôn ngữ. Chúng ta sẽ thấy 1 ví dụ trong 14.5

### 3.3.5 Pattern Matching

- Js định nghĩa một datatype được gọi là regular expression hoặc (RegExp) để mô tả khớp với các mẫu trong strings văn bản. RegExp không phải là một trong những datatypes cơ bản trong JS nhưng chúng có cú pháp literal giống như number và string, vì vậy đôi khi chúng có vẻ như là cơ bản. Ngữ pháp của regular expression literals (giá trị ký tự biểu thức chính quy) rất phức tạp và API mà chúng định nghĩa không tầm thường. Chúng được ghi lại chi tiết trong 11.3. Tuy nhiên vì RegExp mạnh mẽ và thường được sử dụng để xử lý văn bản, phần này cung cấp 1 cái nhìn tổng quan ngắn gọn
- Văn bản giữa một cặp dấu gạch chéo tạo thành regular expression literal. Dấu gạch chéo thứ 2 trong cặp cũng có thể được theo sau bởi một hoặc nhiều chữ cái, điều này sửa đổi ý nghĩa của mẫu.
    
    ```jsx
    /^HTML/; // Khớp các chữ cái H T M L ở đầu chuỗi
    /[1-9][0-9]*/; // Khớp một chữ số khác 0, theo sau là bất kỳ số chữ số nào
    /\bjavascript\b/i; // Khớp "javascript" như một từ, không phân biệt chữ hoa chữ thường
    ```
    
- Các objects RegExp định nghĩa 1 số methods hữu ích và strings cũng có methods chấp nhận đôi số RegExp
    
    ```jsx
    let text = "testing: 1, 2, 3"; // Văn bản mẫu
    let pattern = /\d+/g; // Khớp tất cả các trường hợp của một hoặc nhiều chữ số
    pattern.test(text) // => true: tồn tại kết quả khớp
    text.search(pattern) // => 9: vị trí của kết quả khớp đầu tiên
    text.match(pattern) // => ["1", "2", "3"]: mảng của tất cả các kết quả khớp
    text.replace(pattern, "#") // => "testing: #, #, #"
    text.split(/\D+/) // => ["","1","2","3"]: tách trên các ký tự không phải chữ số
    ```
## 3.4 Boolean Values
- Một giá trị boolean đại diện cho đúng sai, bật tắt, có hoặc không. Chỉ có 2 giá trị khả dĩ cho kiểu dữ liệu này. Các từ khoá dành riêng true và false đánh giá (evaluate) thành hai giá trị này. Giá trị boolean thường là kết quả của các phép so sánh bạn thực hiện trong các chương trình Js của mình
    
    ```jsx
    a === 4
    ```
    
- Đoạn mã này kiểm tra giá trị của biến a có bằng số 4 hay không. Nếu có, kết quả của phép so sánh này là giá trị boolean true. Nếu a không bằng 4, kết quả của phép so sánh là false.
- Giá trị boolean thường được sử dụng trong các cấu trúc điều khiển Js. Ví dụ: if else trong Js thực hiện hành động nếu giá trị là true hoặc false. Bạn thường kết hợp một phép so sánh tạo ra các giá trị boolean trực tiếp với 1 câu lệnh sử dụng nó. Kết quả trông như này
    
    ```jsx
    if (a === 4) {
      b = b + 1;
    } else {
      a = a + 1;
    }
    ```
    
- Đoạn code này sẽ kiểm tra xem a có bằng 4 không. Nếu có, nó sẽ cộng 1 vào b; nếu không, nó sẽ cộng 1 vào a
- Như chúng ta sẽ thảo luận trong 3.9, bất kỳ giá trị Js nào cũng có thể được chuyển đổi thành giá trị boolean. Các giá trị sau được chuyển đổi thành và do đó hoạt động như false
    - **undefined**
    - **null**
    - 0
    - 0
    - **NaN**
    - "" // chuỗi rỗng
- Tất cả các giá trị khác, bao gồm tất cả các object(và array) được chuyển đổi và hoạt động giống như true. false và 6 giá trị được chuyển đổi thành nó, đôi khi được gọi là giá trị falsy, và tất cả các giá trị khác được gọi là truthy. Bất cứ khi nào Js mong đợi 1 giá trị boolean, một giá trị falsy hoạt động như false và một giá trị truthy hoạt động như true
- Ví dụ giả sử biến o chứa 1 object hoặc giá trị null. Bạn có thể kiểm tra rõ ràng xem o có phải là non-null hay không bằng câu lệnh if
    
    ```jsx
    if (o !== null) ... 
    ```
    
- Toán tử không bằng `!==` so sánh o với null và đánh giá thành true hoặc false. Nhưng bạn có thể bỏ qua phép so sánh và thay vào đó dựa vào thực tế là null là falsy và các object là truthy
    
    ```jsx
    if (o) ... 
    ```
    
- Trong trường hợp đầu tiên, phần thân của if sẽ chỉ được thực thi nếu o không phải là null. Trường hợp thứ 2 ít nghiêm ngặt hơn: Nó sẽ chỉ thực thi phần thân của if nếu o không phải là false hoặc bất kỳ giá trị falsy nào (chẳng hạn như null hoặc undefined). Câu lệnh if nào phù hợp với chương trình của bạn thực sự phụ thuộc vào những giá trị bạn mong đợi sẽ gán cho o. Nếu bạn cần phân biệt null với 0 và “”, thì bạn nên sử dụng phép so sánh rõ ràng
- Giá trị boolean có phương thức `toString()` mà bạn có thể sử dụng để chuyển đổi chúng thành chuỗi “true” hoặc “false”, nhưng chúng không có bất kỳ phương thức hữu ích nào khác. Mặc dù API không đáng kể, có 3 toán tử boolean quan trọng
- Toán từ `&&` thực hiện phép toán booean AND. Nó đánh giá thành một giá trị truthy nếu và chỉ nếu cả 2 toán hạng của nó đều là truthy nếu và chỉ nếu cả 2 toán hạng của nó đều là truthy; nó đánh giá thành giá trị falsy nếu không. Toán từ `||` là phéo toán Boolean OR: nó đánh giá thành một giá trị truthy nếu 1 trong 2 (hoặc cả 2) toán hạng của nó là truthy và đánh giá thành một giá trị falsy nếu cả 2 toán hạng đều là falsy. Cuối cùng, toán tử unary `!` thực hiện phép toán Boolean NOT: nó đánh giá thành true nếu toán hạng của nó là falsy và thành false nếu giá trị là truthy
    
    ```jsx
     if ((x === 0 && y === 0) || !(z === 0)) {
      // x và y đều bằng không hoặc z khác không 
    }
    ```
    
- Chi tiết đầy đủ về các toán tử này có trong 4.10

## 3.5 null and undefined
- `null` là một từ khoá đặc biệt của ngôn ngữ, đánh giá một giá trị đặt biệt thường được sử dụng để hiển thị sự vắng mặt của một giá trị. Sử dụng toán tử `typeof` trên null trả về chuỗi “object”, cho biết rằng null có thể được coi như một giá trị object đặc biệt biểu thị “không có đối tượng”. Tuy nhiên trong thực tế, null thường được coi là thành viên duy nhất của kiểu dữ liệu riêng của nó và nó có thể được sử dụng để biểu thị “không có giá trị” cho số và chuỗi cũng như các object. Hầu hết các ngôn ngữ lập trình đều có một giá trị tương đương với null của Js: bạn có thể đã quen thuộc nó dưới dạng NULL, nil hoặc None
- Js cũng có một giá trị thứ 2 để biểu thị sự vắng mặt của value. Giá trị undefined đại diện cho một kiểu vắng mặt sâu hơn. Nó là giá trị của các biến chưa được khởi tạo và giá trị bạn nhận được khi bạn truy vấn giá trị của một thuộc tính object hoặc phần tử array không tồn tại. Giá trị undefined cũng là giá trị trả về của các function không trả về giá trị một cách rõ ràng và giá trị của các tham số function mà không có đối số nào được truyền vào. `undefined` là một hằng số toàn cục được xác định trước (không phải là từ khoá ngôn ngữ như null, mặc dù đây không phải là sự khác biệt quan trọng trong thực tế) được khởi tạo thành giá trị undefined. Nếu bạn áp dụng toán tử typeof cho giá trị undefined, nó sẽ trả về “undefined”, cho biết rằng giá trị này là thành viên duy nhất của một kiểu đặc biệt
- Mặc dù có những khác biệt này, cả null và undefined đều biểu thị sự vắng mặt của giá trị và thường có thể được sử dụng thay thế cho nhau. Toán tử == coi chúng như là bằng nhau. (Sử dụng toán từ === để phân biệt chúng). Cả 2 đều là giá trị falsy: chúng hoạt động giống như false khi yêu cầu giá trị boolean. Cả null và undefined đều không có bất kỳ thuộc tính hoặc phương thức nào. Trên thực tế, sử dụng `.` hoặc `[]` để truy cập thuộc tính hoặc phương thức của các giá trị này sẽ gây ra TypeError
- Tôi coi `undefined` là đại diện cho sự vắng mặt giá trị ở cấp hệ thống, không mong muốn hoặc giống như lỗi và null đại diện cho sự vắng mặt giá trị ở cấp chương trình, bình thường hoặc mong đợi. Tôi tránh sử dụng null và undefined khi có thể, nhưng nếu tôi cần gán một trong những giá trị này cho một biến hoặc 1 thuộc tính hoặc truyền hoặc trả về một trong những giá trị này đến hoặc từ một function, tôi thường sử dụng null. Một số lập trình viên cố gắng tránh null hoàn toàn và sử dụng undefined thay thế bất cứ khi nào họ có thể