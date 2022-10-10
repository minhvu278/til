# useRef 
- Lưu giá trị qua một tham chiếu bên ngoài function component
- Mỗi hàm được gọi sẽ luôn tạo ra phạm vi mới và không liên quan gì đến phạm vi trước đó
- Nó là 1 hàm & nhận vào 1 giá trị initialValue
    - Sử dụng giá trị này lần đầu tiên khi component được mounted
- Luôn trả về giá trị là object(Kể cả truyền vào giá trị khởi tạo là số hay string) & có 1 property là current 
    - Để lấy được giá trị của ref thì phải chọc qua current
    ```js
    const ref = useRef(99)

    console.log(ref.current)
    ```
- Thường dùng để lưu DOM element
    - React hỗ trợ nếu lưu 1 object ref cho 1 thằng reactElement tượng trưng cho những thẻ được render vào DOM thật (div, h1,...)
    ```js
    const h1Ref = useRef()

    useEffect(() => {
        console.log(h1Ref.current); // OUTPUT: <h1>OK Bae</h1>
    })
    
     return (
        <h1 ref={h1Ref}>OK Bae</h1>
     )
    ```
    - Nó giống hệt với việc getElementById || querySelector -> Lấy element luôn
    
### VD
- Biết được giá trị của hiện tại và trước đó của state trước 1 lần render
    ```js 
    function App() {

        const [count, setCount] = useState(60)

        const timerId = useRef()
        const prevCount = useRef()

        useEffect(() => {
            prevCount.current = count
        }, [count])

        const handleStart = () => {
            timerId.current = setInterval(() => {
                setCount(prevCount => prevCount - 1)
            }, 1000)
            console.log('Start ->', timerId.current)
        }

        const handleStop = () => {
            clearInterval(timerId.current)

            console.log('Stop ->', timerId.current)
        }

        console.log(count, prevCount.current)

        return (
            <div className="App" style={{padding: '20px'}}>
                <h1>{count}</h1>
                <button onClick={handleStart}>Start</button>
                <button onClick={handleStop}>Stop</button>
            </div>
        )
    }
    ```
