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

