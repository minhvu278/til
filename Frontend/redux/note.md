# reducer 
- Có nhiều reducer
- Mỗi reducer sẽ quản lý 1 phần state của app 
- Là 1 function đơn giản - Chuyển đổi state cũ sang state mới thông qua action
    ```js
    const rootReducer = combineReducers({
    hobby: hobbyReducer,
    user: userReducer
    });
    ```
    - Sử dụng `combineReducers` để map vào các key. Vd map vào key là hobby thì sẽ sử dụng thằng hobbyReducer

# action
- Là 1 object: 
    - Quy định các type, payload

# action creator
- Là hàm nhận vào tham số & tạo ra các action tương ứng 
    ```js
    export const addNewHobby = (hobby) => {
        return {
            type: 'ADD_HOBBY',
            payload: hobby
        }
    }
    ```
# redux provider 
- Muốn kết nối redux store đến bất cứ nơi nào trong app thì phải setup redux provider trên tầng cao nhất của app

- Hạn chế kết nối redux vào file App.js - Vì nó là thằng to nhất nếu k may để nó re-render lại thì nó sẽ re-render lại hết các thằng con
- Redux chỉ kết nối với những thằng xử lý logic cho app

# useSelector
- Lấy state từ redux store 
- Connect vao store
    ```js
    // Strict comparison ===
    const hobbyList = useSelector(state => state.hobby.list)
    const activeId = useSelector(state => state.hobby.activeId)

    // Shallow comparison
    const hobbyState = useSelector(state => ({
        list: state.hobby.list,
        activeId: state.hobby.activeId,
    }))
    ```
    - Với cách sử dụng **Strict comparison** thì mỗi lần thằng redux được cập nhật hoặc thay đổi thì useSelector sẽ được chạy lại & tính toán lại 1 state mới. Nó sẽ so sánh *state.hobby.list* cũ so sánh với *state.hobby.list* cũ (So sánh ===) nếu như nó giống nhau thì sẽ không trigger re-render - còn khác thì sẽ trigger
    - Với cách sử dụng **Shallow comparison** nó sẽ luôn trả về 1 object mới vì thế nên lúc nào nó cũng sẽ trigger  re-render 

# Redux toolkit
- createSlice: Tạo trạng thái ban đầu của state
- configureState: Tạo store
- selector: store xuất ra dữ liệu gì đó thì component sẽ nhận dữ liệu đó