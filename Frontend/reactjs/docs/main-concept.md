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

# Rending Element 
- 1 phần tử mô tả những gì trên màn hình 
    ```js
    const element = <h1>Hello, world</h1>;
    ```
## Hiển thị 1 phần tử vào DOM 
- Giả sử có thẻ div ở trong HTML 
    ```
    <div id="root"></div>
    ```
    //TODO: Xem ở F8 và note lại
# Components và props
- Cho phép chia giao diện thành các thành phần đôc lập, có thể tái sử dụng lại 
- Về mặt khái niệm thì các thành phần giống với trong Js 
- ..
## Function và class component 
- Cách đơn giản để xác định 1 thành phần là viết 1 hàm JS
    ```js
    function Welcome(props) {
        return <h1>Hello, {props.name}</h1>;
    }
    ```
    - Hàm này là 1 thành phần hợp lệ vì nó chấp nhận 1 props duy nhất(Viết tắt của thuộc tính)
    - Ta gọi các thành phần này là các `function component` vì nó chúng thực sự là các thành phần chức năng bởi vì cơ bản nó là hàm JS 
    - Ta cũng có thể sử dụng class ES6 để xác định 1 thành phần
        ```js
        class Welcome extends React.Component {
        render() {
            return <h1>Hello, {this.props.name}</h1>;
        }
        }
        ```
    - Cả 2 function & class đều tương đương nhau

## Rendering a component 
- Trước đây ta chỉ gặp các phần tử React đại diện cho thẻ DOM 
    ```js
    const element = <div />;
    ```
- Tuy nhiên các phần tử cũng có thể đại diện cho các thành phần do người dùng xác định
    ```js
    const element = <Welcome name="Sara" />;
    ```
- Khi react thấy 1 phần tử đại diện cho 1 người dùng xác định, nó chuyển các thuộc tính JSX và các phần tử con cho các thành phần này như 1 đối tượng duy nhất - Hay còn gọi là props 
    - VD render người dùng tên Sara lên giao diện 
        ```js 
        function Welcome(props) {
            return <h1>Hello, {props.name}</h1>;
            }

            const root = ReactDOM.createRoot(document.getElementById('root'));
            const element = <Welcome name="Sara" />;
            root.render(element);
        ```
        