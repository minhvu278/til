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
