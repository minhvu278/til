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
    - Tạo action dưới dạng function & trả ra 1 object
        ```js
        const setJob = payload => {
            return {
                type: SET_JOB,
                payload
            }
        }

        console.log(setJob('Rua bat'))
        ```
        - payload nghĩa là dữ liệu mang theo đi tương ứng với người dùng gõ vào input 
- VD: Ứng dụng todo 
    ```js
    //Init state
    import {useReducer, useRef} from "react";

    const initState = {
        job: '',
        jobs: []
    }

    //Action
    const SET_JOB = 'set_job'
    const ADD_JOB = 'add_job'
    const DELETE_JOB = 'delete_job'

    const setJob = payload => {
        return {
            type: SET_JOB,
            payload
        }
    }

    const addJob = payload => {
        return {
            type: ADD_JOB,
            payload
        }
    }

    const deleteJob = payload => {
        return {
            type: DELETE_JOB,
            payload
        }
    }

    console.log(setJob('Rua bat'))

    //Reducer
    const reducer = (state, action) => {
        console.log('Action: ', action)
        console.log('State: ', state)

        let newState

        switch (action.type) {
            case SET_JOB:
                newState = {
                    ...state,
                    job: action.payload
                }
                break
            case ADD_JOB:
                newState = {
                    ...state,
                    jobs: [...state.jobs, action.payload]
                }
                break
            case DELETE_JOB:
                const newJob = [...state.jobs]

                newJob.splice(action.payload, 1)
                
                newState = {
                    ...state,
                    jobs: newJob
                }
                break
            default:
                throw new Error('Invalid action')
        }
        console.log('New state ', newState)
        return newState
    }

    function App() {

        const [state, dispatch] = useReducer(reducer, initState)

        const {job, jobs} = state

        const inputRef = useRef()

        const handleSubmit = () => {
            dispatch(addJob(job))
            dispatch(setJob(''))

            inputRef.current.focus()
        }

        return (
            <div className="App" style={{padding: '20px'}}>
                <h3>Todo</h3>
                <input
                    ref={inputRef}
                    value={job}
                    onChange={e => {
                        dispatch(setJob(e.target.value))
                    }}
                    placeholder="Enter todo..."
                />
                <button onClick={handleSubmit}>Add</button>

                <ul>
                    {jobs.map((job, index) => (
                        <li
                            key={index}>{job}
                            <span onClick={() => dispatch(deleteJob(index))}>&times;</span>
                        </li>
                    ))}
                </ul>
            </div>
        )
    }

    export default App;
    ```

# useReducer recap (tom tat)
## Lợi ích khi sử dụng useReducer 
- Sử dụng trong function component thôi, còn 2 đối số truyền vào `reducer, initState` thì nhận ở bên ngoài vào
    - Có thể tách các thành các file riêng: VD tách action, reducer ra các file khác nhau và import vào
    - Làm cho code nhìn gọn hơn 

# So sánh Redux & react-context
- Cách hoạt động của **context** giống với redux, tuy nhiên thì nó không phải sinh ra để thay thế thằng redux 
- Ưu điểm của redux: 
    - Dễ dàng để triển khai debug hơn (Có thư viện react-debugg giúp có thể inspace từng element dễ quan sát state thay đổi trong ứng dụng hơn)
    - Có cơ chế để apply middleware dễ dàng 
    - Có addons để dễ dàng mở rộng hơn 
    - Là Cross-platform(Đa nền tảng) không bị phụ thuộc vào react (Đáp ứng được tất cả các dự án nào sử dụng JS kể cả code thuần - Còn context chỉ sử dụng được cho react)
    - Có thể dễ dàng cấu hình & performent sẽ hơn hẳn khi sử dụng context
- Nhược điểm của thằng context: 
    - Nó sẽ re-render lại toàn bộ lại ứng dụng nếu bao nó vào App (Redux thì cái nào thay đổi nó mới render lại) vì thế chỉ nên sử dụng trong ứng dụng vừa nhỏ
- `Ứng dụng nhỏ thì nên sử dụng context, còn ứng dụng lớn thì sử dụng redux nó sẽ tối ưu hơn`