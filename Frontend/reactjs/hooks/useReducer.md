# useReducer
- Cung cấp thêm 1 sự lựa chọn khi sử dụng state cho function component 
- useState xử lý được cái gì thì useReducer cũng xử lý được và ngược lại 
## Vậy khi nào dùng thằng nào
- Trong hầu hết các trường hợp, ta sử dụng useState để tạo ra trạng thái cho component - useState có xu hướng sử dụng phù hợp hơn đối với các component đơn giản
- Trong trường hợp có nhiều state trong 1 component thì sử dụng useReducer thì nó sẽ đơn giản hoá hơn, hoặc có thế tách ra 1 file riêng 

## Cách triển khai khác nhau như nào 
- VD: Cho bài toán là giá trị khởi tạo là 0 bấm up tăng lên 1 down - 1
    - Sử dụng useState: 
        - Init state: 0
        - Actions: Up (state + 1) / Down (state - 1)

    - Sử dụng useReducer 
        - Init state: 0
        - Actions: Up (state + 1) / Down (state - 1)
        - Reducer: Nhận đầu vào và trả ra đầu ra mới (Input & output)
            - Là 1 hàm, nhận đầu vào là state và action & tùy vào action để trả ra state mới tùy thuộc vào logic 
            ```js
            const initState = 0

            //Action
            const UP_ACTION = 'up'
            const DOWN_ACTION = 'down'

            //Reducer
            const reducer = (state, action) => {
                switch (action) {
                    case UP_ACTION:
                        return state + 1
                    case DOWN_ACTION:
                        return state - 1
                    default:
                        throw new Error('Invalid action')
                }
            }
            ```
        - Dispatch: Dùng để xác định action nào sẽ được thực hiện dẫn đến việc state được thay đổi và nó re-render lại component 
        ```js
        function App() {

            const [count, dispatch] = useReducer(reducer, initState)

            return (
                <div className="App" style={{padding: '20px'}}>
                    <h1>{count}</h1>
                    <button
                        onClick={() => dispatch(DOWN_ACTION)}
                    >
                        Down
                    </button>
                    <button
                        onClick={() => dispatch(UP_ACTION)}
                    >
                        Up
                    </button>
                </div>
            )
        }
        ```
