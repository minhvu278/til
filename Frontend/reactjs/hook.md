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
    
