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