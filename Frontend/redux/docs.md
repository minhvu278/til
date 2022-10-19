# Redux
- Redux là gì? Kiến trúc của nó như nào?
- Khi nào cần sử dụng redux 
- Redux có phải chỉ để dùng với reactjs không?
- Vd mẫu
- Các thư viện làm viêc với redux 

## Redux là gì 
- Là thư viện js quản lý state - state này có thể dự đoán được 
- Sử dụng kiến trúc uni-directional data flow (1 chiều)
    - Store -> view -> action 
        - Store có giá trị gửi lên view -> view click button tạo ra action -> action nó chỉ là object chứa thông tin mô tả muốn làm gì với store -> Store cập nhật và trả lại ra 1 state mới -> Khi có state mới nó sẽ thông báo ra view để cập nhật lại giao diện 
- L
    - Initstate  --> view (click button)  -->  action  -->  Store(action, reducer(state hiện tại, action))  --> State mới  --> View
- Trong store có 3 phần: 
    - Dispatcher 
        - Là phần quản lý các middleware: Thường dùng để gọi API, log,...
    - Reducer
        - Là 1 function nhận vào 2 thứ: `State hiện tại và Action gửi lên ` (Đi qua dispatcher mới vào reducer)
    - State 
        - Và khi reducer biến đổi nó sẽ trả ra state mới rồi lại báo UI cập nhật lại
## Khi nào cần sử dụng redux 
- Khi cần sử dụng ở nhiều nơi: Như login, cart 
- Hỗ trợ undo/redo 
- Cần cache lại dữ liệu để sử dụng cho các lần sau 

## VD
- Định nghĩa reducer: state hiện tại & thông tin của action
    ```js
    function counter(state = 0, action) {
        switch (action.type) {
            case 'INCREMENT': 
                return state + 1
            case 'DECREMENT': 
                return state - 1
            default: 
                return state
        }
    }
    ```
    - action chỉ là object có nhiệm vụ đổi từ state cũ sang state mới dựa và action type
- Setup store: có hàm **createStore** nhận vào reducer
    ```js 
    let store = createStore(couter)
    ```
    - Khi tạo store nó sẽ có 3 hàm: *subscribe, dispatch, getState*
        - subscribe: Đăng kí mỗi lần state thay đổi sẽ thực hiện 1 hàm nào đó
        - dispatch: Tạo ra các action
        - getState: State hiện tại
- Subscribe to state changes to update UI
    ```js 
    store.subcribe(() => console.log(store.getState()))
    ```
- Dispatch action 
    ```js
    store.dispatch({ type: 'INCREMENT' }) //1
    store.dispatch({ type: 'INCREMENT' }) //2
    store.dispatch({ type: 'DECREMENT' }) //1
    ```


## `Tóm lại` 
- Redux sử dụng kiến trúc 1 chiều 
- Store chỉ sử dụng 1 nguồn duy nhất Single Source of Truth
- Redux state là READ-ONLY. Muốn update phải dispatcher 1 action 
- Những thay đổi của redux state được thực hiện bởi reducer 
- Redux được sử dụng cho javascript app chứ không chỉ cho riêng react


# rootReducer 
- Kết hợp tất cả các reducer lại tất cả các reducer trong app
- Tổng hợp các reducer con lại