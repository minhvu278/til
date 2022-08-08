# Các khái niệm chính
- Ví dụ đơn giản hiển thị `Hello World` ra màn hình
    ```js 
    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<h1>Hello, world!</h1>);
    ```
# JSX 
- Cú pháp JSX 
    ```js 
    const element = <h1>Hello, world!</h1>;
    ```
    - Nhìn thì có vẻ khá là giống khai báo chuỗi hay HTML - Nma nó là cú pháp của JSX
    - Nó là phần mở rộng cú pháp cho JS
## Lý do nên sử dụng JSX
    - Logic hiện thị kết hợp với giao diện của người dùng: Cách các sự kiện được xử lý, trạng thái thay đổi theo thời gian 
    - Thay vì phải tách các logic ra các file riêng, react sẽ chia thành các `component` chứa logic của cả 2 
    - React không yêu cầu sử dụng JSX - Tuy nhiên thì nó rất hữu ích khi làm việc với giao diện người dùng bên trong code JS
    - Nó cũng cho phép React hiển thị các warning & error hữu ích hơn
## Nhúng biểu thức vào trong JSX
- Sử dụng biến trong JSX thì cần đặt trong `{}` 
    ```js 
    const name = 'Vu Do';
    const element = <h1>Hello, {name}</h1>;
    ```
- Có thể sử dụng bất kì biểu thức JS hợp lệ nào bên trong `{}`