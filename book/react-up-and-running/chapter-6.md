# Chapter 6: Setting Up for App Development
- Giờ các bạn đã biết rất nhiều về React, JSX và quản lý state trong cả component dựa trên class và function, đã đến lúc chuyển sang tạo và triển khai 1 ứng dụng thực tế
- Chương 7 sẽ bắt đầu quá trình này nhưng có một vài yêu cầu bạn cần phải lo trước
- Đối với bất kỳ phát triển và triển khai nghiêm túc nào bên ngoài mẫu hoặc thử nghiệm JSX, bạn cần thiết lập 1 môi trường build. Các mục tiêu là sử dụng JSX và bất kỳ Js hiện đại nào khác mà không phải đợi trình duyệt triển khai chúng. Bạn cần thiết lập một chuyển đổi chạy trong nền khi bạn đang code
- Quá trình chuyển đổi sẽ tạo ra mã càng gần với mã mà người dùng cuối của bạn sẽ chạy trên trang web trực tiếp càng tốt (có nghĩa là không cần chuyển đổi phía máy khách nữa). Quy trình cũng nên gây càng ít khó chịu càng tốt để bạn không còn cần phải chuyển giữa môi trường phát triển và build. Cộng đồng và hệ sinh thái Js cung cấp rất nhiều tuỳ chọn khi nói đến quy trình phát triển và build
- Một trong những cách tiếp cận dễ nhất và phổ biến nhất là sử dụng tiện ích `Create React App (CRA)` , vì vậy, chúng ta hãy bắt đầu với nó

## Create React App

- CRA là một tập hợp các script Node.js và dependency của chúng, giúp bạn gỡ bỏ gánh nặng thiết lập mọi thứ bạn cần để bắt đầu

### Node.js

- Để cài đặt node, hãy truy cập vào trang chủ và cài nó xuống cho hệ điều hành của mình. Làm theo hướng dẫn cài đặt và thế là xong. Bây giờ bạn có thể tận dụng các dịch vụ được cung cấp bởi tiện ích dòng lệnh `Node Package Manager (npm)` .
- Ngay cả khi bạn cài đặt Node, bạn phải đảm bảo nó là phiên bản mới nhất. Để xác minh, hãy nhập vào terminal của bạn
    
    ```jsx
    $ npm --version
    ```
    
- Nếu bạn không có kinh nghiệm sử dụng terminal, đây là thời điểm tuyệt vời để bạn sử dụng

### Hello CRA

- Bạn có thể cài đặt CRA và có sẵn cục bộ cho các dự án trong tương lai. Nhưng điều đó có nghĩa là cập nhật nó thường xuyên. Một cách tiếp cận thậm chí còn thuận tiện hơn là sử dụng `npx` đi kèm với NodeJs. Nó cho phép bạn thực thi các script gói Node. Bạn có thể chạy script CRA một lần: Nó tải xuống và thực thi phiên bản mới nhất, thiết lập ứng dụng của bạn và nó biến mất. Lần sau, khi bạn cần bắt đầu 1 dự án khác, bạn chạy lại nó mà không cần lo về bản cập nhật
- Để bắt đầu, hãy tạo 1 thư mục tạm thời và thực thi CRA
    
    ```jsx
    $ mkdir ~/reactbook/test
    $ cd ~/reactbook/test
    $ npx create-react-app hello
    ```
    
- Hãy dành cho nó 1-2 phút để hoàn thành quá trình và bạn sẽ nhận được thông báo thành công
    
    ```jsx
    Success! Created hello at /[...snip...]/reactbook/hello
    ```
    
- Bên trong thư mục đó, bạn có thể chạy một số lệnh
    
    ```jsx
     npm start
     Khởi động máy chủ phát triển.
    npm run build
     Gói ứng dụng thành các tệp tĩnh để sản xuất.
     npm test
     Khởi động trình chạy thử nghiệm.
     npm run eject
     Xóa công cụ này và sao chép các phụ thuộc build, tệp cấu hình
     và script vào thư mục ứng dụng. Nếu bạn làm điều này, bạn không thể quay lại!
    We suggest that you begin by typing:
     cd hello
     npm start
    Happy hacking!
    ```
    
- Như trên màn hình hiển thị, hãy chạy
    
    ```jsx
    $ cd hello
    $ npm start
    ```
    
- Thao tác này sẽ mở trình duyệt của bạn và trỏ nó đến http://localhost:3000/ nơi bạn có thể thấy một ứng dụng React đang hoạt động.
- Bây giờ bạn có thể mở ~/reactbook/test/hello/src/App.js và thực hiện một thay đổi nhỏ. Ngay sau khi bạn lưu các thay đổi, trình duyệt sẽ cập nhật với các thay đổi mới.
### Build and Deploy

- Giả sử bạn đã hài lòng với ứng dụng của bạn và sẵn sàng tung ứng dụng ra thế giới. Hãy dừng ứng dụng của bạn lại và hãy nhập vào terminal
    
    ```jsx
    $ npm run build
    ```
    
- Đây là quá trình build và đóng gói ứng dụng, sẵn sàng để được triển khai - nó sẽ tạo ra 1 thư mục `build`
- Sao chép nội dung vào server - ngay cả dịch vụ lưu trữ dùng chung đơn giản cũng được - và bạn đã sẵn sàng để công bố ứng dụng mới
- Khi bạn muốn thay đổi và lặp lại quy trình
    
    ```jsx
    $ npm start
    // làm việc, làm việc, làm việc ...
    // Ctrl + C
    $ npm run build
    ```
    

### Mistakes Were Made

- Khi bạn lưu 1 file có lỗi trong đó, (có thể bạn quên đóng thẻ JSX) quá trình build đang diễn ra sẽ thất bại và bạn sẽ nhận được 1 thông báo lỗi cả console và browser
- Thật tuyệt vời, bạn nhận được phản hồi ngay lập tức. Trích dẫn John C.Maxwell, “Thất bại sớm, thất bại thường xuyên, nhưng luôn thất bại về phía trước”

### package.json and node_modules

- File `package.json` được tìm thấy trong thư mục gốc của ứng dụng chứa các cấu hình khác nhau cho ứng dụng (CRA có tài liệu mở rộng). Một trong những phần liên quan đến phụ thuộc, chẳng hạn như React và React-DOM. Các phụ thuộc này đặt trong `node_modules` và thư mục gốc của ứng dụng. Các phụ thuộc ở đó là để phát triển và buil ứng dụng chứ không để triển khai. Và chúng không nên được bao gồm nếu bạn chia sẻ code ứng dụng của mình với người khác. Ví dụ nếu bạn chia sẻ ứng dụng này lên github, bạn sẽ không đính kèm `node_modules`
- Khi người khác muốn đóng góp hoặc bạn muốn đóng góp cho 1 ứng dụng khác, bạn cài đặt các phụ thuộc cục bộ
- Hãy thử điều này, xoá thư mục `node_modules` và sau đó chạy
    
    ```jsx
    npm i
    ```
    
- Bằng cách này, tất cả các phụ thuộc được liên kết trong package.json của bạn (và các phụ thuộc của chúng) được cài đặt trong thư mục `node_modules` mới được tạo

## Poking Around the Code

- Hãy cùng xem xét code được tạo bởi CRA và lưu ý một số chi tiết cụ thể liên quan đến các điểm nhập của ứng dụng (index.html và index.js) và cách xử lý các phụ thuộc Js và Css của nó

### Indices

- Trong `public/html` bạn sẽ thấy trang index html kiểu cũ, là gốc của mọi thứ được hiển thị bởi trình duyệt. Đây là nơi `<div id="root">` được định nghĩa và nơi React sẽ hiển thị component cấp cao nhất của bạn và các phần tử con của nó. Tệp `src/index.js` là mục nhập chính cho ứng dụng theo quan điểm của React
- Lưu ý phần trên cùng
    
    ```jsx
    import React from 'react';
    import ReactDOM from 'react-dom';
    import './index.css';
    import App from './App';
    ```
    

### JavaScript: Modernized

- Các ví dụ trong sách hiện cho đến nay chỉ hoạt động với các component đơn giản và đảm bảo React và React DOM có sẵn dưới dạng biến toàn cục. Khi bạn chuyển sang các ứng dụng phức tạp hơn với component, bạn cần một kế hoạch để tổ chức tốt hơn. Việc “rải” các biến toàn cục là nguy hiểm (chúng có xu hướng gây ra xung đột tên) và việc dựa vào biến toàn cục luôn có mặt là không chắc chắn.
- Bạn cần các module. Module chia nhỏ các phần chức năng khác nhau tạo nên ứng dụng của bạn thành các file nhỏ, dễ quản lý. Nói chung bạn nên có 1 module riêng biệt cho mỗi mối quan tâm; module và các mối quan tâm có mối quan hệ 1-1.
- Một số module có thể là các component React riêng lẻ; một số có thể chỉ đơn giản là các tiện ích liên quan hoặc không liên quan đến React - ví dụ: một reducer, một hook tuỳ chỉnh hoặc 1 thư viện xử lý định dạng ngày tháng hoặc tiền tệ
- Mẫu chung dành cho 1 module là: Khai báo các yêu cầu ở trên cùng, xuất ở dưới cùng triển khai “phần thịt” ở giữa. Nói cách khác 3 nhiệm vụ này
    - Yêu cầu/ nhập các phụ thuộc
    - Cung cấp api dưới dạng component/class/object
    - Xuất API
- Đối với component React, mẫu có thể trông như sau
    
    ```jsx
    import React from 'react';
    import MyOtherComponent from './MyOtherComponent';
    
    function MyComponent() {
     return <div>Hello</div>;
    }
    
    export default MyComponent;
    ```
    
- Một lần nữa, một quy ước có thể hữu ích là: **một module xuất 1 component React**
- Bạn có nhận thấy sự khác biệt khi nhập React so với `MyOtherComponent`: `from 'react'` và `from './MyOtherComponent` không?
- Cái sau là đường dẫn thư muc - bạn đang yêu cầu module kéo phụ thuộc từ 1 vị trí tệp tương đối so với module, trong khi cái trước đang kéo phụ thuộc từ một nơi được chia sẻ (node_modules)

### CSS

- Trong `src/index.js` bạn có thể thấy cách Css được coi như một module khác
    
    ```jsx
    import './index.css';
    ```
    
- `src/index.css` nên chứa các kiểu khung. chẳng hạn như body, html,… áp dụng cho toàn bộ trang. Ngoài các kiểu trong toàn ứng dụng, bạn cần các kiểu cụ thể cho từng component. Theo quy ước, một file Css (và 1 file Js) cho mỗi component React, bạn nên có `MyComponent.css` chứa các kiểu chỉ liên quan đến `MyComponent.js` và không có gì khác. Cũng nên thêm tiền tố cho tất cả các tên class được sử dụng trong `MyComponent.js` bằng `MyComponent-`
    
    ```jsx
    .MyComponent-table {
     border: 1px solid black;
    }
    
    .MyComponent-table-heading {
     border: 1px solid black;
    }
    ```
    
- Mặc dù có nhiều cách khác để tạo Css, nhưng hãy giữ cho nó đơn giản và “kiểu cũ”: bất cứ thứ gì sẽ chỉ chạy trong trình duyệt mà không cần bất kỳ chuyển đổi nào

## Moving On

- Bây giờ, bạn đã có một ví dụ về quy trình viết, build và triển khai đơn giản. Với tất cả những điều này phía sau bạn, đã đến lúc chuyển sang các chủ đề thú vị hơn
- Build và thử nghiệm 1 ứng dụng thực tế trong khi tận dụng nhiều tính năng mà Js hiện đại cung cấp
