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
## Properties (Thuộc tính)
- Việc hiển thị UI được mã hoá cứng trong custom component là hoàn toàn ổn và có công dụng của nó. Nhưng các component cũng có thể nhận được thuộc tính và hiển thị hoặc hoạt động khác nhau tuỳ thuộc vào giá trị của thuộc tính. Hãy nghĩ về phần tử <a> trong HTML và cách nó hoạt động khác nhau dựa trên giá trị của thuộc tính href. Ý tưởng về thuộc tính trong React cũng tương tự (Và cú pháp JSX cũng vậy)
- Trong các class component, tất cả các thuộc tính đều có sẵn thông qua đối tượng this.props . Hãy xem ví dụ dưới đây
```js
class MyComponent extends React.Component {
  render() {
    return <span>My name is <em>{this.props.name}</em></span>;
  }
}
```
  - Trong ví dụ này, bạn có thể sử dụng {} để thêm các giá trị và biểu thức trong JSX của bạn. 
- Việc truyền 1 giá trị cho thuộc tính name khi hiển thị component sẽ như thế này
```js
ReactDOM.render(
  <MyComponent name="Bob" />,
  document.getElementById('app')
);
```
- Điều quan trọng cần nhớ là this.props là chỉ đọc. Nó được dùng để truyền cấu hình từ component cha xuống component con, nhưng nó không phải là bộ nhớ chung cho các giá trị. Nếu bạn cảm thấy muốn đặt thuộc tính của this.props, hãy sử dụng các biến cục bộ hoặc thuộc tính của class component của bạn thay vào (có nghĩa là sử dụng this.thing thay vì this.props.thing)
## Properties in Function Components
- Trong các function component, không có this (chế độ nghiêm ngặt của Js) hoặc this  đề cập đến đối tượng toàn cục (trong chế độ không nghiêm ngặt, chúng ta có thể nói đó là chế độ cẩu thả). Vì vậy thay vì this.props, bạn nhận được 1 đối tượng props được truyền vào hàm của bạn dưới dạng đối số đầu tiên
```js
const MyComponent = function(props) {
  return <span>My name is <em>{props.name}</em></span>;
};
```
- Một mẫu phổ biến là sử dụng phép gán destructuring của JS và gán các giá trị thuộc tính cho các biến cục bộ. Nói cách khác, ví dụ trên sẽ trở thành như thế này
```js
const MyComponent = function({name}) {
  return <span>My name is <em>{name}</em></span>;
};
```
- Bạn có thể có bao nhiêu thuộc tính tuỳ thích. Ví dụ nếu bạn cần 2 thuộc tính (name và job) 
```js
const MyComponent = function({name, job}) {
  return <span>My name is <em>{name}</em>, the {job}</span>;
};

ReactDOM.render(
  <MyComponent name="Bob" job="engineer"/>,
  document.getElementById('app')
);
```
## Default properties
- Component của bạn có thể cung cấp 1 số thuộc tính, nhưng đôi khi một số thuộc tính có thể có 1 số giá trị mặc định phù hợp với các trường hợp phổ biến nhất. Bạn có thể chỉ định các giá trị thuộc tính mặc định bằng cách sử dụng thuộc tính defaultProps cho cả class và function
- Đối với funtion component
```js
const MyComponent = function({name, job}) {
  return <span>My name is <em>{name}</em>, the {job}</span>;
};

MyComponent.defaultProps = {
  job: 'engineer',
};

ReactDOM.render(
  <MyComponent name="Bob" />,
  document.getElementById('app')
);
```
- Đối với class component
```js
class MyComponent extends React.Component {
  render() {
    return (
      <span>My name is <em>{this.props.name}</em>,
        the {this.props.job}</span>
    );
  }
}

MyComponent.defaultProps = {
  job: 'engineer',
};

ReactDOM.render(
  <MyComponent name="Bob" />,
  document.getElementById('app')
);
```
- Trong cả 2 trường hợp, kết quả sẽ là
```
My name is Bob, the engineer
```
- Lưu ý:
    - Các câu lệnh return của phương thức **render()** bao bọc giá trị được trả về trong dấu ngoặc đơn. Điều này chỉ vì cơ chế chèn dấu chấm phẩy tự động (ASI) của Js. Một câu lệnh `return` theo sau 1 dòng mới giống như `return ;` mà cũng giống như **return undefined;** điều này chắc chắn không phải là điều bạn muốn. Việc bao bọc biểu thức được trả về trong dấu ngoặc đơn cho phép định dạng code tốt hơn trong khi vẫn giữ được tính chính xác
## State
- Các ví dụ cho đến nay khá tĩnh (hoặc không trạng thái). Mục tiêu chỉ là cung cấp cho bạn một ý tưởng về các block để xây dựng giao diện người dùng của bạn. Nhưng nơi React thực sự toả sáng (và nơi việc thao tác và bảo trì DOM của trình duyệt theo cách cũ trở nên phức tạp) là khi dữ liệu trong ứng dụng của bạn thực sự thay đổi
- React có khái niệm về state, đó là bất kỳ dữ liệu nào mà các component muốn sử dụng để hiển thị chính mình. Khi state thay đổi, React sẽ xây dựng lại UI người dùng trong DOM mà bạn không cần phải làm gì. Sau khi bạn xây dựng giao diện người dùng ban đầu trong phương thức `render()` của mình (hoặc trong hàm hiển thị trong trường hợp function component), tất cả những gì bạn quan tâm là cập nhật dữ liệu. Bạn không cần phải lo lắng về việc thay đổi giao diện người dùng chút nào. Sau cùng phương thức/hàm `render()` của bạn đã cung cấp bản thiết kế về các component trông thế nào
    - **“Stateless (không trạng thái)” không phải là 1 từ xấu, không hề. Các component stateless dễ quản lý và suy nghĩ hơn nhiều. Tuy nhiên trong khi việc sử dụng stateless bất cứ khi nào có thể là tốt hơn, các ứng dụng phức tạp cần state**
- Tương tự như cách bạn truy cập thuộc tính thông qua **this.props**, bạn đọc **state** thông qua đối tượng **this.state**. Để cập nhật state, bạn sử dụng **this.setState()**. Khi **this.setState** được gọi, React sẽ gọi phương thức **render()** của component của bạn (và các component con của nó) và cập nhật UI người dùng
- Các cập nhật đối với UI người dùng sau khi gọi **this.setState()** được thực hiện bằng cách sử dụng cơ chế xếp hàng hiệu quả để xử lý các thay đổi theo lô. Việc cập nhật `this.state` trực tiếp có thể dẫn đến lỗi không mong muốn và bạn không nên làm điều đó. Tương tự như this.props, hãy xem đối tượng this.state chỉ là đọc, không chỉ về mặt ngữ nghĩa nó là 1 ý tưởng không hay mà còn vì có thể hoạt động theo những cách mà bạn không mong đợi. Tương tự, đừng bao giờ tự gọi `this.render()` - thay vào đó, hãy để React xử lý các thay đổi theo lô, tìm ra lượng công việc tối thiểu và gọi `render()` khi và nếu cần thiết.
## A textarea Component
- Hãy cùng tạo 1 component mới - Một textarea đếm số lượng kí tự được nhập vào
- Bạn (cũng như những người sử dụng component có thể tái sử dụng trong tương lai) có thể sử dụng component mới như sau
  ```js
  ReactDOM.render(
    <TextAreaCounter text="Bob" />,
    document.getElementById('app')
  );
  ```
- Bây giờ hãy triển khai component. Đầu tiên hãy tạo 1 phiên bản stateless (không trạng thái) không xử lý các cập nhật; điều này không khác biệt nhiều so với các ví dụ trước
  ```js
  class TextAreaCounter extends React.Component {
    render() {
      const text = this.props.text;
      return (
        <div>
          <textarea defaultValue={text}/>
          <h3>{text.length}</h3>
        </div>
      );
    }
  }

  TextAreaCounter.defaultProps = {
    text: 'Count me as I type',
  };
  ```
  - Bạn có thể nhận thấy rằng `<textarea>` trong đoạn code trên sử dụng thuộc tính defaultValue trái ngược với `text` bạn thường thấy trong HTML thông thường. Điều này là do có 1 số khác biệt nhỏ giữa React và HTML khi nói đến form element. Chúng ta sẽ được thảo luận kỹ hơn trong cuốn sách - hãy yên tâm, không có quá nhiều sự khác biệt
- Như bạn đã thấy, component `TextAreaCounter` nhận 1 thuộc tính chuỗi văn bản text và hiển thị 1 `textarea` với giá trị được cho, cũng như phần tử <h3> sẽ hiển thị đỗ dài của chuỗi. Nếu `text` không được cung cấp, giá trị mặc định **Count me as I type** sẽ được sử dụng
## Make It  Stateful 
- Bước tiếp theo là biến component không trạng thái thành có trạng thái. Hay nói cách khác, hãy để component duy trì 1 số dữ liệu (trạng thái) và sử dụng dữ liệu này để hiển thị chính nó và sau đó cập nhật chính nó (render lại) khi dữ liệu thay đổi
- Đầu tiên, bạn cần đặt state ban đầu trong hàm tạo lớp bằng `this.state` . Hãy nhớ rằng hàm tạo (constructor) là nơi duy nhất bạn có thể đặt state trực tiếp mà không cần phải gọi **this.setState()**
- Khởi tạo **this.setState** là bắt buộc; nếu bạn không làm điều đó, việc truy cập liên tục vào **this.state** trong phương thức **render()** sẽ thất bại
- Trong trường hợp này, việc khởi tạo **this.state.text** là không cần thiết vì bạn có thể sử dụng thuộc tính **this.props.text**
  ```js
  class TextAreaCounter extends React.Component {
    constructor() {
      super();
      this.state = {};
    }

    render() {
      const text = 'text' in this.state ? this.state.text : this.props.text;
      return (
        <div>
          <textarea defaultValue={text} />
          <h3>{text.length}</h3>
        </div>
      );
    }
  }
  ```
  - Gọi super() trong constructor là bắt buộc trước khi bạn có thể sử dụng this
- Dữ liệu mà component này duy trì là nội dung của textarea vì vậy state chỉ có 1 thuộc tính gọi là text - có thể truy cập thông qua this.state.text . Tiếp theo, bạn cần cập nhật state. Bạn có thể sử dụng 1 phương thức trợ giúp cho mục đích này
  ```js
  onTextChange(event) {
    this.setState({
      text: event.target.value,
    });
  }
  ```
- - Bạn luôn cập nhật state bằng `this.setState()` , hàm này nhận 1 object và hợp nhất nó với dữ liệu đã tồn tại trong **this.state.** Như bạn có thể đoán, **onTextChange()** là 1 trình xử lý sự kiện nhận vào 1 event object và truy cập vào nó để lấy nội dung của đầu vào textarea
- Điều cuối cùng cần làm là cập nhật phương thức **render()** để thiết lập event handler
  ```js
  render() {
    const text = 'text' in this.state ? this.state.text : this.props.text;
    return (
      <div>
        <textarea
          value={text}
          onChange={event => this.onTextChange(event)}
        />
        <h3>{text.length}</h3>
      </div>
    );
  }
  ```
- Bây giờ, bất cứ khi nào người dùng gõ vào textarea, giá trị của bộ đếm sẽ được cập nhật để phản ánh nội dung
- Lưu ý rằng trước đây bạn có `<textarea defaultValue...>` , giờ đây là `<textarea value...>` trong đoạn code trên. Điều này là do cách thức hoạt động của các đầu vào trong HTML, nơi state của chúng ta được duy trì bởi trình duyệt. Nhưng React có thể làm tốt hơn. Trong ví dụ này, việc triển khai **onChange** có nghĩa là textarea hiện được kiểm soát bởi React. Bạn sẽ được tìm hiểu thêm về các component được kiểm soát (controlled components) trong các chương sau của cuốn sách