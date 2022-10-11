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