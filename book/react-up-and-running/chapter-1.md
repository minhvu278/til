# Hello world
- Hãy bắt đầu quá trình chinh phục ứng dụng phát triển web bằn React. Trong chương này, chúng ta sẽ học cách thiết lập ứng dụng React và viết ứng dụng web Hello World ban đầu của mình 
## Setup
- Trước tiên chúng ta cần có bản sao của thư viện React. Có rất nhiều cách để thực hiện điều này, nhưng chúng ta sẽ sử dụng cách đơn giản nhất, không yêu cầu bất kỳ công cụ đặc biệt nào giúp chúng ta có thể bắt đầu ngay lập tức
  - Tạo thư mục
    ```
    $ mkdir ~/reactbook
    ```
  - Tạo thư mục React
    ```
    $ mkdir ~/reactbook/react
    ```
  - Download React và React DOM
    ```
    $ curl -L https://unpkg.com/react@17/umd/react.development.js > ~/reactbook/react/react.js
    $ curl -L https://unpkg.com/react-dom@17/umd/react-dom.development.js > ~/reactbook/react/react-dom.js
    ```
  - **Sử dụng trực tiếp [unpkg.com](http://unpkg.com)(không cần tải xuống)**: Chúng ta không cần tải xuống thư viện và có thể sử dụng trực tiếp từ unpkg. Tuy nhiên thì vẫn nên dùng ở local để có thể tiện sử dụng ở bất kì đâu nếu không có mạng
- Phiên bản React: Quyển sách này sử dụng phiên bản @17
## Hello world
- Hãy bắt đầu với 1 trang đơn giản
  ```html
  <!DOCTYPE html>
    <html>
    <head>
    <title>Hello React</title>
    <meta charset="utf-8">
    </head>
    <body>
    <div id="app">
    <!-- my app renders here -->
    </div>
    <script src="react/react.js"></script>
    <script src="react/react-dom.js"></script>
    <script>
    // my app's code
    </script>
    </body>
    </html>
  ```
- Có 2 điều cần chú ý trong file này:
  - **Kết nối thư viện React**: Bao gồm thư viện React và add-on Document Object Model (DOM) của nó qua(qua thẻ script src)
  - **Xác định vị trí hiển thị ứng dụng**: Bạn xác định vị trí ứng dụng sẽ được đặt lên trang (<div id=”app”>)
  - Bạn luôn có thể kết hợp nội dung HTML thông thường cũng như các thư viện JS khác với ứng dụng React. Bạn cũng có thể có nhiều ứng dụng React trên 1 trang. Tất cả những gì bạn cần là 1 vị trí trong DOM mà bạn có thể chỉ định cho React và nói **“Thực hiện phép thuật của bạn ở đây”**
- Bây giờ hãy thêm code “Hello world vào thay thế cho // my app’s code
  ```javascript
    ReactDOM.render(
      React.createElement('h1', null, 'Hello world!'),
      document.getElementById('app')
    );
  ```
- Chúc mừng, bạn đã tạo thành công dự án đầu tiên của mình. Hãy copy và chạy thử nó
## What Just Happend
- Có 1 vài điểm đáng chú ý trong code đã giúp ứng dụng của bạn hoạt động
  - Đối tượng React: Bạn sử dụng đối tượng React. Tất cả các API có sẵn cho bạn đều có thể truy cập thông qua đối tượng này. API được thiết kế đơn giản nên bạn không cần nhớ quá nhiều tên phương thức
  - Đối tượng React DOM: Bạn cũng có thể thấy đối tượng ReactDOM. Nó chỉ có 1 số ít phương thức, trong đó phương thức render() là phương thức hữu ích nhất. ReactDOM chịu trách nhiệm hiển thị ứng dụng trong trình duyệt. Thực tế là bạn có thể tạo ứng dụng React và hiển thị chúng trong các môi trường khác nhau ngoài trình duyệt - ví dụ như canvas hoặc Android, IOS
  - **Khái niệm components:** Bạn xây dựng giao diện người dùng bằng cách sử dụng các component và kết hợp chúng theo bất kỳ cách nào bạn muốn.
    - Bạn sẽ tạo các các component tuỳ chỉnh của riêng bạn, nhưng để giúp bạn bắt đầu React cung cấp các lớp bao bọc xung quanh các phần tử HTML DOM. Bạn sử dụng các lớp bao bọc thông qua **React.createElement**.
    - Trong ví dụ đầu tiên này ta có thể thấy việc sử dụng phần tử h1 - nó tương đương với <h1> trong html và có sẵn cho bạn bằng cách gọi **React.createElement(’h1’)**
  - **Tự động hoá DOM:** Một khi bạn chuyển từ DOM sang React, bạn không còn phải lo lắng về việc thao tác DOM nữa, vì React sẽ thực hiện chuyển đổi từ các component sang nền tảng cơ bản(DOM của trình duyệt, canvas,…)
    - Thực tế việc không phải lo lắng về DOM là 1 trong những điểm tuyệt vời của React. Bạn chỉ cần tập chung vào việc tạo ra các compoenent và data của chúng - phần quan trọng nhất của ứng dụng - và để React xử lý việc cập nhật DOM 1 cách hiệu quả nhất. Không còn phải tìm kiếm các nút DOM, firstChild, appendChild() và các phương thức khác nữa
  - **Thao tác DOM(nếu cần):** Bạn không cần phải lo lắng về DOM, nhưng điều đó không có nghĩa là bạn không thể thao tác nó. React cung cấp cho bạn các **escape hatches (lối thoát)** nếu bạn muốn quay lại DOM-land vì bất kỳ lý do nào mà bạn cần
### Hình dung tổng quan
- Bạn đã hiển thị 1 component React trong 1 vị trí DOM mà bạn chọn. Bạn luôn hiển thị component ở cấp cao nhất và nó có thể có bao nhiêu component con cháu,… tuỳ thuộc vào nhu cầu. Ngay cả trong ví dụ đơn giản này, component h1 cũng có 1 component con - Text Hello world
## React.createElement()
- Bạn có thể sử dụng 1 số phần tử HTML dưới dạng React component thông qua phương thức React.createElement(). Hãy cùng xem xét kỹ API này
  ```js
  ReactDOM.render(
    React.createElement('h1', null, 'Hello world!'),
    document.getElementById('app')
  );
  ```
  - Tham số đầu tiên của createElement là loại phần tử cần tạo 
  - Tham số thứ hai (bằng null trong trường hợp này) là một đối tượng xác định bất kỳ thuộc tính nào(nghĩ về các thuộc tính DOM) mà bạn có thể truyền cho phần tử của mình. Ví dụ:
    ```js
    React.createElement(
      'h1',
      {
        id: 'my-heading',
      },
      'Hello world!'
    ),
    ```
  - Tham số thứ 3 xác định 1 component con trong component cha. Trường hợp đơn giản nhất chỉ là 1 component con dạng văn bản(nút văn bản trong DOM) như bạn thấy trong code trước. Nhưng bạn có thể có bao nhiêu component con lồng nhau tuỳ thích và bạn truyền chúng dưới dạng các tham số bổ sung
    ```js
    React.createElement(
      'h1',
      {id: 'my-heading'},
      React.createElement(
        'span',
        null,
        'Hello ',
        React.createElement('em', null, 'Wonderful'),
      ),
      ' world!'
    ),
    ```
  - DOM được tạo bởi React có phần tử <em> là component con của span - mà lần lượt là component con của h1(và là component cùng cấp với text “world!”)
  - Như vậy, React.createElement cho phép bạn tạo các component React, cấu trúc các component con và thêm thuộc tính vào chúng
## JSX
- Khi bắt đầu lồng các component, bạn sẽ nhanh chóng gặp phải vấn đề là gọi nhiều cuộc gọi hàm và dấu ngoặc đơn để theo dõi. Để làm mọi thứ dễ dàng hơn, bạn có thể sử dụng cú pháp JSX
- JSX là 1 cú pháp gây tranh cãi: Nhiều người thường thấy phản cảm khi nhìn thấy nó lần đầu(XML trong JS) nhưng sau đó lại cảm thấy nó rất cần thiết
- Không rõ JSX viết tắt của gì nhưng có thể là JavascriptXML hoặc Javascript Synstax eXtenstion. Đây là trang web chính thức của jsx: https://facebook.github.io/jsx/
- Dưới đây là đoạn code trước đó nhưng sử dụng JSX
  ```js
  ReactDOM.render(
    <h1 id="my-heading">
      <span>Hello <em>Wonderful</em></span> world!
    </h1>,
    document.getElementById('app')
  );
  ```
  - Cú pháp này dễ đọc hơn nhiều. Nó giống như html - và bạn đã biết HTML. Tuy nhiên nó không phải là Js hợp lệ mà trình duyệt có thể hiểu. Bạn cần chuyển đổi(transpile) code này để nó hoạt động trong trình duyệt. Bạn cần Babel, thư viện này dịch Js mới (và JSX) sang JS cũ hoạt động trong các phiên bản trình duyệt cũ
## Setup Babel
- Giống như với React, chúng ta sẽ tải xuống. bản sao local của Babel
  ```
  $ curl -L https://unpkg.com/babel-standalone/babel.min.js > ~/reactbook/react/babel.js
  ```
- Sau đó cần cập nhật code để bao gồm Babel
  ```html
  <!DOCTYPE html>
  <html>
  <head>
  <title>Hello React+JSX</title>
  <meta charset="utf-8">
  </head>
  <body>
  <div id="app">
  <!-- my app renders here -->
  </div>
  <script src="react/react.js"></script>
  <script src="react/react-dom.js"></script>
  <script src="react/babel.js"></script>
  <script type="text/babel">
  // my app's code
  </script>
  </body>
  </html>
  ```
## On Transpilation
- Thật tuyệt khi bạn đã khiến JSX và Babel hoạt động, nhưng có 1 vài lời giải thích không thừa, đặc biệt nếu bạn là người mới với babel và quá trình transpilation
### JSX là gì
- JSX là 1 công nghệ riêng biệt đối với React và hoàn toàn tuỳ chọn. Như các bạn đã thấy các ví dụ trong chương này thậm chí không sử dụng JSX. Bạn có thể chọn lựa không bao giờ sử dụng JSX. Nhưng rất có thể một khi bạn thử nó, bạn sẽ không muốn quay lại cách gọi hàm nữa
### Transpilation là gì
- Quá trình transpilation là một quá trình lấy code và viết lại nó để đạt được cùng 1 kết quả nhưng cú pháp được các trình duyệt cũ hơn hiểu. Nó khác với sử dụng polyfill. Một ví dụ về polyfill là thêm 1 phương thức vào Array.prototype như map(), được giới thiệu trong ES5 và khiến nó hoạt động trong các trình duyệt chỉ hỗ trợ ES3. Nó là 1 giải pháp tốt khi thêm các phương thức mới vào đối tượng hiện có hoặc triển khai đối tượng mới (chẳng hạn như JSON). Nhưng nó không đủ khi cú pháp mới được giới thiệu vào ngôn ngữ
- Bất kỳ cú pháp nào mới trong mắt của 1 trình duyệt không hỗ trợ đều là không hợp lệ và đưa ra lỗi phân tích cú pháp. Không có cách nào để polyfill nó. Do đó, cú pháp mới yêu cầu trình biên dịch (transpilation) để nó được chuyển đổi trước khi được phục vụ cho trình duyệt
### Transpilation Javascript
- Việc transpilation js ngày càng phổ biến khi các lập trình viên muốn sử dụng các các tính năng của Js mới(ECMAScript) mà không cần chờ đợi các trình duyệt triển khai chúng. Nếu bạn thiết lập quy trình xây dựng, bạn có thể đơn giản thêm các bước JSX vào đó
- Giả sử bạn không có quy trình xây dựng, bạn sẽ thấy các bước cần thiết để thiết lập nó trong phần sau của cuốn sách
### Transpilation JSX
- Hiện tại, hãy để transpilation JSX ở phía client(trong trình duyệt) và tiếp tục học React. Hãy nhớ rằng, đây chỉ dành cho mục đính giáo dục và thử nghiệm. Các chuyển đổi phía client không được sử dụng trực tiếp trên PRD vì chúng chậm hơn và sử dụng nhiều tài nguyên hơn so với việc phục vụ code đã được transpiled
