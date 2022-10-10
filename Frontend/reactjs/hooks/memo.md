# React.memo HOC (Ghi nhớ)
- Không phải là 1 hooks
- memo() ->Higher Order Component (HOC) - Component bậc cao - Không dùng ở bên trong mà sẽ wrap component lại
    ```js
    export default memo(App)
    ```
- Giúp ghi nhớ lại các props của component để nó quyết định có render lại các component đó hay không để tối ưu về hiệu năng 
    - `memo giúp xử lý 1 component để tránh bị re-render trong những tình huống không cần thiết`
## 3 khái niệm hay sử dụng trong react 
- Hook
- HOC
- Render props
    - Cả 3 thằng đều được sử dụng để kế thừa logic - Thay vì bị lặp đi lặp lại logic nhiều lần thì ngta thiết kế ra 3 cái này & mỗi cái chứa tính năng cụ thể

## Nguyên lý hoạt động của component
- Nhận vào 1 component, sau đó check các props của component có bị thay đổi không
    - Nếu ít nhất có 1 props thay đổi thì component sẽ bị re-render
    - Còn không thì nó sẽ không re-render 
    ```js
    import React, {memo} from 'react';

    function Memo() {
        console.log('re-render')
        return (
            <h2>HELLO BAE</h2>
        );
    }

    export default memo(Memo);
    ```
    - Trường hợp không có memo thì khi thằng cha gọi đến thì thằng con cũng sẽ bị re-render

# useMemo
- Là 1 hooks (Khác với memo - HOC - Ôm lấy component)
- Viết trong phần thân của function component 
- Tránh thực hiện 1 logic nào đó không cần thiết
//TODO: Note sau