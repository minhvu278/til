# useState
- Trạng thái của dữ liệu (VD như đổi từ số 1 sang số 2)
- Giúp đơn giản hóa được việc đơn giản hóa dữ liệu ra giao diện người dùng 
## Vậy khi nào thì sử dụng ? 
- Sử dụng khi muốn dữ liệu thay đổi thì giao diện cũng tự động được cập nhật(render lại dữ liệu)
## Nguyên lý hoạt động của useState
- Khởi tạo 
    ```js
    const [state, setState] = useState(initState)
    ```
    - initState: Là giá trị khởi tạo - Chỉ dùng cho 1 lần trong lần đầu. Sau đó thì nó return ra 1 mảng gồm 2 phần tử 
        - state: Lấy giá trị khởi tạo initState
        - setState: Dùng để xét lại state (Vd state đang là 1 mà muốn chuyển thành 2 thì gọi đến setState và truyền 2 vào thì state sẽ được sửa thành 2)
## VD 
- Tạo ra ứng dụng đếm số 
    ```js 
    import {useState} from "react";

    function App() {
    const [count, setCount] = useState(1)

    const handleIncrease = () => {
        setCount(count + 1)
    }

    return (
        <div className="App">
            <h1>{count}</h1>
            <button onClick={handleIncrease}>Increase</button>
        </div>
    )
    }
    ```
- Logic chạy của đoạn code trên 
    - Giá trị khởi tạo là 1 => count sẽ là 1 -> Tạo ra hàm handleIncrease(Tạo ra chứ chưa chạy)  -> Truyền count vào h1 nên render ra giao diện là 1  -> Khi click vào Increase  -> gọi hàm handleIncrease set count + thêm 1  -> Sau khi set xong nó sẽ gọi lại hàm App() -> Không lấy giá trị khởi tạo nữa mà sẽ lấy setCount ở hàm handle => count lúc này sẽ là 2
- init State
    ```js
    const orders = [100, 200, 300]

    function App() {
    const total = orders.reduce((total, cur) => total + cur)

    const [count, setCount] = useState(total)

    const handleIncrease = () => {
        setCount(count + 1)
    }

    return (
        <div className="App">
            <h1>{count}</h1>
            <button onClick={handleIncrease}>Increase</button>
        </div>
    )
    }
    ```
    - Như này sẽ bị tính lại logic sau mỗi lần re-render
    - Fix
    ```js 
    const [count, setCount] = useState(() => {
        const total = orders.reduce((total, cur) => total + cur)
        console.log(total)
        return total
    })

    const handleIncrease = () => {
        setCount(count + 1)
    }
    ```
    - Lấy giá trị return làm initialState

## **Note nhẹ**
- Component sẽ được re-render sau khi setState 
- Initial state chỉ dùng cho lần đầu 
- Set state với callback 
- Initial state với callback
- Set state là thay thế bằng giá trị mới
    - Chú ý trong trường hợp thêm vào thì cần dùng spread(...) hoặc callback để lưu lại giá trị cũ
        - Sử dụng spread 
        ```js
        const [info, setInfo] = useState({
        name: 'Vu Do',
        age: 24
        })

        const handleUpdate = () => {
            setInfo({
                ...info,
                address: 'HN'
            })
        }
        ```
        - Sử dụng callback
        ```js
        const [info, setInfo] = useState({
        name: 'Vu Do',
        age: 24
        })

        const handleUpdate = () => {
            setInfo(prev => ({
                ...prev,
                address: 'HN'
            }))
        }
        ```