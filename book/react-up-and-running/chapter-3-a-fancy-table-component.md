# Excel: A Fancy Table Component
- Bạn đã biết cách custom 1 component React, kết hợp UI bằng cách sử dụng component DOM chung và custom component của riêng bạn, đặt props, duy trì state, lifecycle của 1 component và tối ưu hoá hiệu suất bằng cách không render lại khi cần thiết
- Bây giờ, hãy kết hợp các điều này (và học thêm về React trong quá trình đó) bằng cách tạo 1 component mạnh mẽ hơn - a data table (bảng dữ liệu). Hãy nghĩ nó như một nguyên mẫu sơ khai của Microsoft Excel, cho phép bạn chỉnh sửa nội dung trên data table, sắp xếp, tìm kiếm, xuất dữ liệu dưới dạng file có thể download
# Data first
- Bảng là về dữ liệu, vì vậy table component phức tạp (tại sao không gọi nó là Excel?) nên nhận 1 mảng dữ liệu và 1 mảng title mô tả từng cột dữ liệu. Để kiểm tra, lấy danh sách sách bán chạy nhất của Wikipedia 
```json
const headers = ['Book', 'Author', 'Language', 'Published', 'Sales'];
const data = [
  [
    'A Tale of Two Cities', 'Charles Dickens',
    'English', '1859', '200 million',
  ],
  [
    'Le Petit Prince (The Little Prince)', 'Antoine de Saint-Exupéry',
    'French', '1943', '150 million',
  ],
  [
    'Harry Potter and the Philosopher's Stone', 'J. K. Rowling',
    'English', '1997', '120 million',
  ],
  [
    'And Then There Were None', 'Agatha Christie',
    'English', '1939', '100 million',
  ],
  [
    'Dream of the Red Chamber', 'Cao Xueqin',
    'Chinese', '1791', '100 million',
  ],
  [
    'The Hobbit', 'J. R. R. Tolkien',
    'English', '1937', '100 million',
  ],
];
```
- Vậy làm sao để render dữ liệu này thành 1 table? Hãy cùng xây dựng data table của bạn
# Table Headers Loop
- Bước đầu tiên để tạo component mới là hiển thị title của table. 
```js
class Excel extends React.Component {
  render() {
    const headers = [];
    for (const title of this.props.headers) {
      headers.push(<th>{title}</th>);
    }
    return (
      <table>
        <thead>
          <tr>{headers}</tr>
        </thead>
      </table>
    );
  }
}
```
- Bây giờ bạn đã có một component hoạt động, đây là cách sử dụng nó
```js
ReactDOM.render(
  <Excel headers={headers} />,
  document.getElementById('app'),
);
```
- Phần return của component khá đơn giản. Nó giống như 1 table HTML ngoại trừ mảng headers
```js
return (
  <table>
    <thead>
      <tr>{headers}</tr>
    </thead>
  </table>
);
```
- Như bạn đã thấy trong chương trước, bạn có thể sử dụng `{}` trong JSX và đặt bất kỳ giá trị biểu thức JS nào trong đó. Nếu giá trị này là 1 mảng như trong trường hợp trước, bộ phân tích cú pháp JSX sẽ xử lý nó giống như việc truyền từng phần tử của 1 mảng một cách riêng biệt. Ví dụ: `{headers[0]}{headers[1]}...`
- Trong ví dụ này, phần tử mảng `headers` chứa nhiều nội dung JSX hơn và điều này hoàn toàn ổn. Vòng lặp trước phần return điền mảng headers bằng các giá trị JSX, nếu bạn mã hoá cứng dữ liệu, nó sẽ trông giống như thế này
```js
const headers = [
  <th>Book</th>,
  <th>Author</th>,
  // ...
];
```
- Bạn có thể có các biểu thức Js trong dấu ngoặc nhọn bên trong JSX và bạn có thể lồng chúng theo nhu cầu. Đây thực sự là 1 vẻ đẹp của React  - bạn có thể tận dụng sức mạnh của Js để tạo UI. Vòng lặp và các điều kiện hoạt động như bình thường và bạn không cần phải học thêm cú pháp Framework nào mới để xây dựng UI
# Table Headers Loop, a Terse Version
- Ví dự trước đã hoạt động tốt (hãy gọi nó là v1), nhưng hãy xem cách bạn có thể đạt được điều tương tự với ít code hơn. Hãy di chuyển vòng lặp vào trong JSX được trả về ở cuối. Về bản chất, toàn bộ phương thức render trở thành 1 return duy nhất
```js
class Excel extends React.Component {
  render() {
    return (
      <table>
        <thead>
          <tr>
            {this.props.headers.map(title => <th>{title}</th>)}
          </tr>
        </thead>
      </table>
    );
  }
}
```
- Hãy xem cách mảng title được gọi ra bằng cách sử dụng map() trên dữ liệu được truyền qua `this.props.headers` . Một cuộc gọi map() nhận 1 mảng đầu vào, thực thi 1 hàm callback trên mỗi phần tử và tạo ra một mảng mới
- Trong ví dụ trước, hàm callback sử dụng cú pháp arrow function ngắn gọn nhất. Nếu điều này hơi khó hiểu đối với bạn, hãy gọi nó là v2 và khám phá thêm các lựa chọn khác
- Đây là v3: Vòng lặp map() rõ ràng hơn
```js
{
  this.props.headers.map(
    function(title) {
      return <th>{title}</th>;
    }
  )
}
```
- Tiếp theo, v4 gọn gàng hơn, sử dụng arrow function
```js
{
  this.props.headers.map(
    (title) => {
      return <th>{title}</th>;
    }
  )
}
```
- Để định dạng đẹp hơn nữa, ta sử dụng v5
```js
{this.props.headers.map((title) => {
  return <th>{title}</th>;
})}
```
- Bạn có thể chọn cách yêu thích của mình để lặp qua mảng để tạo đầu ra JSX dựa trên sở thích cá nhân và độ phức tạp của nội dung cần render. Data đơn giản được lặp qua 1 cách thuận tiện trong JSX (v2 đến v5). Nếu dữ liệu quá nhiều đối với 1 map nội tuyến, bạn có thể thấy dễ đọc hơn khi tạo nội dung ở đầu hàm render() và giữ cho JSX đơn giản, bằng cách nào đó tách biệt việc xử lý dữ liệu khỏi UI (v1 là 1 ví dụ). Đôi khi có quá nhiều biểu thức nội tuyến có thể gây nhầm lẫn khi theo dõi các dấu đóng mở ngoặc
## Debugging the Console Warning
- Khi load 2 ví dụ trước, bạn sẽ thấy warning trong console log của browser
```js
Warning: Each child in a list should have a unique "key" prop.
Check the render method of `Excel`.
```
- Warning này có nghĩa là gì và làm thế nào để khắc phục? Như thông báo cảnh cáo, React muốn bạn cung cấp 1 ID duy nhất cho các phần tử mảng để nó có thể cập nhật chúng hiệu quả hơn sau này. Để khắc phục, bạn thêm thuộc tính `key` vào mỗi title. Các giá trị của thuộc tính mới này có thể là bất kỳ thứ gì miễn là chúng duy nhất cho mỗi phần tử
- Ở đây bạn có thể sử dụng các chỉ mục của mảng
```js
// Truoc
for (const title of this.props.headers) {
  headers.push(<th>{title}</th>);
}

// Sau
for (const idx in this.props.headers) {
  const title = this.props.headers[idx];
  headers.push(<th key={idx}>{title}</th>);
}
```
- Các `key` chỉ cần là duy nhất tromg mỗi vòng lặp mảng, không phải là duy nhất trọng toàn bộ ứng dụng React, vì vậy giá trị 0, 1 là hoàn toàn có thể chấp nhận được
- Cách sửa đổi tương tự như phiên bản nội tuyến (v5) lấy index của phần tử từ đối số thứ 2 được truyền vào callback
```js
// Truoc
<tr>
  {this.props.headers.map((title) => {
    return <th>{title}</th>;
  })}
</tr>

// Sau
<tr>
  {this.props.headers.map((title, idx) => {
    return <th key={idx}>{title}</th>;
  })}
</tr>
```
## Adding <td> Content
- Bây giờ bạn đã có phần title rồi, hãy hoàn thiện phần thân bảng. Dữ liệu cần render là mảng 2 chiều (hàng và cột) trông như sau
```js
const data = [
  [
    'A Tale of Two Cities', 'Charles Dickens',
    'English', '1859', '200 million',
  ],
  ....
];
```
- Để truyền dữ liệu vào `<Excel>` , hãy sử dụng 1 prop mới là `initialData` . Tại sao lại là “initial” thay vì chỉ “data”? Như đã đề cập ngắn gọn trong chương trước, đó và về việc quản lý kỳ vọng. Người gọi component `Excel` của bạn nên có thể truyền dữ liệu để khởi tạo bảng. Nhưng sau đó, khi tiếp tục tồn tại, dữ liệu sẽ thay đổi, bởi vì người dùng có thể sắp xếp, chỉnh sửa,… Nói cách khác, state của component sẽ thay đổi. Vì vậy hãy sử dụng [`this.state.data`](http://this.state.data) để theo dõi các thay đổi và sử dụng `this.props.initialData` để cho phép người gọi khởi tạo component
- Render 1 component excel sẽ trông như thế này
```js
ReactDOM.render(
  <Excel headers={headers} initialData={data} />,
  document.getElementById('app'),
);
```
- Tiếp theo, bạn cần thêm 1 hàm constructor để đặt state ban đầu từ dữ liệu đã cho. Hàm constructor nhận props làm đối số và cũng cần gọi hàm constructor của cha mẹ thông qua super() 
```js
constructor(props) {
  super();
  this.state = {data: props.initialData};
}
```
- Tiếp tục render this.state.data . Dữ liệu là 2 chiều, vì vậy bạn cần 2 vòng lặp: Một vòng lặp lặp qua dữ liệu các hàng và 1 vòng lặp lặp qua dữ liệu (ô) cho mỗi hàng. Điều này có thể thực hiện bằng cách sử dụng 2 vòng lặp map()
```js
{this.state.data.map((row, idx) => (
  <tr key={idx}>
    {row.map((cell, idx) => (
      <td key={idx}>{cell}</td>
    ))}
  </tr>
))}
```
- Như bạn có thể thấy, cả 2 vòng lặp đều cần key={idx} và trong trường hợp này, tên idx  đã được tái sử dụng để làm biến cục bộ bên trong mỗi vòng lặp
```js
class Excel extends React.Component {
  constructor(props) {
    super();
    this.state = {data: props.initialData};
  }

  render() {
    return (
      <table>
        <thead>
          <tr>
            {this.props.headers.map((title, idx) => (
              <th key={idx}>{title}</th>
            ))}
          </tr>
        </thead>
        <tbody>
          {this.state.data.map((row, idx) => (
            <tr key={idx}>
              {row.map((cell, idx) => (
                <td key={idx}>{cell}</td>
              ))}
            </tr>
          ))}
        </tbody>
      </table>
    );
  }
}
```
## Prop Types
- Khả năng xác định kiểu dữ liệu trong các biến mà bạn đã làm việc (string, number,…) không tồn tại trong Js. Nhưng đối với các dev đến từ ngôn ngữ khác, và những người làm việc trên các dự án lớn với nhiều dev khác, họ thực sự nhớ đến điều đó
- Có 2 lựa chọn phổ biến cho phép bạn viết Js với kiểu dữ liệu: Flow và Ts. Bạn chắc chắn có thể sử dụng chúng để viết code React. Nhưng có 1 lựa chọn khác, giới hạn chỉ xác định kiểu dữ liệu của các props mà component của bạn mong đợi bằng `props type` . Ban đầu, chúng là 1 phần của React, nhưng đã được chuyển sang thành 1 thư viện riêng biệt từ bản v15.5
- `Props type` cho phép bạn cụ thể hơn về loại dữ liệu mà `Excel` nhận và do đó hiển thị lỗi cho dev ngay từ đầu. Bạn có thể thiết lập các `props type` như sau
```js
Excel.propTypes = {
  headers: PropTypes.arrayOf(PropTypes.string),
  initialData: PropTypes.arrayOf(PropTypes.arrayOf(PropTypes.string)),
};
```
- Khả năng xác định kiểu dữ liệu trong các biến mà bạn đã làm việc (string, number,…) không tồn tại trong Js. Nhưng đối với các dev đến từ ngôn ngữ khác, và những người làm việc trên các dự án lớn với nhiều dev khác, họ thực sự nhớ đến điều đó
- Có 2 lựa chọn phổ biến cho phép bạn viết Js với kiểu dữ liệu: Flow và Ts. Bạn chắc chắn có thể sử dụng chúng để viết code React. Nhưng có 1 lựa chọn khác, giới hạn chỉ xác định kiểu dữ liệu của các props mà component của bạn mong đợi bằng `props type` . Ban đầu, chúng là 1 phần của React, nhưng đã được chuyển sang thành 1 thư viện riêng biệt từ bản v15.5
- `Props type` cho phép bạn cụ thể hơn về loại dữ liệu mà `Excel` nhận và do đó hiển thị lỗi cho dev ngay từ đầu. Bạn có thể thiết lập các `props type` như sau
```
$ curl -L https://unpkg.com/prop-types/prop-types.js > ~/reactbook/react/proptypes.js
```
- Sau đó, trong HTML bạn bao gồm thư viện mới cùng với các thư viện khác
```js
<script src="react/react.js"></script>
<script src="react/react-dom.js"></script>
<script src="react/babel.js"></script>
<script src="react/prop-types.js"></script>
<script type="text/babel">
  class Excel extends React.Component {
    /* ... */
  }
</script>
```
- Sau đó, trong HTML bạn bao gồm thư viện mới cùng với các thư viện khác
```js
// Truoc
const headers = ['Book', 'Author', 'Language', 'Published', 'Sales'];

// Sau
const headers = [0, 'Author', 'Language', 'Published', 'Sales'];
```
- Khi load lại trang, bạn sẽ thấy trong tab console của browser
```js
Warning: Failed prop type: Invalid prop `headers[0]` of type `number` supplied
to `Excel`, expected `string`.
```
- Thật nghiêm ngặt! Để khám phá các propsType khác, hãy nhập PropsType vào console
## Sorting
- Bao nhiêu lần bạn đã nhìn thấy một table trên trang web mà bạn ước nó được sắp xếp khác đi? May mắn thay, việc này đơn giản với React. Thực tế đây là một ví dụ điển hình về sự “toả sáng” của React, bởi vì bạn chỉ cần sắp xếp mảng dữ liệu và tất cả các cập nhật UI sẽ được xử lý tự động
- Để thuận tiện và dễ đọc, toàn bộ logic được sắp xếp trong phương thức `sort()` của lớp `Excel` . Sau khi tạo phương thức này, bạn cần thêm 2 mảnh ghép quan trọng. Đầu tiên, thêm handler click vào hàng title
```js
<thead onClick={this.sort}>
  ```
- Tiếp theo, ràng thuộc this.sort trong hàm constructor 
```js
class Excel extends React.Component {
  constructor(props) {
    super();
    this.state = {data: props.initialData};
    this.sort = this.sort.bind(this);
  }

  sort(e) {
    // TODO: thực hiện sắp xếp
  }

  render() { /* ...*/}
}
```
- Bây giờ hãy thực hiện phương thức sort() . Bạn cần biết cột nào cần được sắp xếp, điều này có thể dễ dàng truy xuất bằng thuộc tính cellIndex của DOM (DOM là “lõi” của trang web, nơi chứa các phần tử HTML) thuộc đối tượng sự kiện (event target - đây là tiêu đề cột <th>) 
```js
const column = e.target.cellIndex;
```
## Sorting UI Cues
- Table đã được sắp xếp 1 cách đẹp mắt, nhưng người dùng không biết cột nào đang được sort. Hãy cập nhật UI để hiển thị mũi tên dựa trên cột đang được sắp xếp. Và trong khi bạn đang làm điều đó, hãy triển khai sắp xếp theo thứ tự giảm dần
- Để theo dõi state mới, bạn cần thêm 2 thuộc tính vào this.state
    - `this.state.sortby` : Chỉ số của 1 cột hiện đang được sort
    - `this.state.descending` : Một giá trị boolean để xác định sort tăng dần hay giảm dần
- Hàm constructor của chúng ta sẽ trông như thế này:
```js
constructor(props) {
  super();
  this.state = {
    data: props.initialData,
    sortby: null,
    descending: false,
  };
  this.sort = this.sort.bind(this);
}
```
- Trong sort() bạn cần xác định cách sắp xếp. Mặc định tăng dần (từ A đến Z), trừ khi chỉ số của cột mới trông giống với cột sort hiện tại và sắp xếp chưa phải là giảm dần từ lần click trước vào title cột
```js
const column = e.target.cellIndex;
const data = clone(this.state.data);
const descending = this.state.sortby === column && !this.state.descending;
```
- Bạn cũng cần chỉnh sửa nhỏ để cho hàm gọi lại sort
```js
data.sort((a, b) => {
  if (a[column] === b[column]) {
    return 0;
  }
  return descending
    ? a[column] < b[column]
      ? 1
      : -1
    : a[column] > b[column]
      ? 1
      : -1;
});
```
- Cuối cùng bạn cần đặt state mới
```js
this.setState({
  data,
  sortby: column,
  descending,
});
```
- Tại thời điểm này, sắp xếp giảm dần đã hoạt động. Click vào title cột sẽ sắp xếp dữ liệu trước tiên theo thứ tự tăng dần, sau đó giảm dần và sau đó chuyển đổi giữa 2 thứ tự này
- Nhiệm vụ duy nhất còn lại là cập nhật hàm `render()` để hiển thị hướng sort. Đối với cột đang được sort, hãy thêm 1 biểu tượng mũi tên vào title. Giờ đây vòng lặp title sẽ trông như sau:
```js
{this.props.headers.map((title, idx) => {
  if (this.state.sortby === idx) {
    title += this.state.descending ? ' \u2191' : ' \u2193'
  }
  return <th key={idx}>{title}</th>
})}
```
- Chức năng sắp xếp đã hoàn thành - người dùng có thể sắp xếp theo bất kỳ cột nào
## Editing Data
- Bước tiếp theo là cho component Excel là cho phép người dùng chỉnh sửa dữ liệu trong table
    - Click chuột vào 1 ô: Excel sẽ xác định ô được click và chuyển nội dung của nó từ văn bản đơn giản thành input được điền sẵn nội dung
    - Chỉnh sửa nội dung
    - Ấn enter
## Editable Cell
- Bước đầu tiên là thiết lập 1 event handler đơn giản. Khi click đúp, component sẽ ghi nhớ ô được chọn
    
    ```jsx
    <tbody onDoubleClick={this.showEditor}>
    ```
    
- Hãy xem hàm `showEditor`
    
    ```jsx
    showEditor(e) {
      this.setState({
        edit: {
          row: parseInt(e.target.parentNode.dataset.row, 10),
          column: e.target.cellIndex,
        },
      });
    }
    ```
    
- Điều gì xảy ra ở đây
    - Hàm này thiết lập 1 thuộc tính edit của this.state. Thuộc tính này có giá trị null khi không chỉnh sửa và chuyển thành 1 object với các thuộc tính row và column, chứa chỉ số hàng và chỉ sô cột của ô đang được chỉnh sửa. Ví dụ nếu bạn nhấp đúp và ô đầu tiên, this.state.edit sẽ có giá trị `{row: 0, column: 0}`
    - Để xác định chỉ sô cột, bạn sử dụng [`e.target](http://e.target).cellIndex` như trước, trong đó e.target là ô <td> được click đúp
    - Không có `rowIndex` nào được cung cấp sẵn trong DOM, vì vậy bạn cần tự làm bằng thuộc tính `data-` . Mỗi hàng nên có thuộc tính `data-row` với chỉ sô hàng, mà bạn có thể sử dụng parseInt() để lấy lại chỉ số
- Đầu tiên, thuộc tính `edit` chưa từng tồn tại trước đó và cũng nên được khởi tạo trong contructor, hãy ràng buộc phương thức `showEditor()` và `save()`
    
    ```jsx
    constructor(props) {
      super();
      this.state = {
        data: props.initialData,
        sortby: null,
        descending: false,
        edit: null, // {row: index, column: index}
      };
      this.sort = this.sort.bind(this);
      this.showEditor = this.showEditor.bind(this);
      this.save = this.save.bind(this);
    }
    ```
    
- Thuộc tính `data-row` là điều bạn cần theo dõi chỉ số hàng. Bạn có thể lấy index từ index mảng trong khi lặp. Trước đây, bạn đã thấy cách `idx` được sử dụng lại làm biến cục bộ bởi cả vòng lặp hàng và cột, hãy đổi tên nó thành `rowidx` và `columnidx` để rõ ràng hơn
    
    ```jsx
    <tbody onDoubleClick={this.showEditor}>
      {this.state.data.map((row, rowidx) => (
        <tr key={rowidx} data-row={rowidx}>
          {row.map((cell, columnidx) => {
            // TODO - Chuyển `cell` thành một trường nhập liệu nếu `columnidx`
            // và `rowidx` khớp với ô đang được chỉnh sửa;
            // nếu không, chỉ hiển thị nó dưới dạng văn bản
            return <td key={columnidx}>{cell}</td>;
          })}
        </tr>
      ))}
    </tbody>
    ```
    
- Cuối cùng, hãy làm những gì phần TODO yêu cầu - tạo 1 input field nếu cần. Toàn bộ hàm `render()` được gọi lại chỉ bởi hàm `setState()` thiết lập thuộc tính edit. React sẽ hiển thị lại table, điều này cho phép bạn cập nhật ô được click đúp chuột
### Input Field Cell

- Hãy xem đoạn code thay thế cho TODO. Đầu tiên hãy lưu trữ trạng thái edit để cho ngắn gọn
    
    ```jsx
    const edit = this.state.edit;
    ```
    
- Kiểm tra `edit` có được thiết lập hay không, nếu có thì xem đây có phải ô được chỉnh sửa hay không
    
    ```jsx
    if (edit && edit.row === rowidx && edit.column === columnidx) {
      // ...
    }
    ```
    
- Nếu đây là ô mục tiêu, hãy tạo 1 form và 1 input field với nội dung của ô
    
    ```jsx
    cell = (
      <form onSubmit={this.save}>
        <input type="text" defaultValue={cell} />
      </form>
    );
    ```
    
- Như bạn đã thấy, đó là 1 form với 1 input duy nhất được điền sẵn nội dung. Khi form được gửi đi, sự kiện gửi sẽ được xử lý trong phương thức `save()`

### Saving

- Cuối cùng, lưu các thay đổi nội dung khi người dùng hoàn thành nhập và send form (thông qua enter)
    
    ```jsx
    save(e) {
      e.preventDefault();
      // ... thực hiện lưu
    }
    ```
    
- Sau khi ngăn chặn hành vi mặc định, bạn cần tham chiếu đến input. Đối tượng sự kiện [`e.target`](http://e.target) là form và con đầu tiên và duy nhất của nó là input field
    
    ```jsx
    const input = e.target.firstChild;
    ```
    
- Copy data để không sửa trực tiếp vào `this.state`
    
    ```jsx
    const data = clone(this.state.data);
    ```
    
- Update data với value mới, chỉ số row và col được lưu trong thuộc tính edit của state
    
    ```jsx
    data[this.state.edit.row][this.state.edit.column] = input.value;
    ```
    
- Cuối cùng đặt lại state, điều này sẽ gây ra việc render lại UI
    
    ```jsx
    this.setState({
      edit: null,
      data,
    });
    ```
    

### Conclusion and Virtual DOM Diffs

- Tính năng chỉnh sửa đã hoành thành. Tất cả những gì bạn cần làm là:
    - Theo dõi ô nào cần edit thông qua `this.state.edit`
    - Hiển thị 1 input field khi hiển thị nếu index của row và col khớp với ô mà người dùng dblClick
    - Update mảng data mới từ input
- Ngay khi bạn gọi `setState()` với dữ liệu mới, React sẽ gọi `render()` của component và UI sẽ được cập nhật 1 cách **magic.** Có thể bạn sẽ nghĩ việc hiển thị lại toàn bộ table thay vì nội dung của 1 ô sẽ không hiệu quả lắm. Và thực tế, React chỉ cập nhật 1 ô duy nhất trong DOM trình duyệt
- Bạn có thể mở devTool lên, bạn có thể thấy được những phần nào được DOM update khi bạn tương tác với ứng dụng của mình
- Bên dưới lớp vỏ, React gọi phương thức `render()` và tạo 1 cây DOM ảo (virtual DOM tree). Khi `render()` được gọi lại, React sẽ lấy cây ảo trước và sau tính toán 1 diff(sự khác biệt). Dựa vào diff này, React sẽ xác định các thao tác DOM tối thiểu cần thiết để thực hiện thay đổi đó vào DOM của browser
- Bằng cách tính toán thay đổi tối thiểu và gộp các thao tác DOM, React chỉ **chạm** nhẹ vào DOM
- React hỗ trợ bạn về hiệu suất và cập nhật UI bằng cách:
    - Chạm nhẹ vào DOM
    - Sử dụng uỷ thác sự kiện (event delegation) cho sự tương tác của ứng dụng

## Search

- Tiếp theo thêm tính năng search vào component Excel
    - Thêm 1 nút để bật tắt tính năng tìm kiếm
    - Nếu tính năng tìm kiếm được bật, thêm 1 hàng input, mỗi input sẽ search trong cột tương ứng
    - Khi người dùng nhập vào input, hãy lọc mảng [state.data](http://state.data) để chỉ hiển thị nội dung phù hợp
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9a9d30aa-4822-4cd2-ade5-57a403553962/7512d3a8-06bc-49ed-a1cf-e6bb5acd2001/image.png)
    

### State and UI

- Đầu tiên, hãy cập nhật hàm constructor bằng cách:
    - Thêm thuộc tính `search` vào đối tượng `this.state` để xem tính năng search có được bật hay không.
    - Ràng buộc 2 phương thức mới: `this.toggleSearch()` để bật/tắt search và `this.search()` để thực hiện tìm kiếm thực tế
    - Thiết lập thuộc tính lớp mới `this.preSearchData`
    - Cập nhật data ban đầu được truyền vào với 1 ID liên tiếp để giúp xác định các hàng khi chỉnh sửa nội dung của dữ liệu được lọc
        
        ```jsx
        constructor(props) {
          super();
          const data = clone(props.initialData).map((row, idx) => {
            row.push(idx);
            return row;
          });
          this.state = {
            data,
            sortby: null,
            descending: false,
            edit: null, // {row: index, column: index}
            search: false,
          };
          this.preSearchData = null;
          this.sort = this.sort.bind(this);
          this.showEditor = this.showEditor.bind(this);
          this.save = this.save.bind(this);
          this.toggleSearch = this.toggleSearch.bind(this);
          this.search = this.search.bind(this);
        }
        ```
        
- Việc copy và update `initialData` sẽ thay đổi dữ liệu được sử dụng trong state bằng cách thêm 1 loại ID bản ghi. Điều này hữu ích khi chỉnh sửa dữ liệu đã được lọc. Bạn dùng map() trên data, thêm 1 cột bổ sung là ID số nguyên
    
    ```jsx
    const data = clone(props.initialData).map((row, idx) =>
      row.concat(idx),
    );
    ```
    
- Kết quả là, [`this.state.data`](http://this.state.data) giờ sẽ trông như sau
    
    ```jsx
    [
      'A Tale of Two Cities', ..., 0
    ],
    [
      'Le Petit Prince (The Little Prince)', ..., 1
    ],
    // ...
    ```
    
- Thay đổi này cũng yêu cầu thay đổi phương thức render(), cụ thể là sử dụng ID bản ghi này để xác định các hàng, bất kể chúng ta đang xem tất cả data hay một tập hợp con được lọc của nó
    
    ```jsx
    {this.state.data.map((row, rowidx) => {
      // Phần dữ liệu cuối cùng trong một hàng là ID
      const recordId = row[row.length - 1];
      return (
        <tr key={recordId} data-row={recordId}>
          {row.map((cell, columnidx) => {
            if (columnidx === this.props.headers.length) {
              // Không hiển thị ID bản ghi trong UI của bảng
              return;
            }
            const edit = this.state.edit;
            if (
              edit &&
              edit.row === recordId &&
              edit.column === columnidx
            ) {
              cell = (
                <form onSubmit={this.save}>
                  <input type="text" defaultValue={cell} />
                </form>
              );
            }
            return <td key={columnidx}>{cell}</td>;
          })}
        </tr>
      );
    })}
    ```
    
- Tiếp theo là cập nhật UI với nút tìm kiếm. Trước đây, có 1 table làm gốc, bây giờ có 1 div với 1 nút tìm kiếm và cùng 1 bảng
    
    ```jsx
    <div>
      <button className="toolbar" onClick={this.toggleSearch}>
        {this.state.search ? 'Hide search' : 'Show search'}
      </button>
      <table>
        {/* ... */}
      </table>
    </div>
    ```
    
- Như bạn đã thấy, label của nút search là động, để phản ánh xem [this.state.search](http://this.state.search) là true hoặc false
- Tiếp theo là hàng hộp tìm kiếm. Bạn có thể thêm nó vào phần JSX ngày càng lớn, hoặc bạn có thể nó trước và thêm vào 1 hằng số được bao gồm trong JSX chính. Hãy đi theo con đường thứ 2. Nếu tính năng tìm kiếm không được bật, bạn không cần phải hiển thị gì, vì vậy `searchRow` chỉ là null. Nếu không, một hàng bảng mới sẽ được tạo, trong đó mỗi ô là 1 input
    
    ```jsx
    const searchRow = !this.state.search ? null : (
      <tr onChange={this.search}>
        {this.props.headers.map((_, idx) => (
          <td key={idx}>
            <input type="text" data-idx={idx} />
          </td>
        ))}
      </tr>
    );
    ```
    
- Hàng input search chỉ là một nút con khác trước vòng lặp dữ liệu chính (vòng lặp tạo ra tất cả các hàng và ô bảng). Bao gồm `searchRow` ở đó:
    
    ```jsx
    <tbody onDoubleClick={this.showEditor}>
      {searchRow}
      {this.state.data.map((row, rowidx) => (....
    ```
    

## Filtering Content

- Tính năng filter sẽ khá đơn giản: Gọi phương thức `Array.prototype.filter()` trên mảng dữ liệu và trả về 1 mảng được lọc với các phần tử khớp với chuỗi tìm kiếm. UI vẫn sử dụng [`this.state.data`](http://this.state.data) để hiển thị, nhưng `this.state.data` là 1 phiên bản rút gọn của chính nó
- Bạn cần 1 tham chiếu đến dữ liệu trước khi tìm kiếm, để bạn không bị mất đi dữ liệu mãi mãi. Điều này cho phép người dùng quay lại bảng đầy đủ hoặc đổi chuỗi tìm kiếm để có được kết quả phù hợp khác. Bây giờ có dữ liệu ở 2 nơi, phương thức save() sẽ cần được update, để cả 2 nơi cần được update nếu người dùng quyết định chỉnh sửa dữ liệu bất kể nó đã được lọc hay chưa
- Khi người dùng click vào nút search, hàm `toggleSearch()` được gọi. Nhiệm vụ của hàm này là bật tắt tính năng search. Nó thực hiện nhiệm vụ của mình bằng cách
    - Thiết lập [`this.state.search`](http://this.state.search) thành true hoặc false cho phù hợp
    - Khi bật search, “ghi nhớ” dữ liệu hiện tại
    - Khi tắt search, khôi phục dữ liệu được “ghi nhớ”
- Dưới đây là cách hàm này có thể được viết
    
    ```jsx
    toggleSearch() {
      if (this.state.search) {
        this.setState({
          data: this.preSearchData,
          search: false,
        });
        this.preSearchData = null;
      } else {
        this.preSearchData = this.state.data;
        this.setState({
          search: true,
        });
      }
    }
    ```
    
- Điều cuối cùng cần làm là thực hiện hàm `search()` được gọi mỗi khi có thay đổi trong hàng search, nghĩa là người dùng nhập vào 1 trong các input. Dưới đây là toàn bộ, tiếp theo là một số chi tiết bổ sung
    
    ```jsx
    search(e) {
      const needle = e.target.value.toLowerCase();
      if (!needle) {
        this.setState({data: this.preSearchData});
        return;
      }
      const idx = e.target.dataset.idx;
      const searchdata = this.preSearchData.filter((row) => {
        return row[idx].toString().toLowerCase().indexOf(needle) > -1;
      });
      this.setState({data: searchdata});
    }
    ```
    
- Bạn lấy chuỗi tìm kiếm từ mục tiêu của sự kiện thay đổi (đó là ô input). Hãy gọi nó là “needle(kim)” vì chúng ta đang tìm 1 cái kim trong đống dữ liệu
    
    ```jsx
    const needle = e.target.value.toLowerCase();
    ```
    
- Nếu không có chuỗi tìm kiếm (người dùng xoá hết những gì đã nhập), hàm này sẽ lấy dữ liệu gốc được lưu trữ trong bộ nhớ cache và dữ liệu này sẽ trở thành state mới
    
    ```jsx
    if (!needle) {
      this.setState({data: this.preSearchData});
      return;
    }
    ```
    
- Nếu có chuỗi tìm kiếm, hãy lọc dữ liệu gốc và thiết lập các kết quả được lọc làm state mới của dữ liệu
    
    ```jsx
    const idx = e.target.dataset.idx;
    const searchdata = this.preSearchData.filter((row) => {
      return row[idx].toString().toLowerCase().indexOf(needle) > -1;
    });
    this.setState({data: searchdata});
    ```
    
- Và với điều này, tính năng tìm kiếm đã hoàn tất. Để thực hiện tính năng này, tất cả những gì bạn cần làm là
    - Thêm UI tìm kiếm
    - Hiển thị/ẩn Ui mới theo yêu cầu
    - “Logic nghiệp vụ thực tế” : Một cuộc gọi filter() mảng đơn giản
- Như thường lệ, bạn chỉ cần lo lắng về state dữ liệu của mình và để React xử lý việc hiển thị (và tất cả các công việc DOM liên quan) bất cứ khi nào state dữ liệu thay đổi

### Update the save() Method

- Trước đây, chỉ có [state.data](http://state.data) được copy và update, nhưng bây giờ bạn cũng có cả preSearchData được **ghi nhớ.** Nếu người dùng đang chỉnh sửa(ngay cả khi đang search), bây giờ 2 phần dữ liệu cần được cập nhật. Đó là lý do chính để thêm ID bản ghi - để bạn có thể tìm thấy hàng thực sự ngay cả trong state được lọc
- Cập nhật `preSearchData` giống như thực hiện `save()` trước đó; chỉ cần tìm hàng và cột. Cập nhật state data yêu cầu bước bổ sung là tìm ID bản ghi của hàng và khớp với hàng hiện tại đang được chỉnh sửa `this.state.edit.row`
    
    ```jsx
    save(e) {
      e.preventDefault();
      const input = e.target.firstChild;
      const data = clone(this.state.data).map((row) => {
        if (row[row.length - 1] === this.state.edit.row) {
          row[this.state.edit.column] = input.value;
        }
        return row;
      });
      this.logSetState({
        edit: null,
        data,
      });
      if (this.preSearchData) {
        this.preSearchData[this.state.edit.row][this.state.edit.column] =
          input.value;
      }
    }
    ```
    

## Instant Replay

- Như bạn đã biết, các component của bạn lo lắng về state của chúng va để React hiển thị lại bất cứ khi nào phù hợp. Điều này có nghĩa là với cùng 1 dữ liệu (state và props), ứng dụng sẽ trông giống hệt nhau, bất kể những gì thay đổi trước hoặc sau state dữ liệu cụ thể này. Điều này mang đến cơ hội tuyệt vời cho bạn để gỡ lỗi trong thực tế
- Hãy tưởng tượng ai đó gặp lỗi khi sử dụng ứng dụng của bạn - họ có thể click vào 1 nút để báo cáo lỗi mà không cần giải thích điều gì đã xảy ra. Báo lỗi này chỉ cần gửi lại cho bạn 1 bản sao của this.state và this.props, và bạn có thể tạo lại chính xác trạng thái của ứng dụng và xem kết quả trực quan
- “undo” có thể là 1 tính năng khác, vì React hiển thị ứng dụng của bạn theo cùng 1 cách với cùng 1 props và state. Trên thực tế, thực hiện “undo” khá đơn giản: bạn chỉ cần quay lại state trước đó.
- Hãy đưa ý tưởng đó xa hơn 1 chút, chỉ để cho vui. Hãy ghi lại mỗi thay đổi state trong Excel component và sau đó phát lại. Thật thú vị khi xem tất cả các hành động của bạn được phát lại trước mặt bạn. Câu hỏi về khi nào thay đổi xảy ra không quá quan trọng, vì vậy hãy “phát” các thay đổi state của ứng dụng theo khoảng thời gian 1s
- Để thực hiện tính năng này, bạn cần thêm 1 phương thức logSetState() trước tiên sẽ ghi log state vào 1 mảng `this.log` và sau đó gọi `setState()` . Tất cả mọi nơi trong mã mà bạn đã gọi `setState()` giờ sẽ được thay đổi thành `logSetState()` . Đầu tiên, hãy tìm kiếm và thay thế tất cả các cuộc gọi đến `setState()` bằng các hàm mới
    
    ```jsx
    this.setState(...);
    
    se tro thanh
    
    this.logSetState(...);
    ```
    
- Bây giờ hãy chuyển sang hàm constructor. Bạn cần ràng buộc 2 hàm mới, `logSetState()` và `replay()` khai báo mảng `this.log` và gán state ban đầu cho nó
    
    ```jsx
    constructor(props) {
      // ...
      // Ghi nhật ký trạng thái ban đầu
      this.log = [clone(this.state)];
      // ...
      this.replay = this.replay.bind(this);
      this.logSetState = this.logSetState.bind(this);
    }
    ```
    
- `logSetState` cần làm 2 việc: ghi log state mới và sau đó chuyển nó sang `setState()` . Dưới đây là 1 ví dụ thực hiện nơi bạn tạo ra bản sao sâu của state và nối nó vào this.log
    
    ```jsx
    logSetState(newState) {
      // Ghi nhớ trạng thái cũ trong một bản sao
      this.log.push(clone(newState));
      // Bây giờ hãy thiết lập nó
      this.setState(newState);
    }
    ```
    
- Bây giờ tất cả các thay đổi state đều được ghi log lại, hãy phát lại chúng. Để kích hoạt phát lại, hãy thêm một event handler đơn giản sẽ bắt các action của bàn phím và gọi hàm `replay()` . Nơi dành cho các event handler như thế này là trong phương thức vòng đời componentDidMount()
    
    ```jsx
    componentDidMount() {
      document.addEventListener('keydown', e => {
        if (e.altKey && e.shiftKey && e.keyCode === 82) {
          // ALT+SHIFT+R(eplay)
          this.replay();
        }
      });
    }
    ```
    
- Cuối cùng, hãy xem xét phương thức `replay()` . Nó sử dụng setInterval() và mỗi giây nó sẽ đọc object tiếp theo từ log và chuyển nó sang setState()
    
    ```jsx
    replay() {
      if (this.log.length === 1) {
        console.warn('Chưa có thay đổi trạng thái nào để phát lại');
        return;
      }
      let idx = -1;
      const interval = setInterval(() => {
        if (++idx === this.log.length - 1) {
          // Kết thúc
          clearInterval(interval);
        }
        this.setState(this.log[idx]);
      }, 1000);
    }
    ```
    

### Cleaning Up Event Handlers

- Tính năng replay() cần được dọn dẹp 1 chút. Khi component này là thứ duy nhất được diễn ra trên trang, việc cleanup là không cần thiết; trong 1 ứng dụng thực tế, các component được thêm vào và xoá khỏi DOM thường xuyên hơn. Khi xoá khỏi DOM, 1 component tốt bụng nên dọn dẹp chính nó. Trong ví dụ trên, có 2 mục cần được cleanup: event handler `keydown` và interval callback
- Nếu bạn không cleanup event handler keydown, nó sẽ tồn tại trong bộ nhớ sau khi component biến mất. Và vì nó đang sử dụng this, toàn bộ instance Excel cần được giữ lại trong bộ nhớ, điều này thực sự là một rò rỉ bộ nhớ. Quá nhiều rò rỉ bộ nhớ như vậy và người dùng có thể hết bộ nhớ và ứng dụng của bạn có thể làm sập tab trình duyệt
- Đối với interval, hàm gọi lại sẽ tiếp tục thực thi khi component biến mất và gây ra rò rỉ bộ nhớ khác. Callback function sẽ cố gắng gọi `setState()` trên 1 component không tồn tại
- Bạn có thể test bằng cách xoá componet ra khỏi DOM trong khi replay vẫn đang diễn ra. Để xoá component ra khỏi DOM, bạn chỉ cần thay thế nó
    
    ```jsx
    ReactDOM.render(
      React.createElement('h1', null, 'Hello world!'),
      document.getElementById('app'),
    );
    ```
    
- Bạn cũng có thể ghi log trong callback function để xem nó tiếp tục được thực thi
    
    ```jsx
    const interval = setInterval(() => {
      // ...
      console.log(Date.now());
      // ...
    }, 1000);
    ```
    
- Bây giờ, khi bạn thay thế component trong khi phát lại, bạn sẽ thấy lỗi từ React và dấu thời gian của callback function interval vẫn được ghi log, bằng chứng cho thấy hàm vẫn đang chạy
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9a9d30aa-4822-4cd2-ade5-57a403553962/d9ad43bd-bd6e-404e-adc2-e8956cf07d70/image.png)
    
- Tương tự, bạn có thể kiểm tra rò rỉ bộ nhớ bằng cách nhấn Alt + Shift + R sau khi component bị xoá khỏi DOM

### Cleaning Solution

- Việc xử lý rò rỉ này khá đơn giản. Bạn cần giữ tham chiếu đến các event handler và khoảng thời gian/hẹn giờ mà bạn muốn cleanup. Sau đó dọn dẹp chúng trong `componentWillUnMount()`
- Đối với event handler, hãy tạo thành 1 class method thay vì 1 hàm inline
    
    ```jsx
    keydownHandler(e) {
      if (e.altKey && e.shiftKey && e.keyCode === 82) {
        // ALT+SHIFT+R(eplay)
        this.replay();
      }
    }
    ```
    
- Sau đó, componentDidMount() trở nên đơn giản hơn
    
    ```jsx
    componentDidMount() {
      document.addEventListener('keydown', this.keydownHandler);
    }
    ```
    
- Đối với ID phát lại interval, hãy tạo nó thành một class property thay vì 1 biến cục bộ
    
    ```jsx
    this.replayID = setInterval(() => {
      if (++idx === this.log.length - 1) {
        // Kết thúc
        clearInterval(this.replayID);
      }
      this.setState(this.log[idx]);
    }, 1000);
    ```
    
- Và tất nhiên bạn cần ràng buộc phương thức mới vào hàm `constructor`
    
    ```jsx
    constructor(props) {
      // ...
      this.replayID = null;
      // ...
      this.keydownHandler = this.keydownHandler.bind(this);
    }
    ```
    
- Và cuối cùng dọn dẹp chúng trong `componentWillUnMount()`
    
    ```jsx
    componentWillUnmount() {
      document.removeEventListener('keydown', this.keydownHandler);
      clearInterval(this.replayID);
    }
    ```
    

## Download the Table Data

- Sau khi sắp xếp, chỉnh sửa, tìm kiếm, cuối cùng người dùng cũng hài lòng với state của data trong bảng. Sẽ thật tuyệt nếu họ có thể download data, kết quả của tất cả công sức của họ, để sử dụng sau này
- May mắn thay, không có gì dễ dàng hơn trong React. Tất cả những gì bạn cần làm là lấy [`this.state.data`](http://this.state.data) hiện tại và trả lại nó - ví dụ ở định dạng JSON hoặc giá trị được phân cách bởi dấu phẩy (CSV)
- Đầu tiên cần làm là thêm các tuỳ chọn mới vào thanh công cụ (nơi có nút search). Hãy sử dụng 1 chút “magic” HTML buộc `<a>` kích hoạt download file
    
    ```jsx
    <div className="toolbar">
      <button onClick={this.toggleSearch}>
        {this.state.search ? 'Hide search' : 'Show search'}
      </button>
      <a href="data.json" onClick={this.downloadJSON}>
        Export JSON
      </a>
      <a href="data.csv" onClick={this.downloadCSV}>
        Export CSV
      </a>
    </div>
    ```
- Như bạn đã thấy,  bạn cần các phương thức `downloadJson()` và `downloadCSV()` . Những phương thức này có 1 số logic lặp lại, vì vậy chúng có thể thực hiện bởi 1 hàm `download` duy nhất được ràng buộc với đối số định dạng (nghĩa là kiểu tệp). Chữ ký của `download()` có thể giống như:
    
    ```jsx
    download(format, ev) {
      // TODO: thực hiện
    }
    ```
    
- Trong hàm constructor bạn có thể ràng buộc phương thức này 2 lần như sau
    
    ```jsx
    this.downloadJSON = this.download.bind(this, 'json');
    this.downloadCSV = this.download.bind(this, 'csv');
    ```
    
- Tất cả công việc của React đã được thực hiện, bây giờ đến hàm download. Trong khi xuất định dạng JSON là đơn giản, CSV cần thêm 1 chút công việc. Về bản chất, nó chỉ là 1 vòng lặp lặp qua các hàng và các ô trong 1 hàng, tạo ra 1 chuỗi dài. Sau khi hoàn thành, hàm này sẽ khởi tạo tải xuống thông qua thuộc tính `download` và blob `href` được tạo bởi `windown.URL`
    
    ```jsx
    download(format, ev) {
      const data = clone(this.state.data).map(row => {
        row.pop(); // bỏ cột cuối cùng, ID bản ghi
        return row;
      });
      const contents =
        format === 'json'
          ? JSON.stringify(data, null, ' ')
          : data.reduce((result, row) => {
              return (
                result +
                row.reduce((rowcontent, cellcontent, idx) => {
                  const cell = cellcontent.replace(/"/g, '""');
                  const delimiter = idx < row.length - 1 ? ',' : '';
                  return `${rowcontent}"${cellcontent}"${delimiter}`;
                }, '') +
                '\n'
              );
            }, '');
      const URL = window.URL || window.webkitURL;
      const blob = new Blob([contents], { type: 'text/' + format });
      ev.target.href = URL.createObjectURL(blob);
      ev.target.download = 'data.' + format;
    }
    ```
    

## Fetching Data

- Trong suốt chương này, component Excel đã có quyền truy cập vào cùng 1 file. Nhưng nếu dữ liệu nằm ở 1 nơi khác trên server và cần được lấy? Có nhiều giải pháp khác nhau cho việc này và bạn sẽ thấy trong các chương sau của sách, nhưng hãy thử 1 trong những phương pháp đơn giản nhất - lấy dữ liệu trong componentDidMount()
- Hãy nói rằng, component Excel được tạo với initialData trống
    
    ```jsx
    ReactDOM.render(
      <Excel headers={headers} initialData={[]} />,
      document.getElementById('app'),
    );
    ```
    
- Component có thể hiển thị state trung gian một cách duyên dáng để người dùng biết rằng dữ liệu đang đến. Trong phương thức render() bạn có thể có 1 điều kiện và hiển thị một phần tử bảng khác nếu dữ liệu không có
    
    ```jsx
    {this.state.data.length === 0 ? (
      <tbody>
        <tr>
          <td colSpan={this.props.headers.length}>
            Loading data...
          </td>
        </tr>
      </tbody>
    ) : (
      <tbody onDoubleClick={this.showEditor}>
        {/* ... giống như trước ...*/}
      </tbody>
    )}
    ```
    
- Bây giờ hãy lấy dữ liệu. Sử dụng API fetch, hãy thực hiện 1 request đến server và khi response đến, hãy đặt state với dữ liệu mới. Bạn cũng cần chú ý đến việc thêm ID vào bản ghi, điều này trước đây là công việc của constructor
    
    ```jsx
    componentDidMount() {
      document.addEventListener('keydown', this.keydownHandler);
      fetch('https://www.phpied.com/files/reactbook/table-data.json')
        .then((response) => response.json())
        .then((initialData) => {
          const data = clone(initialData).map((row, idx) => {
            row.push(idx);
            return row;
          });
          this.setState({ data });
        });
    }
    ```
