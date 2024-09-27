# Building the App’s Components
- Bây giờ bạn đã biết tất cả các kiến thức cơ bản về việc tạo các custom component React (và sử dụng các component tích hợp sẵn), sử dụng JSX để xác định giao diện người dùng và sử dụng create-react-app để build và triển khai kết quả, đã đến lúc xây dựng 1 ứng dụng hoàn chỉnh hơn
- Ứng dụng được gọi là “Whinepad” và nó cho phép người dùng ghi chú và xếp hạng các loại rượu mà họ đang thử. Nó không nhất thiết phải là rượu vang; nó có thể là bất cứ thứ gì họ muốn “phàn nàn”. Nó nên làm tất cả những gì bạn mong đợi từ một ứng dụng tạo, đọc, cập nhật và xoá. Nó cũng nên là 1 ứng dụng phía client, lưu trữ dữ liệu trên máy client
- Mục tiêu là tìm hiểu React, vì vậy các phần không phải React (server, CSS) được giữ ở mức tối thiểu
- Khi xây dựng 1 ứng dụng, bạn nên bắt đầu với các component nhỏ, có thể tái sử dụng và kết hợp chúng để tạo thành 1 tổng thể. Các component này càng độc lập và có thể tái sử dụng càng tốt. Chương này sẽ tập chung vào tạo các component, từng cái một và chương sau sẽ kết hợp chúng lại với nhau

## Setup

- Đầu tiên, khởi tạo và bắt đầu ứng dụng CRA mới
    
    ```jsx
    $ cd ~/reactbook/
    $ npx create-react-app whinepad
    $ cd whinepad
    $ npm start
    ```
    

## Start Coding

- Bây giờ, vì mục đích tổ chức, chung ta hãy giữ tất cả các component React và CSS tương ứng của chúng bên trong 1 thư mục mới `whinepad/src/components`. Bất kỳ code nào khác không phải component, như các tiện ích khác nhau mà bạn có thể cần, có thể nằm trong `whinepad/src/module`. Thư mục gốc src chứa tất cả các file do CRA tạo ra
- Bạn có thể thay đổi chúng, tất nhiên, nhưng bất kỳ code mới nào sẽ nằm trong 1 trong 2 thư mục mới `components` hoặc `modules`
    
    ```jsx
    whinepad/
    ├── public/
    │ ├── index.html
    └── src/
     ├── App.css // do CRA tạo
     ├── App.js // do CRA tạo
     ├── ...
     └── components/ // tất cả các component nằm ở đây
     │ ├── Excel.js
     │ ├── Excel.css
     │ ├── ...
     │ └── ...
     └── modules/ // các module JS trợ giúp ở đây
     ├── clone.js
     ├── ...
     └── ...
    ```
    

## Refactoring the Excel Component

- Hãy bắt đầu Whinepad. Đó là nơi 1 ứng dụng xếp hạng nơi bạn note. Vậy làm thế nào về việc để màn hình welcome là danh sách nhữnng thứ bạn đã xếp hạng trong 1 bảng đẹp? Điều này có nghĩa là tái sử dụng component `<Excel>` từ chương 4.
- Copy và paste vào `components/Excel.js` . Excel bây giờ có thể là một component độc lập, có thể tái sử dụng, không biết gì về nơi dữ liệu đến từ đâu và cách nội dung được chèn vào HTML. Nó chỉ là 1 component trong React, một trong những block xây dựng của app
- Và bạn đã biết rằng 1 components có thể sử dụng được có 3 nhiệm vụ
    - Nhập các phụ thuộc
    - Làm công việc
    - Xuất component
- Bỏ qua phần phụ thuộc trong 1 phút, bây giờ Excel có thể trông như thế này
    
    ```jsx
    // các phụ thuộc nằm ở đây
    // làm công việc
    function Excel({headers, initialData}) {
     // giống như trước
    }
    // xuất
    export default Excel;
    ```
    
- Quay lại các phụ thuộc. Trước đây, khi xử lý HTML thuần, React là một biến toàn cục và PropTypes cũng vậy. Bây giờ bạn import chúng
    
    ```jsx
    import React from 'react';
    import PropTypes from 'prop-types';
    ```
    
- Bây giờ bạn có thể sử dụng state hook thông qua `React.useState()`. Tuy nhiên, thường thuận tiện khi gán 1 số thuộc tính React bằng cách sử dụng cú phép import co tên
    
    ```jsx
    import {useState, useReducer} from 'react';
    ```
    
- Và bây giờ bạn có thể sử dụng state hook với `useState()` ngắn hơn
- Cuối cùng, hãy chuyển trình trợ giúp nhân bản object vào module của riêng nó, vì nó không thực sự là công việc của Excel và việc di chuyển nó sẽ giúp dễ dàng thay thế việc triển khai “nhanh chóng và bẩn” bằng một thư viện thích hợp vào bất kỳ lúc nào sau này
- Điều này có nghĩa là import 1 module `clone` mới từ Excel
    
    ```jsx
    import clone from '../modules/clone.js';
    ```
    
- Việc triển khai modue clone nằm trong thư mục modules, nơi được thiết kết cho các module. Nói cáckhác, đó là 1 file Js không có phụ thuộc nào
    
    ```jsx
    function clone(o) {
     return JSON.parse(JSON.stringify(o));
    }
    
    export default clone;
    ```
    
- **Lưu ý**: Khi import file js, bạn có thể bỏ qua `.js`
- Bạn có thể sử dụng
    
    ```jsx
    import clone from '../modules/clone';
    ```
    
- Thay vì
    
    ```jsx
    import clone from '../modules/clone.js';
    ```
    
- Và vì vậy Excel mới trông như sau
  ```js
  import {useState, useReducer} from 'react';
  import PropTypes from 'prop-types';
  import clone from '../modules/clone';

  // làm công việc
  function Excel({headers, initialData}) {
  // giống như trước
  }

  // xuất
  export default Excel;
  ```

## Version 0.0.1 of the New App
- Bây giờ bạn đã có một component có thể tái sử dụng độc lập. Vì vậy hãy sử dụng nó. File `App.js` được tạo bởi CRA là component cấp cao nhất cho ứng dụng và bạn có thể nhập Excel ở đó
- Xoá code do CRA tạo và thay thế bằng Excel và một số dữ liệu tạm thời, bạn sẽ nhận được
    
    ```jsx
    import './App.css';
    import Excel from './components/Excel';
    
    function App() {
     return (
     <div>
     <Excel
     headers={['Tên', 'Năm']}
     initialData={[
     ['Charles', '1859'],
     ['Antoine', '1943'],
     ]}
     />
     </div>
     );
    }
    
    export default App;
    ```
    
- Với điều này, bạn có 1 ứng dụng đang hoạt động. Nó khá khiêm tốn nhưng nó vẫn có thể tìm kiếm và chỉnh sửa dữ liệu

## CSS

- Như đã thảo luận trong chương 6, hãy có 1 file CSS cho mỗi component. Vì vậy, component `Excel.js` nên đi kèm (nếu cần) với `Excel.css`. Bất kỳ tên class nào trong `Excel.js` phải có tiền tố là `Excel-`.
- Trong triển khai hiện đại từ chương 4, các phần tử được tạo kiểu bằng cách sử dụng bộ chọn HTML (vd `table th {...}`), nhưng trong 1 ứng dụng thực tế bao gồm các phần tử có thể tái sử dụng, các kiểu nên được giới hạn trong các component để chúng không can thiệp vào các component khác
- Lưu ý có rất nhiều tuỳ chọn khi nói đến việc tạo kiểu cho ứng dụng của bạn. Nhưng vì mục đích của cuộc thảo lluận này, chúng ta hãy tập chung vào các phần React. Một quy ước đặt tên CSS đơn giản sẽ thực hiện được mánh khoé này
- Bất kỳ kiểu “global” nào cũng có thể nằm trong `App.css` do CRA tạo, nhưng những kiểu này nên được giới hạn trong 1 tập hợp nhỏ các kiểu thực sự chung chung, ví dụ như phông chữ cho toàn bộ ứng dụng. CRA cũng tạo ra một `index.css` nhưng để tránh nhầm lẫn về kiểu global nào đi đâu, chúng ta hãy xoá no
- Vì vậy div cao nhất mà Excel hiển thị trở thành
    
    ```jsx
    return (
     <div className="Excel">
     {/* mọi thứ khác */}
     <div>
    );
    ```
    
- Bây giờ bạn có thể giới hạn phạm vi các kiểu chỉ áp dụng cho component này bằng cách sử dụng tiền tố Excel
    
    ```jsx
    .Excel table {
     width: 100%;
    }
    
    .Excel td {
     /* etc. */
    }
    
    .Excel th {
     /* etc. */
    }
    ```
## Local Storage

- Để giới hạn cuộc thảo luận ở React càng nhiều càng tốt, chúng ta hãy giữ tất cả dữ liệu trong trình duyệt và không lo lắng về các phần phía máy chủ
- Nhưng thay vì mã hoá cứng dữ liệu trong ứng dụng, hãy sử dụng localStorage. Nếu bộ nhớ trống, một mặc định sẽ đủ để gợi ý cho người dùng về mục đích cùa ứng dụng. Việc truy xuất dữ liệu có thể xảy ra trong `App.js` cấp cao nhất
    
    ```jsx
    const headers = localStorage.getItem('headers');
    const data = localStorage.getItem('data');
    
    if (!headers) {
     headers = ['Tiêu đề', 'Năm', 'Xếp hạng', 'Nhận xét'];
     data = [['Rượu vang đỏ', '2021', '3', 'bình thường']];
    }
    ```
    
- Chúng ta sẽ xoá nút “search” khỏi Excel; nó nên trở thành một phần của component của riêng nó, được tách biệt tốt hơn khỏi component Excel. Và với điều đó, bạn đang trên đường đến một ứng dụng tuyệt vời

## The Components

- Bây giờ bạn đã biết thiết lập đang được hoạt động, đã đến lúc build tất cả các component tạo nên ứng dụng
- Tái sử dụng component Excel là một cách để bắt đầu; tuy nhiên, component này đang làm quá nhiều việc. Tốt hơn là “chia để trị” bằng cách chia nó thành các component nhỏ, có thể tái sử dụng
- Ví dụ các button nên là các component của riêng chúng để chúng có thể được tái sử dụng bên ngoài ngữ cảnh của bảng Excel. Ngoài ra, ứng dụng cần một số component chuyên biệt khác chẳng hạn như widget xếp hạng hiển thị biểu tượng cảm xúc thay vì chỉ là một số, component modal,…
- Mục tiêu của nó là cho phép bạn phát triển và kiểm tra component một cách độc lập. Thường thì sử dụng một component trong một ứng dụng sẽ khiến bạn “gắn kết” component đó với ứng dụng và giảm khả năng tái sử dụng của nó. Việc có component này một cách riêng biệt buộc bạn phải đưa ra quyết định tốt hơn về việc tách biệt rời nó khỏi môi trường; cho các thành viên khác trong nhóm khám phá và tái sử dụng các component hiện có. Khi ứng dụng của bạn phát triển, nhóm cũng vậy
- Để giảm thiểu rủi ro hai người làm việc trên các component giống nhau một cách đáng kinh ngạc và để thúc đẩy việc tái sử dụng component (điều này dẫn đến việc phát triển ứng dụng nhanh hơn), bạn nên đặt tất cả các component vào một nơi cùng với các ví dụ về cách chúng được sử dụng
- Có các công cụ có sẵn cho phép khám phá và thử nghiệm component, nhưng chúng ta đừng giới thiệu một phụ thuộc khác. Thay vào đó, hãy sử dụng phương pháp “tự làm” nhẹ nhàng

## **Discovery (Khám phá)**

- Một công cụ khám phá có thể được triển khai như một component mới cùng tồn tại với ứng dụng. Nhiệm vụ này có thể đơn giản như tạo 1 component mới (src/components/Discovery.js) trong đó, bạn liệt kê các component của mình. Bạn thậm chí có thể hiển thị  cùng một component với các thuộc tính khác nhau để minh hoạ các cách sử dụng khác nhau của một component
    
    ```jsx
    import Excel from './Excel';
    // thêm các nhập khẩu khác ở đây ...
    
    function Discovery() {
     return (
     <div>
     <h2>Excel</h2>
     <Excel
     headers={['Tên', 'Năm']}
     initialData={[
     ['Charles', '1859'],
     ['Antoine', '1943'],
     ]}
     />
     {/* thêm các component khác ở đây */}
     </div>
     );
    }
    
    export default Discovery;
    ```
    
- Bây giờ bạn có thể tải component Discovery thay vì ứng dụng thực, bằng cách sử dụng URL làm điều kiện trong `App.js` của bạn
    
    ```jsx
    const isDiscovery = window.location.pathname.replace(/\//g, '') === 'discovery';
    
    function App() {
     if (isDiscovery) {
     return <Discovery />;
     }
     return (
     <div>
     <Excel headers={headers} initialData={data} />
     </div>
     );
    }
    ```
    
- Bây giờ nếu bạn tải http://localhost:3000/discovery thay vì http://localhost:3000/, bạn có thể thấy tất cả các component mà bạn đã thêm vào Discovery
- Tại thời điểm này, chỉ có một component duy nhất, nhưng trang này sẽ sớm được phát triển. Hãy bắt tay vào làm việc và xây dựng chúng - từng cái một
