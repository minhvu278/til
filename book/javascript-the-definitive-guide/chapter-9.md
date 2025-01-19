# Classes
- Các object js đã được đề cập trong chương 6. Chương đó coi mỗi object như 1 tập hợp các property duy nhất, khác với mọi object khác. Tuy nhiên, thường hữu ích khi định nghĩa 1 class các object chia sẻ các property nhất định. Các thành viên, hoặc các thể hiện của class có các property riêng để lưu giữ hoặc định nghĩa các status của chúng, nhưng chúng cũng có các method định nghĩa hành vi của chúng. Các method này được định nghĩa bởi class và được chia sẻ bởi tất cả các thể hiện. Ví dụ 1 class `Complex` biểu diễn và thực hiện các phép tính số học trên các số phức. Một thể hiện `Complex` sẽ có các property để lưu trữ phần thực và ảo(trạng thái) của số phức. Và class Complex sẽ định nghĩa lại các method để thực hiện phép cộng và phép nhân (hành vi) của các số đó
- Trong Js, các class sử dụng kế thừa dựa trên nguyên mẫu: nếu 2 object kế thừa các property (thường là các property có giá trị function hoặc method) từ cùng 1 nguyên mẫu, thì chúng ta có thể nói rằng các object đó là các thể hiện của cùng 1 class. Tóm lại đó là cách các class Js hoạt động
- Nếu 2 object kế thừa cùng 1 nguyên mẫu, điều này (nhưng k cần thiết) thường có nghĩa là chúng được tạo và khởi tạo bởi cùng 1 hàm tạo hoặc hàm factory. Các hàm tạo đã đc đề cập trong 4.6, 6.2.2, 8.2.3 và chương này có thêm nội dung trong 9.2. Js luôn cho phép định nghĩa các class. ES6 đã giới thiệu 1 cú pháp hoàn toàn mới (bao gồm cả từ khoá `class`) giúp việc tạo class dễ dàng hơn nữa. Các class Js mới này hoạt động tương tự như class cũ nhưng chúng ta sẽ đi phần cũ trước để hiểu nó hoạt động đằng sau như thế nào rồi mới đến cái mới
- Class trong Js và cơ chế kế thừa dựa trên nguyên mẫu về cơ bản khác với các class và cơ chế kế thừa dựa trên class của Java và các ngôn ngữ tương tự

# 9.1 Classes and Prototypes
- Trong Js, 1 class là 1 tập hợp các object kế thừa các property từ cùng 1 object nguyên mẫu. Do đó, object nguyên mẫu là đặc điểm trung tâm của 1 class. Chương 6 đã cập nhật hàm `Object.create()` trả về object mới được tạo kế thừa từ 1 object nguyên mẫu được chỉ định. Nếu chúng ta định nghĩa 1 object nguyên mẫu và sau đó sử dụng `Object.create()` để tạo các object kế thừa từ nó, thì chúng ta đã định nghĩa 1 class js. Thông thường các thể hiện của 1 class yêu cầu khởi tạo thêm và thường định nghĩa 1 hàm tạo và khởi tạo object mới. Ví dụ bên dưới: định nghĩa 1 object nguyên mẫu cho 1 class biểu thị 1 phạm vi giá trị và cũng định nghĩa 1 hàm factory tạo và khởi tạo 1 thể hiện mới của class
```js
// Đây là một hàm factory trả về một đối tượng phạm vi mới.
function range(from, to) {
  // Sử dụng Object.create() để tạo một đối tượng kế thừa từ đối tượng nguyên mẫu được định nghĩa bên dưới.
  // Đối tượng nguyên mẫu được lưu trữ dưới dạng thuộc tính của hàm này và định nghĩa các phương thức được chia sẻ (hành vi) cho tất cả các đối tượng phạm vi.
  let r = Object.create(range.methods);
  // Lưu trữ các điểm bắt đầu và kết thúc (trạng thái) của đối tượng phạm vi mới này.
  // Đây là các thuộc tính không được kế thừa duy nhất cho đối tượng này.
  r.from = from;
  r.to = to;
  // Cuối cùng trả về đối tượng mới
  return r;
}

// Đối tượng nguyên mẫu này định nghĩa các phương thức được kế thừa bởi tất cả các đối tượng phạm vi.
range.methods = {
  // Trả về true nếu x nằm trong phạm vi, ngược lại là false
  // Phương thức này hoạt động cho phạm vi văn bản và Ngày cũng như số.
  includes(x) { return this.from <= x && x <= this.to; },
  // Một hàm tạo làm cho các thể hiện của lớp có thể lặp lại.
  // Lưu ý rằng nó chỉ hoạt động cho phạm vi số.
  *[Symbol.iterator]() {
    for(let x = Math.ceil(this.from); x <= this.to; x++) yield x;
  },
  // Trả về biểu diễn chuỗi của phạm vi
  toString() { return "(" + this.from + "..." + this.to + ")"; }
};

// Dưới đây là các ví dụ sử dụng đối tượng phạm vi.
let r = range(1,3); // Tạo một đối tượng phạm vi
r.includes(2) // => true: 2 nằm trong phạm vi
r.toString() // => "(1...3)"
[...r] // => [1, 2, 3]; chuyển đổi thành một mảng thông qua trình lặp
```
- Có vài điều cần lưu ý:
  - Định nghĩa 1 function `range()` để tạo các object `Range` mới
  - Nó sử dụng property `methods` của function `range()` này như 1 nơi thuận tiện để lưu trữ object nguyên mẫu định nghĩa class
  - Function `range()` định nghĩa các property `from` và `to` trên mỗi object `Range`. Đây là các property không được share, kế thừa, xác định trạng thái duy nhất của từ object Range riêng lẻ
  - Object `range.methods` sử dụng cú pháp viết tắt của es6 định nghĩa các method - đó là lý do k thấy từ khoá function
  - Các method được share, được kế thừa được định nghĩa trong `range.methods` đều sử dụng các property `from` và `to` đã được khởi tạo trong funtion factory `range()`. Để tham chiếu chúng, sử dụng từ khoá `this` để tham chiếu đến các object mà chúng được gọi thông qua đó. Việc sử dụng `this` là 1 đặc điểm cơ bản của các method của bất kỳ class nào