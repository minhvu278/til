# Functional Excel
- Bạn còn nhớ các function component không? Tại một sổ điểm trong Chương 2, ngay khi state xuất hiện, các function component đã bị loại bỏ khỏi cuộc thảo luận. Đã đến lúc chúng trở lại

## A Quick Refresher: Function versus Class Components

- Trong dạng đơn giản nhất, một class component chỉ cần 1 phương thức render(). Đây là nơi bạn xây dựng UI, tuỳ chọn sử dụng this.props và this.state
    
    ```jsx
    class Widget extends React.Component {
      render() {
        let ui;
        // Thực hiện với this.props và this.state
        return <div>{ui}</div>;
      }
    }
    ```
    
- Trong 1 function component, toàn bộ component là function và UI là bất cứ điều gì hàm trả về. `props` được truyền vào function khi component được tạo
    
    ```jsx
    function Widget(props) {
      let ui;
      // Thực hiện với props nhưng trạng thái ở đâu?
      return <div>{ui}</div>;
    }
    ```
    
- Sự hữu ích của các function component đã kết thúc với React v16.8: Bạn chỉ có thể sử dụng chung cho các component stateless (không state). Nhưng với viêc bổ sung hook trong v16.8, giờ đây bạn có thể sử dụng các component ở mọi nơi
- Trong phần còn lại của chương này, bạn sẽ thấy cách component Excel từ chương 3 có thể được thực hiện dưới dạng 1 function component

## Rendering the Data

- Bước đầu tiên là hiển thị dữ liệu được truyền vào component. Cách component được sử dụng không thay đổi. Nói cách khác, một developer sử dụng component của bạn không cần phải biết component của bạn là class hay function. `initialData` và `headers` props trông giống nhau. Ngay cả định nghĩa `propTypes` cũng giống nhau
    
    ```jsx
    function Excel(props) {
      // thực hiện...
    }
    
    Excel.propTypes = {
      headers: PropTypes.arrayOf(PropTypes.string),
      initialData: PropTypes.arrayOf(PropTypes.arrayOf(PropTypes.string)),
    };
    
    const headers = ['Book', 'Author', 'Language', 'Published', 'Sales'];
    const data = [
      [
        'A Tale of Two Cities', 'Charles Dickens', // ...
      ],
      // ...
    ];
    
    ReactDOM.render(
      <Excel headers={headers} initialData={data} />,
      document.getElementById('app'),
    );
    ```
    
- Việc thực hiện phần thân của function component phần lớn là copy và paste phần thân của phương thức render() của class component
    
    ```jsx
    function Excel({ headers, initialData }) {
      return (
        <table>
          <thead>
            <tr>
              {headers.map((title, idx) => (
                <th key={idx}>{title}</th>
              ))}
            </tr>
          </thead>
          <tbody>
            {initialData.map((row, idx) => (
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
    ```
    
- Trong đoạn code trên, bạn có thể thấy rằng thay vì `function Excel(props){}` bạn có thể sử dụng cú pháp destructuring `function Excel({ headers, initialData}){}` để đỡ phải gõ `props.headers` và `props.initialData`

## The State Hook

- Để có thể duy trì state trong function component, bạn cần hook. Hook là gì? Nó là 1 function được thêm tiền tô `use*` cho phép bạn sử dụng nhiều tính năng của React, chẳng hạn như công cụ để quản lý state và lifecycle component. Bạn cũng có thể tạo hook của riêng mình. Đến cuối chương này, bạn sẽ học cách sử dụng một số hook được tích hợp sẵn cũng như viết hook của riêng mình.
- Hãy bắt đầu với hook state. Nó là 1 function có tên `useState()` có sẵn dưới dạng 1 property của React object (React.useState()). Nó nhận 1 giá trị, giá trị ban đầu của 1 biến state (một phần dữ liệu mà bạn muốn quản lý) và trả về 1 mảng gồm 2 phần tử (một tuple). Phần từ đầu tiên là biến state và phần tử thứ 2 là 1 hàm để thay đổi biến này. Hãy xem 1 ví dụ
- Trong 1 class component, trong constructor(), bạn định nghĩa các giá trị ban đầu như sau
    
    ```jsx
    this.state = {
      data: initialData;
    };
    ```
    
- Sau này, khi bạn muốn thay đổi state dữ liệu, bạn có thể làm như sau:
    
    ```jsx
    this.setState({
      data: newData,
    });
    ```
    
- Trong 1 function component, bạn định nghĩa cả state ban đầu và một hàm cập nhật
    
    ```jsx
    const [data, setData] = React.useState(initialData);
    ```
    
- Lưu ý, cú pháp destructuring, trong đó bạn gán 2 phần tử của mảng được trả về bởi useState() cho 2 biến: `data` và `setData` . Đây là cách ngắn gọn và clean hơn để lấ 2 giá trị trả về, ví dụ:
    
    ```jsx
    const stateArray = React.useState(initialData);
    const data = stateArray[0];
    const setData = stateArray[1];
    ```
    
- Để hiể thị, bạn co thể sử dụng biến data. Khi bạn muốn cập nhật biến này, hãy sử dụng:
    
    ```jsx
    setData(newData)
    ```
    
- Việc viết lại component để sử dụng state hook giờ có thể trông như thế này
    
    ```jsx
    function Excel({ headers, initialData }) {
      const [data, setData] = React.useState(initialData);
      return (
        <table>
          <thead>
            <tr>
              {headers.map((title, idx) => (
                <th key={idx}>{title}</th>
              ))}
            </tr>
          </thead>
          <tbody>
            {data.map((row, idx) => (
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
    ```
## Sorting the Table

- Trong 1 class component, tất cả các phần state khác nhau sẽ được đưa vào object `this.state` , một “túi đựng” các thông tin thường không liên quan đến nhau. Sử dụng state hook, bạn vẫn có thể làm điều tương tự, nhưng bạn cũng có thể quyết định giữ các phần state trong các biến khác nhau
- Khi nói đến việc sort table, data có trong table là 1 phần thông tin, trong khi thông tin bổ sung dành riêng cho việc sort là 1 phần thông tin khác. Nói cách khác, bạn có thể sử dụng state hook nhiều lần tuỳ thích
    
    ```jsx
    function Excel({ headers, initialData }) {
      const [data, setData] = React.useState(initialData);
      const [sorting, setSorting] = React.useState({
        column: null,
        descending: false,
      });
      // ....
    }
    ```
    
- `data` là những gì bạn hiển thị trong table; object `sorting` là một mối quan tâm riêng biệt. Nó liên quan đến cách bạn sắp xếp (tăng hoặc giảm dần) và theo cột vào (title, author,…)
- Function thực hiện việc sắp xếp giờ được đặt inline bên trong hàm Excel
    
    ```jsx
    function Excel({ headers, initialData }) {
      // ..
      function sort(e) {
        // thực hiện...
      }
      return (
        <table>
          {/* ... */}
        </table>
      );
    }
    ```
    
- Function `sort()` xác định cột nào cần được sắp xếp (bằng cách sử dụng chỉ số của nó) và việc sort có thể giảm dần hay không
    
    ```jsx
    const column = e.target.cellIndex;
    const descending = sorting.column === column && !sorting.descending;
    ```
    
- Sau đó, nó sao chép array data vì vẫn là 1 ý tưởng tồi khi sửa đổi state trực tiếp
    
    ```jsx
    const dataCopy = clone(data);
    ```
    
- Lưu ý rằng function `clone()` vẫn là cách nhanh chóng và bẩn để sao chép sâu bằng cách mã hoá/giải mã JSON
    
    ```jsx
    function clone(o) {
      return JSON.parse(JSON.stringify(o));
    }
    ```
    
- Việc sắp xếp thực tế giống như trước
    
    ```jsx
    dataCopy.sort((a, b) => {
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
    
- Và cuối cùng, hàm `sort()` cần cập nhật 2 phần state với các giá trị mới
    
    ```jsx
    setData(dataCopy);
    setSorting({ column, descending });
    ```
    
- Và đó là về cơ bản cho việc sort. Những gì còn lại là chỉ cập nhật UI (giá trị trả về của Excel()) để phản ánh cột nào được sử dụng để sắp xếp và để xử lý click vào bất kỳ tiêu đề nào
    
    ```jsx
    <thead onClick={sort}>
      <tr>
        {headers.map((title, idx) => {
          if (sorting.column === idx) {
            title += sorting.descending ? ' \u2191' : ' \u2193';
          }
          return <th key={idx}>{title}</th>;
        })}
      </tr>
    </thead>
    ```
    
- Bạn có thể nhận thấy 1 điều thú vị khác về việc sử dụng state hook: Không cần phải ràng buộc bất kỳ callback function nào như bạn đã làm trong constructor của 1 class component. Không có việc `this.sort = this.sort.bind(this) nào nữa. Không có this, không co hàm constructor(). 1 function là tất cả những gì bạn cần để định nghĩa 1 component

## Editing Data

- Như bạn nhớ từ chương 3, chức năng chỉnh sửa bao gồm các bước sau
    - dbClick vào 1 ô table và nó chuyển thành 1 input
    - Nhập dữ liệu vào input
    - Khi hoàn thành, nhấn enter để send form
- Để theo dõi quá trình này, hãy thêm 1 object `edit` . Nó có giá trị null khi không edit; nếu không, nó sẽ lưu trữ chỉ số hàng và cột của ô đang được edit
    
    ```jsx
    const [edit, setEdit] = useState(null);
    ```
    
- Trong UI, bạn cần xử lý dbClick và nếu người dùng đang edit, hãy hiển thị 1 form. Nếu không, chỉ cần hiển thị data. Khi người dùng nhấn enter, bạn sẽ bắt event submit
    
    ```jsx
    <tbody onDoubleClick={showEditor}>
      {data.map((row, rowidx) => (
        <tr key={rowidx} data-row={rowidx}>
          {row.map((cell, columnidx) => {
            if (
              edit &&
              edit.row === rowidx &&
              edit.column === columnidx
            ) {
              cell = (
                <form onSubmit={save}>
                  <input type="text" defaultValue={cell} />
                </form>
              );
            }
            return <td key={columnidx}>{cell}</td>;
          })}
        </tr>
      ))}
    </tbody>
    ```
    
- Có 2 function ngắn còn lại cần được thực hiện: `showEditor()` và `save()`
- Hàm `showEditor` được gọi khi dbClick và 1 ô trong phần tử table. Tại đó, bạn cập nhật trạng thái edit với chỉ sô hàng và cột, để việc hiển thị biết ô nào cần được thay thế bởi form
    
    ```jsx
    function showEditor(e) {
      setEdit({
        row: parseInt(e.target.parentNode.dataset.row, 10),
        column: e.target.cellIndex,
      });
    }
    ```
    
- Function `save()` bắt event submit, ngăn chặn việc gửi và cập nhật state với giá trị mới trong ô đang được edit. Nó cũng gọi `setEdit()` truyền null làm state edit mới, có nghĩa là việc chỉnh sửa đã hoàn thành
    
    ```jsx
    function save(e) {
      e.preventDefault();
      const input = e.target.firstChild;
      const dataCopy = clone(data);
      dataCopy[edit.row][edit.column] = input.value;
      setEdit(null);
      setData(dataCopy);
    }
    ```
