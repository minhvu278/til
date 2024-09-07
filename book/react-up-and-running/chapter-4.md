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