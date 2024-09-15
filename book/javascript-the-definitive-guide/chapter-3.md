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
