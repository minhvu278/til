# The Life of a Component
- Bây giờ bạn đã biết cách sử dụng các component DOM có sẵn, đã đến lúc bạn học cách tạo ra component cho riêng mình
- Có 2 cách để định nghĩa 1 component tuỳ chỉnh, cả 2 đều đạt được 1 kết quả nhưng sử dụng cú pháp khác nhau
    - **Sử dụng function**: Các component được tạo ra bằng cách này được gọi là function component
    - **Sử dụng class**: Sử dụng 1 kết thừa từ **React.Component** được gọi là class component
## A Custom Function Component
- Đây là 1 ví dụ về function component
```js
const MyComponent = function() {
  return 'I am so custom';
};
```
- Nhưng chờ đã, đây chỉ là một function! Đúng vậy, đây là custom component chỉ là 1 hàm trả về giao diện người dùng mà bạn muốn. Trong trường hợp này, giao diện người dùng chỉ là text, nhưng bạn thường cần nhiều hơn thế, có thể là một sự kết hợp của các component khác. Đây là ví dụ sử dụng span để bọc text
```js
const MyComponent = function() {
  return React.createElement('span', null, 'I am so custom');
};
```
- Sử dụng component mới của bạn trong App tương tự với cách sử dụng các component DOM từ chương 1, ngoại trừ việc bạn định nghĩa gọi function component
```js
ReactDOM.render(
  MyComponent(),
  document.getElementById('app')
);
```
## A JSX Version
- Cùng ví dụ đó nhưng sử dụng JSX sẽ dễ đọc hơn 1 chút. Định nghĩa component sẽ như thế này
```js
const MyComponent = function() {
  return <span>I am so custom</span>;
};
```
- Sử dụng component theo cách JSX sẽ như thế này, bất kể component đó được định nghĩa như thế nào
```js
ReactDOM.render(
  <MyComponent />,
  document.getElementById('app')
);
```
## A Custom Class Component
- Cách thứ 2 để tạo 1 component là định nghĩa 1 class kế thừa từ React.Component và triển khai 1 hàm render()
```js
class MyComponent extends React.Component {
  render() {
    return React.createElement('span', null, 'I am so custom');
    // or with JSX:
    // return <span>I am so custom</span>;
  }
}
```
- Hiển thị component trên trang
```js
ReactDOM.render(
  React.createElement(MyComponent),
  document.getElementById('app')
);
```
- Nếu bạn sử dụng JSX, bạn không cần biết component được định nghĩa như nào (bằng cách sử dụng class hay function). Trong cả 2 trường hợp, việc sử dụng component là như nhau
```js
ReactDOM.render(
  <MyComponent />,
  document.getElementById('app')
);
```
## Which Syntax to Use?
- Bạn có thể băn khoăn: Với tất cả những lựa chọn này (JSX so với Js thuần, class component so với function component), nên sử dụng cái nào? JSX là phổ biến nhất. Và trừ khi bạn không thích cú pháp XML trong JS của mình, con đường gõ phím ít hơn là sử dụng JSX. Cuốn sách này sử dụng JSX từ bây giờ - trừ khi để minh hoạ 1 khái niệm nào đó
- Vậy tạo sao lại đề cập đến cách không sử dụng JSX? Bạn nên biết rằng có 1 cách khác và JSX không phải là magic mà là 1 lớp cú pháp mỏng chuyển đổi XML thành các cuộc gọi hàm Js đơn giản như React.createElement trước khi gửi code đến trình duyệt
- Còn về class component so với function component? Đây là vấn đề sở thích. Nếu bạn quen thuộc với lập trình hướng đối tượng (OOP) và bạn thích cách bố trí các class thì hãy sử dụng nó.
    - Các function component nhẹ hơn 1 chút trên CPU máy tính của bạn và liên quan đến việc gõ phím ít hơn 1 chút. Chúng cũng tạo cảm giác tự nhiên hơn đối với JS
    - Thực tế, các class không tồn tại trong các phiên bản đầu tiên của của ngôn ngữ Js; chúng chỉ là 1 suy nghĩ muộn và chỉ là đường cú pháp trên đỉnh của các hàm nguyên mẫu
- Theo lịch sử về React, các funtion component không thể thực hiện mọi thứ mà các class có thể làm. Cho đến khi phát minh ra hook, điều mà bạn sẽ được học trong thời gian tới. Về tương lai, người ta chỉ có thể suy đoán nhưng khả năng React sẽ chuyển sang function component nhiều hơn
    - Cuốn sách này dạy bạn cả 2 cách và không đưa ra quyết định thay bạn. Quyết định chọn cách nào là ở bạn
