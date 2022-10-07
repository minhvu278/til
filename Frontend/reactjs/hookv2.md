# Hook
- Nghĩa là gắn vào, móc vào
- Được thêm vào từ phiên bản 16.8.0
- Khi hook chưa ra đời thì ta sử dụng class để xây dựng ra các tính năng, còn function khi ấy chỉ là render ra giao diện
- Khi có hook, nó hỗ trợ thằng function component đầy đủ các tính năng không thua kém gì class component 
## Vậy hook là gì mà lại làm cho function component trở nên xịn xò hơn
- Thực chất thì nó là các method, function được cũng cấp sẵn của Reactjs. Mỗi hàm này đều có 1 tính năng, 1 trường hợp cụ thể để sử dụng
- Khi sử dụng function component mà ta cần thêm các tính năng mà thằng hook cung cấp thì ta chỉ cần lấy ra và thêm vào dùng trong function đó. Vì thế nên nó được gọi là hook vì cách dùng của nó là gắn vào, móc vào
    ```js
    import {useState} from "react"; // Lấy ra

    function Component() {
        const [state, setState] = useState(initState) //Móc vào 
        
            ...
    }
    ```

# List các hook
- useState
    ```
    const [state, setState] = useState(initState)
    ```
- useEffect
    ```
    useEffect(() => {

    }, [deps])
    ```
- useLayoutEffect
    ```
    useEffect(() => {

    }, [deps])
    ```
- useRef
    ```
    const ref = useRef()
    ```
- useCallback
    ```
    const fn = useCallback(() => {

    }, [deps])
    ```
- useMemo
    ```
    const result = useMemo(() => {

    }, [deps])
    ```
- useReducer
    ```
    const result = useMemo(() => {

    }, [deps])
    ```
- useContext
    ```
    const value = useContext(MyContext)
    ```
- useImperativeHandle
    ```
    useImperativeHandle(ref, createHandle, [deps])
    ```
- useDebugValue
    ```
    useDebugValue(isOnline ? 'Online' : 'Offline')
    ```
## Cần nắm được khi sử dụng hook 
- Tên, ý nghĩa của nó
- Nó nhận đối số là gì 
- Nó có trả ra cái gì hay không
- Những cái nó trả ra thì nó hoạt động như thế nào 

## `Túm lại`
- Hook chỉ dùng cho function component 
- Giúp component trở nên dễ hiểu hơn 
    - Không bị chia logic ra như method trong lifecycle của Class Component 
    - Không cần sử dụng **this** 
- Sử dụng hooks khi nào ?
    - Dự án mới => Hook
    - Dự án cũ 
        - Component mới => Function component + hook
        - Component cũ => Giữ nguyên, có thời gian tối ưu sau 
    - Logic nghiệp vụ cần sử dụng đến các tính chất của OOP (Vd như sử dụng tính kế thừa) => Class Component 
