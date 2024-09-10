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
## Searching

- Search/filter không đặt ra bất kỳ thách thức mới nào khi nói đến React và hook
- Bạn sẽ cần 2 phần  `state` mới
    - `search` kiểu boolean để biểu thị xem người dùng đang filter hay chỉ xem data
    - `preSearchData` là bản sao của dữ liệu, bởi vì giờ `data` trở thành 1 tập hợp con được filter của tất cả data
- Bạn cần chú ý đến việc giữ `preSearchData` được update, vì data (tập hợp con được filter) có thể được update khi người dùng đang edit trong khi đang filter
- Hãy chuyển sang việc thực hiện tính năng phát lại, điều này sẽ mang đến cơ hội làm quen với 2 khái niệm mới
    - Sử dụng lifecycle hook
    - Viết hook của riêng bạn

## Lifecycles in a World of Hooks

- Tính năng phát lại trong chương 3 sử dụng 2 phương thức của lifecycle của class Excel `componentDidMount` và `componentWillUnMount`

### Troubles with Lifecycle Methods

- Xem lại ví dụ bên dưới, bạn có thể thấy rằng mỗi phương thức này có 2 nhiệm vụ, không liên quan đến nhau
    
    ```jsx
    componentDidMount() {
      document.addEventListener('keydown', this.keydownHandler);
      fetch('https://www...')
        .then(/*...*/)
        .then((initialData) => {
          /*...*/
          this.setState({ data });
        });
    }
    
    componentWillUnmount() {
      document.removeEventListener('keydown', this.keydownHandler);
      clearInterval(this.replayID);
    }
    ```
    
- Trong `componentDidMount()` bạn thiết lập 1 event listener `keydown` để khởi động phát lại cũng như lấy dữ liệu từ serve
- Trong `componentWillUnMount()` bạn xoá event listener `keydown` và cũng clean ID `setInterval()` . Điều này minh hoạ cho 2 vấn đề liên quan đến việc sử dụng các lifecycle method của các class component (được giải quyết khi sử dụng hook)
- **Các nhiệm vụ không liên quan được thực hiện cùng nhau**
    - Ví dụ, thực hiện lấy dữ liệu và thiết lập event listener ở một nơi. Điều này khiến các lifecycle method dài hơn trong khi thực hiện các nhiệm vụ không liên quan. Trong các component đơn giản, điều này ổn, nhưng trong các component lớn hơn, bạn cần phải sử dụng comment code hoặc di chuyển các phần code đến các function khác, để bạn có thể tách các nhiệm vụ không liên quan và làm cho code dễ đọc hơn
- **Các nhiệm vụ liên quan được phân tán**
    - Ví dụ, hãy xem việc thêm và xoá cùng 1 event listener. Khi các lifecycle method trở nên lớn hơn, việc xem xét các phần riêng biệt của cùng một mối quan tâm một cách tổng thể trở nên khó khăn hơn vì chúng đơn giản là không phù hợp với cùng một màn hình code khi bạn đọc lại sau này

### useEffect()

- Hook được tích hợp sẵn, thay thế cho cả 2 lifecycle method trên là `React.useEffect()`
- Từ `effect` (hiệu ứng) viết tắt của `side effect` (hiệu ứng phụ) nghĩa là 1 loại công việc không liên quan đến nhiệm vụ chính nhưng xảy ra cùng lúc. Nhiệm vụ chính của component React là hiển thị 1 cái gì đó dựa trên state và props. Nhưng hiển thị cùng lúc (trong cùng 1 hàm) cùng với 1 số công việc phụ (chẳng hạn như lấy data từ server hoặc thiết lập event listener) có thể là cần thiết
- Trong component `Excel` , ví dụ, thiết lập 1 event listener `keydown` là 1 side effect của nhiệm vụ chính là hiển thị dữ liệu trong table
- Hook `useEffect()` nhận 2 đối số
    - Một callback function được gọi vào thời điểm thích hợp
    - 1 dependency tuỳ chọn
- List dependencies sẽ được kiểm tra trước khi callback function được gọi và quyết định xem callback function đó có nên được gọi không
    - Nếu các giá trị của các biến dependencies không thay đổi, không cần gọi lại callback function
    - Nếu list dependencies là mảng trống, hàm gọi lại sẽ chỉ gọi 1 lần, tương tự như `componentDidMount`
    - Nếu các dependencies bị bỏ qua, callback function được gọi lại trong mỗi lần hiển thị lại
    
    ```jsx
    useEffect(() => {
      // Chỉ ghi nhật ký nếu `data` hoặc `headers` thay đổi
      console.log(Date.now());
    }, [data, headers]);
    
    useEffect(() => {
      // Ghi nhật ký một lần, sau khi hiển thị ban đầu, giống như `componentDidMount()`
      console.log(Date.now());
    }, []);
    
    useEffect(() => {
      // Được gọi trong mỗi lần hiển thị lại
      console.log(Date.now());
    }, /* không có phụ thuộc nào ở đây */);
    ```
    

### useLayoutEffect()

- Để kết thúc cuộc thảo luận về `useEffect()` , hãy xem 1 hook khác được tích hợp sẵn có tên là `useLayoutEffect()`
- Chỉ có 1 vài hook được tích hợp sẵn, vì vậy đừng lo lắng về việc phải ghi nhớ một danh sách các API mới
- `useLayoutEffect()` hoạt động giống như `useEffect()` , sự khác biệt duy nhất là nó được gọi trước khi React hoàn thành việc vẽ tất cả các node DOM của 1 lần hiển thị. Nói chung, bạn nên sử dụng `useEffect()` trừ khi bạn cần đo lường một cái gì đó trên trang (có thể là kích thước của 1 component đã được hiển thị hoặc vị trí cuộn sau khi cập nhật) và sau đó hiển thị lại dựa trên thông tin này. Khi không có gì cần thiết, `useEffect()` tốt hơn vì nó là bất đồng bộ và cũng cho người đọc code của bạn biết rằng các thay đổi DOM không liên quan đến component của bạn
- Bởi vì `useLayoutEffect()` được gọi sớm hơn, bạn có thể tính toán lại và hiển thị lại và người dùng chỉ nhìn thấy lần hiển thị cuối cùng. Nếu không, họ sẽ thấy lần hiển thị ban đầu trước, sau đó là lần hiển thị thứ 2. Tuỳ thuộc vào mức độ phức tạp của việc sử dụng bố cục, người dùng có thể nhận thấy sự nhấp nháy giữa 2 lần hiển thị
- Ví dụ hiển thị 1 bảng dài với độ rộng ô ngẫu nhiên. Sau đó, độ rộng của bảng được đặt trong 1 effect hook
    
    ```jsx
    function Example({ layout }) {
      if (layout === null) {
        return null;
      }
      if (layout) {
        useLayoutEffect(() => {
          const table = document.getElementsByTagName('table')[0];
          console.log(table.offsetWidth);
          table.width = '250px';
        }, []);
      } else {
        useEffect(() => {
          const table = document.getElementsByTagName('table')[0];
          console.log(table.offsetWidth);
          table.width = '250px';
        }, []);
      }
      return (
        <table>
          <thead>
            <tr>
              <th>Random</th>
            </tr>
          </thead>
          <tbody>
            {Array.from(Array(10000)).map((_, idx) => (
              <tr key={idx}>
                <td width={Math.random() * 800}>{Math.random()}</td>
              </tr>
            ))}
          </tbody>
        </table>
      );
    }
    
    function ExampleParent() {
      const [layout, setLayout] = useState(null);
      return (
        <div>
          <button onClick={() => setLayout(false)}>useEffect</button>{' '}
          <button onClick={() => setLayout(true)}>useLayoutEffect</button>{' '}
          <button onClick={() => setLayout(null)}>clear</button>
          <Example layout={layout} />
        </div>
      );
    }
    ```
    
- Tuỳ thuộc vào việc bạn kích hoạt đường dẫn `useEffect()` hay `useLayoutEffect()`, bạn có thể thấy sự nhấp nháy khi bảng được thay đổi kích thước từ giá trị ngẫn nhiên của nó (khoảng 600px) đến 250px được fix cứng
- Lưu ý rằng trong cả 2 trường hợp, bạn có thể lấy được hình học của bảng (table.offsetWidth), vì vậy nếu bạn chỉ cần thông tin này cho mục đích thông tin và bạn không định hiển thị lại, `useEffect()` bất đồng bộ sẽ tốn hơn. `useLayoutEffect()` nên được dành riêng để tránh nhấp nháy trong các trường hợp bạn cần hành động (hiển thị lại) dựa trên một cái gì đó bạn đo lường, ví dụ, định vị một component tooltip đẹp dựa trên kích thước của phần tử mà nó đang trỏ đến
- **Tóm lại, `useLayoutEffect()` là “công cụ” để “điều chỉnh” effect trong lifecycle function component khi bạn cần “effect” phức tạp liên quan đến DOM**

## A Custom Hook

- Hãy quay lại Excel và xem cách thực hiện tính năng phát lại. Trong trường hợp của các class component, cần phải tạo 1 hàm logSetState() và sau đó thay thế tất cả các cuộc gọi this.setState() bằng this.logSetState. Với các function component, bạn có thể thay thế tất cả các cuộc gọi đến hook `useState()` bằng `useLoggedState()` . Điều này thuận tiện hơn 1 chút vì chỉ có một vài cuộc gọi (cho phần trạng thái độc lập) và tất cả chug đều ở đầu hàm
    
    ```jsx
    // trước
    function Excel({ headers, initialData }) {
      const [data, setData] = useState(initialData);
      const [edit, setEdit] = useState(null);
      // ... v.v.
    }
    
    // sau
    function Excel({ headers, initialData }) {
      const [data, setData] = useLoggedState(initialData, true);
      const [edit, setEdit] = useLoggedState(null);
      // ... v.v.
    }
    ```
    
- Không có hook `useLoggedState()` nào được tích hợp sẵn, nhưng không sao. Bạn có thể tạo hook tuỳ chỉnh của riêng mình. Giống như các hook được tích hợp sẵn, một custom hook chỉ là 1 hàm bắt đầu bằng `use*()`
    
    ```jsx
    function useLoggedState(initialValue, isData) {
      // ...
    }
    ```
    
- Chữ ký của hook có thể là bất cứ thứ gì bạn muốn. Trong trường hợp này, có thêm đối số `isData` . Mục đích của nó là để giúp phân biệt state của data so với state không phải data. Trong ví dụ class component từ Chương 3, tất cả state là một object duy nhất, nhưng ở đây có nhiều phần state. Trong tính năng replay, mục tiêu chính là hiển thị các thay đổi data và sau đó hiển thị rằng tất cả thông tin hỗ trợ (sắp xếp, giảm dần,…) là thứ không quan trọng. Vì replay được update mỗi giây, sẽ không vui khi xem dữ liệu hỗ trợ thay đổi riêng lẻ; phát lại sẽ quá chậm. Vì vậy, hãy có một log chính (mảng dataLog) và một log phụ (mảng auxLog). Ngoài ra, thật hữu ích khi bao gồm môt flag cho biết liệu thay đổi state có phải do tương tác của người dùng hay (tự động) trong khi replay
    
    ```jsx
    let dataLog = [];
    let auxLog = [];
    let isReplaying = false;
    ```
    
- Mục tiêu của custom hook là không can thiệp vào các update state thông thường, vì vậy nó uỷ thác trách nhiệm này cho `useState` ban đầu. Mục tiêu là ghi state log cùng với 1 tham chiếu đến function biết cập nhật state này trong khi replay
- Function sẽ trông như thế này
    
    ```jsx
    function useLoggedState(initialValue, isData) {
      const [state, setState] = useState(initialValue);
      // thực hiện ở đây...
      return [state, setState];
    }
    ```
    
- Đoạn code trên đang sử dụng `useState` mặc định. Nhưng bây giờ bạn co các tham chiếu đến một phần state và phương tiện để update nó. Bạn cần ghi log điều đó. Hãy tận dụng hook `useEffect()` ở đây
    
    ```jsx
    function useLoggedState(initialValue, isData) {
      const [state, setState] = useState(initialValue);
      useEffect(() => {
        // todo
      }, [state]);
      return [state, setState];
    }
    ```
    
- Phương thức này đảm bảo rằng việc ghi log chỉ xảy ra khi giá trị của state thay đổi. Function `useLoggedState()` có thể được gọi một số lần trong các lần hiển thị khác nhau, nhưng bạn có thể bỏ qua các cuộc gọi này trừ khi chung liên quan đến thay đổi trong một phần trạng thái thú vị
- Trong callback function của useEffect() bạn:
    - Không làm gì nếu người dùng đang phát lại
    - Ghi log mọi thay đổi đối với data state vào `dataLog`
    - Ghi log mọi thay đổi đổi đối với dữ liệu hỗ trợ vào `axLog`, được lập index bởi thay đổi liên quan trong data
    
    ```jsx
    function useLoggedState(initialValue, isData) {
      const [state, setState] = useState(initialValue);
      useEffect(() => {
        // todo
      }, [state]);
      return [state, setState];
    }
    ```
    
- Tại sao custom hook tồn tại? Chúng giúp bạn tách biệt và đóng gói gọn gàng một phần logic được sử dụng trong 1 component và thường được chia sẻ giữa các component. `useLoggedState()`  custom ở trên có thể được đưa vào bất kỳ component nào co thể được hưởng lợi từ việc ghi state log của nó. Ngoài ra, custom hook có thể gọi các hook khác, điều mà các hàm thông thường (không phải hook và không phải component) không thể thực hiện được

## Wrapping up the Replay

- Bây giờ bạn đã có 1 custom hook ghi lại các thay đổi với các phần state khác nhau, đã đến lúc kết nối tính năng replay
- Function `replay()` không phải là một khía cạnh thú vị trong cuộc thảo luận về React, nhưng nó thiết lập 1 ID khoảng thời gian. Bạn cần ID đó để dọn dẹp khoảng thời gian trong trường hợp Excel bị xoá khỏi DOM trong khi replay. Trong replay, các thay đổi data được replay mỗi giây, trong khi các thay đổi phụ được thực hiện cùng 1 lúc
    
    ```jsx
    function replay() {
      isReplaying = true;
      let idx = 0;
      replayID = setInterval(() => {
        const [data, fn] = dataLog[idx];
        fn(data);
        auxLog[idx] &&
          auxLog[idx].forEach((log) => {
            const [data, fn] = log;
            fn(data);
          });
        idx++;
        if (idx > dataLog.length - 1) {
          isReplaying = false;
          clearInterval(replayID);
          return;
        }
      }, 1000);
    }
    ```
    
- Phần kết nối cuối cùng là thiết lập 1 effect hook. Sau khi Excel hiển thị, hook sẽ chịu trách nhiệm thiết lập các trình nghe theo dõi kết hợp cụ thể các phím để bắt đầu replay. Đây cũng là nơi để clean sau khi component bị huỷ
    
    ```jsx
    useEffect(() => {
      function keydownHandler(e) {
        if (e.altKey && e.shiftKey && e.keyCode === 82) {
          // ALT+SHIFT+R(eplay)
          replay();
        }
      }
      document.addEventListener('keydown', keydownHandler);
      return () => {
        document.removeEventListener('keydown', keydownHandler);
        clearInterval(replayID);
        dataLog = [];
        auxLog = [];
      };
    }, []);
    ```
