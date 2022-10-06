# SPA & MPA là gì

## SPA - Single-Page Application
- Ứng dụng 1 trang 
- Được cho là cách tiếp cận hiện đại hơn 
- Không cần load lại trang 

## MPA 
- Cách tiếp cận cổ điển hơn 
- Tải lại trang trong quá trình sử dụng (VD như click vào chuyển trang)

## document.createElement() để làm gì 
- Dùng để tạo element 
    ```js
    const h1 = document.createElement('h1')
    h1.innerText = 'Hello bae!'
    ```
- Lý do `root` không có code ở trong mà vẫn render được ra giao diện 
    - Cần get đến các element mà muốn render giao diện. VD: render vào element body
        ```js
        document.body.appendChild(h1)
        ```
- **Tại sao là className mà không phải là class**
    - Vì class sẽ dễ dàng bị trùng với từ khóa class `class {}` vì thế để tránh nhầm thì ta sử dụng class name

- DOM & React 
    - DOM 
        ```js
        const h1DOM = document.createElement('h1')

        h1DOM.title = 'Hello'
        h1.className = 'heading'

        h1.innerText = 'Hello guys!'

        document.body.appendChild(h1DOM)
        ```
    - React 
        ```js
        // React.createElement(type, props, children, n)
        const h1React = React.createElement('h1', {
            title: 'Hello',
            class: 'heading',
        }, 'Hello guys!')
        ```

# Props 
- React element : Là những thẻ JSX giống HTML
- React components : Những function dùng để tạo component thì gọi là component
- Sử dụng props giống như đối số cho function 

    ```js
    // PostItem.js
    function PostItem(props) {
        return (
            <PostItem
               <h1>{props.title}</h1>
                <h1>{props.desc}</h1>
             />
        )
    }

    // App.js
    function App() {
        return (
            <PostItem
                title="React Js"
                desc="Mo ta"
             />
        )
    }
    ```
- Chú ý là cả 2 props element & component thì props `key` là props đặc biệt
- Props cơ bản là đối số của component, function. Props có thể là bất cứ kiểu dữ liệu gì

# Tạo component linh hoạt
- Xử lý event thì sẽ viết ra 1 hàm handle 
- Thường thì trong xử lý logic thì sẽ tách riêng ra 1 hàm handle chứ không xử lý thẳng ở trong props
    ```js
    function CourseItem({course, onClick}) {
        
        return (
            <h2 onClick={onClick}>
                Title
            </h2>
        )
    }

    function App() {
        const handleClick = () {

        }

        return (
            <div>
                {courses.map(course => (
                    <CourseItem 
                        onClick={handleClick}
                    />
                ))}
            </div>
        )
    }
    ```
    - Logic chạy ở đây sẽ là: 
        - Props onClick nó sẽ truyền vào CourseItem -> Truyền vào click của h2
        - Click vào h2 -> gọi đến props `onClick` của CourseItem -> gọi đến hàm xử lý **handleClick** (Bản chất của nó là callback)
- VD xử lý bài toán trong Form có nhiều ô input, checkbox,... Hãy làm cách nào để có thể kế thừa lại 
    - Cách đơn giản:
        ```js
        const Form = {
            Input() {
                return <input />
            },
            Checkbox() {
                return <input type="checkbox">
            }
        }

        function App() {
            return (
                <div>
                    <Form.Checkbox />
                </div>
            )
        }
        ```
    - Phức tạp hơn 1 chút:
         ```js
        const Form = {
            Input() {
                return <input />
            },
            Checkbox() {
                return <input type="checkbox">
            }
        }

        function App() {
            const type = 'Input'

            const Component = Form[type]

            return (
                <div>
                    <Component />
                </div>
            )
        }
        ```

# Props trong JSX 
- Có 2 kiểu truyền qua props 
    - Truyền qua string 
    - Truyền qua expression: Tạo biến ở ngoài truyền vào hoặc truyền array hoặc object vào
        ```js
        <YourComponent 
            propsName1="Vu Do"
            propsName2={expression}
        />
        ```

# Webpack 
- Khi build lên production thì nó sẽ loại bỏ những thứ không cần thiết, gộp vào 1 file để tối ưu được khi build
- Install webpack 
    ```js
    npm install webpack webpack-cli --save-dev
    ```
    - --save-dev là chỉ dùng cho môi trường dev
        - devDependencies chứa các thư viện được cài đặt với flag --save-dev
    - --save là dùng cho tất cả
- Install react & react DOM 
    ```
    npm install react@17.0.2 react-dom@17.0.2 --save
    ```
- Install babel 
    ```
    npm install @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev
    ```
- Để nó load được css thì cần cài thư viện
    ```
    npm install css-loader style-loader --save-dev
    ```

- Cấu trúc của 1 file webpack 
    ```js
    const path = require("path");

    module.exports = {
        entry: "./src/index.js", // Dẫn tới file index.js ta đã tạo
        output: {
            path: path.join(__dirname, "/build"), // Thư mục chứa file được build ra
            filename: "bundle.js" // Tên file được build ra
        },
        module: {
            rules: [
                {
                    test: /\.js$/, // Sẽ sử dụng babel-loader cho những file .js
                    exclude: /node_modules/, // Loại trừ thư mục node_modules
                    use: ["babel-loader"]
                },
                {
                    test: /\.css$/, // Sử dụng style-loader, css-loader cho file .css
                    use: ["style-loader", "css-loader"]
                }
            ]
        },
        // Chứa các plugins sẽ cài đặt trong tương lai
        plugins: [
        ]
    };
    ```
- Tạo file config babel: Cần phải có file `babelrc` thì nó mới hiểu 
    ```js
    {
        "presets": [
            "@babel/preset-env",
            "@babel/preset-react"
        ]
    }
    ```
- Tạo script cho dự án
    - Thường khi chạy project ta chỉ cần chạy `npm start` hoặc `run build`
        ```js
        "start": "webpack --mode development --watch",
        "build": "webpack --mode production" 
        ```
- Tham khảo thêm ở đây 
    ```
    https://fullstack.edu.vn/blog/phan-1-tao-du-an-reactjs-voi-webpack-va-babel.html
    ```

# Create react app 
- Tạo mới 1 project 
    ```
    npx create-react-app `ten project`
    ```

# Phân biệt giữa NPX, NPM, YARN 
- NPM 
    - Cài đặt trong project scope
        - Chỉ tác động trong project 
            ```js
            npm i react react-dom 

            npm uninstall react react-dom 
            ```
    - Cài đặt global scope
        - Cài vào trong 1 thư mục cấp cao hơn cho all project có thể sử dụng được
- NPX 
    - Nó giúp ta không cần cài thư viện ở local mà có thể truy cập được ở ngoài

- YARN & NPM
    - Có thể sử dụng thay thế cho nhau 
    ```
    https://www.youtube.com/watch?v=7sX_8lKURqo&list=PL_-VfJajZj0UXjlKfBwFX73usByw3Ph9Q&index=26&ab_channel=F8Official
    ```

# JSX 
- Viết tắt của Javascript XML(XML là cú pháp mở rộng của HTML) - Sinh ra để hỗ trợ viết XML HTML trong Js
## Tại sao cần sử dụng JSX? 
- Vì cú pháp gần giống với HTML nên viết code sẽ ngắn và dễ hiểu hơn
- Nếu không sử dụng JSX thì hãy xem ví dụ để tạo ra được 1 element
    ```js
    <div id="root"></div>

    <script>
        const ul = ReactElement(
            'ul',
            null,
            React.createElement('li', null, 'Javascript'),
            React.createElement('li', null, 'Reactjs'),
        )
        ReactDOM.render(ul, document.getElementById('root'))
    </script>
    ```
- Vd trên thì ta cũng thấy là để tạo ra được 1 element thì đều phải sử dụng `React.createElement`, vậy thì để code ra 1 trang hoàn chỉnh sử dụng cái này thì sao. Thì đó chính là lý do sử dụng JSX 
- Tuy nhiên thì JSX nó không thể truyền thằng cho ReactDOM được mà nó cần nhận là `ReactElement` vì thế ta cần phải sử dụng 1 thư viện trung gian đó là Babel - Phân tích cú pháp và chuyển đổi về JSX
    - Có thể thử Live Demo tai đây: https://bit.ly/2VOIMN7
- `1 số điều cần lưu ý khi sử dụng JSX`
    - Có thể tạo ra biến và gán JSX cho biến đó
        ```js 
        const ul = <ul>
                        <li>ReactJS</li>
                    </ul>
        ```
    - Hỗ trợ viết code Js đan xen vào giữa
        ```js 
        const reactCourse = 'ReactJS'

        const ul = <ul>
                        <li>{reactCourse}</li>
                    </ul>
        ```
    - JSX không phải là HTML nên cẩn thận kẻo nhầm cú pháp với HTML 
        - Thay vì viết class như bên HTML thì ta sử dụng `className` - Lý do là class trùng với keyword của Js
        ```js
        //HTML
        <div class="container"></div>

        //JSX
        <div className="container"></div>
        ```
## `Tóm lại`: 
- **Jsx có cú pháp gần giống HTML nên code dễ hiểu hơn**
- **Có thể tạo ra biến và gán JSX cho biến đó** 
- **Hỗ trợ viết code Js đan xen vào giữa** 
- **Sử dụng className thay cho class**

# Component
- Là bộ phận cấu thành của giao diện người dùng
## Tại sao cần chia component ?
- Khi viết code thì thường viết hết vào trong 1 file thì nó có 1 số vấn đề: 
    - Code rất dài 
    - Fix bug khó 
    - Không tái sử dụng được
- Thử tưởng tượng code tầm 10 trang đều sử dụng header và footer giống nhau, copy từ file này ném sang file kia - Nó sẽ bị lặp lại code rất nhiều
-  Vì thế nên chia code thành các component: 
    - Cấu trúc code rõ ràng hơn 
    - Tận dụng được tính năng tái sử dụng của component
- Component được viết trong thư mục `components` 
    - Ví dụ viết component Header để có thể tái sử dụng thì cần tạo file header.js trong component (Nhớ phải export thì mới import vào file khác được)
        - header.js
        ```js
        function Header() {
            return (
                <div className="header">Header</div>
            )
        }
        //Export
        export default Header
        ```
        - Import vào file cần sử dụng. Vd file App.js
            ```js 
            import Header from "../components/header";
            import React from "react";

            const App = () => {
                return (
                    <Header></Header>
                    // Đối với những tag không có children thì có thể đóng luôn 
                    <Header />
                )
            }

            export default App
            ```
## `Tóm lại`
- Component sử dụng để cho code rõ ràng hơn
- Tận dụng được tính năng tái sử dụng 
- Được viết trong thư mục `components`
- Đối với những thẻ tag không có children thì có thể đóng luôn: `<Header></Header>  -> <Header />`

# Props
- Là dữ liệu được truyền từ component cha xuống
- Không thể tự động thay đổi được bởi component hiện tại, nếu muốn thay đổi thì thay đổi từ thằng cha - Bản thân component hiện tại thì nó chỉ nhận chứ không thể thay đổi được giá trị của props
- Cùng xem ví dụ để hiểu rõ hơn về props 
    ```js
    function Box(props) {
    return (
        <div style={{backgroundColor: props.color}}>

        </div>
    )
    }

    function App() {
        return (
            <div>
                <Box color="green" />
                <Box color="red" />
            </div>
        )
    }
    ```
    - Trong ví dụ trên thì `color` được truyền từ thằng cha xuống thằng con sẽ không biết trước được nó sẽ nhận được gì và cũng không thể thay đổi được


# State là gì 
- Ngược lại với props thì state có thể thay đổi được
- Có 2 loại state: state và global state (Redux)

## Khi nào cần sử dụng state và global state 
- State
    - Sử dụng cho những dữ liệu mà chỉ sử dụng trong duy nhất 1 component hiện tại 
    - Được tạo ra, quản lý và xử lý trong duy nhất component hiện tại 
- Global state 
    - Sử dụng bởi nhiều component khác nhau 
    - Sử dụng trong Redux(Redux nó là 1 thư viện dùng để quản lý global state)