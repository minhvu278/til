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
- Sử dụng với 