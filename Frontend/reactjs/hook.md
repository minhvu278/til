# Hook là gì 
- Mang ý nghĩa là gắn, móc vào 
- Là những method, hàm được viết sẵn cung cấp bởi thư viện reactJs
- Chỉ dùng trong function component 
- **Sử dụng hook**
    - Để sử dụng được hook thì ta cần import vào 
        ```js
        import {
            useState,
            useEffect,
            ...
        } from 'react'
# useState
- Là trạng thái của dữ liệu 
    - VD như thay đổi từ `Vu Do` -> `Do Vu` 
- Giúp đơn giản được dữ liệu ra giao diện người dùng (**Dữ liệu thay đổi gì, giao diện thay đổi đó, render lại dữ liệu**)
- ` Lưu ý`: 
    - Component được re-render sau khi `setState`
    - Initial state chỉ dùng được cho lần đầu 
    - Set state với callback 
        - Callback là hàm, nó sẽ trả về giá trị trước đó của state 
            ```js
            function App() {

            const [counter, setCounter] = useState(1)
            // Sử dụng callback: Khi click sẽ tăng lên 2
            const handleIncrease = () => {
                setCounter(prevState => prevState + 1)
                setCounter(prevState => prevState + 1)
            }
            // Khong su dung callback: Vẫn tăng lên 1
            setCounter(counter + 1)
            setCounter(counter + 1)

            return (
                <div className="App">
                <h1>{counter}</h1>
                    <button onClick={handleIncrease}>Increase</button>
                </div>
            );
            ```
            - Callback sẽ lấy giá trị được return để set làm state mới 
    - Initial state với callback 
        - Khi truyền hàm vào, nó sẽ không dùng hàm đó để làm initial state mà dùng giá trị hàm đó return ra để làm initial state
            ```js
            const orders = [100, 200, 300]

            function App() {

            const [counter, setCounter] = useState(() => {
                const total = orders.reduce((total, cur) => total + cur);
                return total
            })

            const handleIncrease = () => {
                setCounter(prevState => prevState + 1)
            }

            return (
                <div className="App">
                <h1>{counter}</h1>
                    <button onClick={handleIncrease}>Increase</button>
                </div>
            );
            }
            ```
    - **Set state là thay thế state bằng giá trị mới** 
        ```js
        function App() {
        const [info, setInfo] = useState({
            name: 'Vudo',
            age: '24',
            address: 'Ha Noi'
        })

        const handleUpdate = () => {
            // Chuỗi lang sẽ được thay thế
            setInfo({
            lang: 'ReactJS'
            })
            // Sử dụng spread để rải chuỗi cũ vào
            setInfo({
                ...info,
            lang: 'ReactJS'
            })
        }

        return (
            <div className="App">
            <h1>{JSON.stringify(info)}</h1>
                <button onClick={handleUpdate}>Update</button>
            </div>
        );
        ```
    - 1 vd nho nhỏ random phần thưởng 
        ```js
        const gifts = [
            'Iphone 13',
            'Ipad Pro 2022',
            'Air port'
        ]

        function App() {
            const [gift, setGift] = useState()

            const handleGift = () => {
                const index = Math.floor(Math.random() * gifts.length)

                setGift(gifts[index])
            }

            return (
                <div className="App">
                    <h1>{gift || 'Chưa có phần thưởng'}</h1>
                    <button onClick={handleGift}>Lấy thưởng</button>
                </div>
            );
        }
        ```
# Two-way binding 
- React là one-way binding 
    - Gõ bên ngoài bên trong thay đổi
- Vue là two-way binding
    - Gõ bên ngoài cả trong cả ngoài đều thay đổi
        ```js
        function App() {
            const [name, setName] = useState('')
            const [email, setEmail] = useState('')

            const handleSubmit = () => {
                console.log({
                    name,
                    email
                })
            }

            return (
                <div className="App">
                    <input type="text"
                        value={name}
                        onChange={e => setName(e.target.value)}
                    />
                    <input type="text"
                        value={email}
                        onChange={e => setEmail(e.target.value)}
                    />
                    <button onClick={handleSubmit}>Register</button>
                </div>
            );
        }
        ```
    
# Mounted (Gắn vào) / Unmounted (Gỡ ra)
- Mounted là khi sử dụng component đó thì gọi là mounted 
- Unmounted là khi mà chúng ta xét điều kiện không sử dụng component nào đó

# useEffect 
- Side effects: Tạo ra sự thay đổi bên cạnh dữ liệu chính (Chạy xong giao diện mới đến effects)
    - Được chia làm 2 loại chính 
        - Effects không cần clean up: Gọi API, tương tác với DOM
        - Effects cần clean up: subscription, setTimeout, setInterval
- Có 3 cách sử dụng useEffect 
    - **useEffect(callback)**
        - Gọi callback mỗi khi component re-render
    - **useEffect(callback, [])**
        - Chỉ gọi callback 1 lần sau khi component mounted
    - **useEffect(callback, [dependency])**
        - `dependency`: Là 1 biến (Có thể là props truyền từ ngoài vào, có thể là state trong component)
        - Callback được gọi lại mỗi khi desp thay đổi 
- `Callback luôn được gọi khi component mounted`
- *Listen DOM event*
    - Scroll: Khi scroll
    - Resize: Khi thay đổi kích thước trang web
- useLayoutEffect 
- Thường sử dụng để xử lý UI 
    - Gần như là giống nhau - Chỉ khác nhau ở thứ tự thự hiện công việc
    ```js
    //useEffect
    1. Cập nhật lại state 
    2. Cập nhật lại DOM (mutated)
    3. Render lại UI
    4. Gọi clean up nếu desp thay đổi 
    5. Gọi useEffect callback

    //useLayoutEffect
    1. Cập nhật lại state 
    2. Cập nhật lại DOM (mutated)
    3. Gọi clean up nếu desp thay đổi (sync)
    4. Gọi useLayoutEffect callback (sync)
    5. Render lại UI
    ```

# useRef 
- ref viết tắt của referent - tham chiếu 
- Giúp tạo 1 biến ra 1 phạm vi bên ngoài function mà khi render lại không bị ảnh hưởng đến biến đó
- Ref luôn trả về object và có property là `current` nên muốn lấy giá trị thì ta phải chọc vào thằng current

# Memo 
- Nghĩa là ghi nhớ 
- Không phải là 1 hook
- memo() -> Higher Order Component (HOC)
- memo sẽ check các props của component xem có props nào bị thay đổi không, nếu có thì mới re-render 
    ```js
    function App() {
        //Code
    }

    export default memo(App)
    ```
# useCallback
- Giúp tránh tạo ra các hàm không cần thiết trong function component 
# useMemo 
- Khác với memo, thằng này là 1 hook, nó viết trong phần thân của function component
- Tránh thực hiện lại 1 logic nào đó không cần thiết
# useReducer 
- Cung cấp thêm 1 giải pháp để xử lý vấn đề (Thường dùng để xử lý các vấn đề phức tạp hơn)
- VD như useState xử lý được thì useReducer cũng xử lý được
    ```js
    //useState 
    1. Init state: 0
    2. Actions: Up (state + 1) / Down (state - 1)

    //useReducer
    1. 

# useState
- **const [todos, setTodos] = useState()**
    - Giá trị trả về của nó là 1 array 
    - todos: Lưu lại trạng thái hiện tại của component 
    - setTodos: Thay đổi trạng thái hiện tại của component 