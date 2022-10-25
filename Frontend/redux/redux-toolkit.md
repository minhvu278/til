# Rexux toolkit
- Setup 1 số hàm có sẵn 
- Giúp viết redux nhanh & gọn hơn

## configureStore() 
- Có sẵn redux devtool
- Có sẵn redux-thunk để thực hiện async actions
    ```js
    import {configureStore} from '@reduxjs/toolkit'
    import rootReducer from './reducers'

    const store = configureStore({reducer: rootReducer})

## createReducer 
- Không sử dụng toolkit
    ```js
    function couterReducer(state = 0, action) {
        switch(action.type) {
            case: 'increment'
                return state + action.payload
            case: 'decrement':
                return state - action.payload
            default: 
                return state
        }
    }
    ```

- Sử dụng toolkit 
    - Mỗi key là 1 case
    - Không cần handle default case
    ```js
    const couterReducer = createReducer(0, {
        increment: (state, action) => state + action.payload,
        decrement: (State, action) => state - action.payload
    })

## createAction
- No toolkit
    ```js
    const INCREMENT = 'counter/increment'

    function increment(amount) {
        return {
            type: INCREMENT,
            payload: amount
        }
    }

    const action = increment(3)
    // {type: 'counter/increment', payload: 3}
    ```

- toolkit
    ```js
    const increment = createAction('counter/increment')

    const action = increment(3)
    // return {type: 'counter/increment', payload: 3}

    console.log(increment.toString())
    // 'counter/increment'

## createSlice 
- Khai báo thay cho action & reducer
    ```js
    const todoSlice = createSlice({
        name: 'todos',
        initialState: [],
        reducers: {
            addPost(state, action) {
                state.push(action.payload)
            },
            removePost(state, action) {
                state.splice(action.payload, 1)
            }
        }
    })

    conar {actions, reducer} = todoSlice
    export const {addPost, removePost} = actions
    export default reducer