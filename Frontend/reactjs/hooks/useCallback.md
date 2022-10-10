# useCallback
- Sinh ra để giúp tránh được tạo các hàm callback không cần thiết
- Sử dụng với reference types (Tham chiếu)
- Cách sử dụng thì khá giống với useEffect 
    ```js
    function App() {

        const [count, setCount] = useState(0)

        const handleIncrease = useCallback(() => {
            setCount(prevCount => prevCount + 1)
        }, [])

        return (
            <div className="App" style={{padding: '20px'}}>
                <Memo onIncrease={handleIncrease} />
                <h1>{count}</h1>
            </div>
        )
    }
    ```
    - Đó, khá giống với useEffect, nếu không thay đổi thì truyền [] còn nếu thay đổi thì truyền [deps] vào

- `1 component có thể nhận nhiều kiểu dữ liệu (có thể là string, object, tham chiếu,...)`
    - Nếu đã dùng **memo** để tránh re-render không cần thiết thì những function đều phải sử dụng **useCallback**