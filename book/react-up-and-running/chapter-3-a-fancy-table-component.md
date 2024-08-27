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
    "Harry Potter and the Philosopher's Stone", 'J. K. Rowling',
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