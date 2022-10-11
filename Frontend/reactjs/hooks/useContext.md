# useContext 
- Là ngữ cảnh - Nó sẽ tạo ra 1 phạm vi để truyền dữ liệu trong phạm vi đó 
- Giúp đơn giản hóa việc truyền dữ liệu từ các component cha xuống các component con mà không cần sử dụng đến props 
- CompA => CompB => CompC
    - Tạo context ôm cả component A thì nó sẽ truyền được dữ liệu xuống bất cứ component nào mà là con của nó mà không cần thông qua trung gian. CompA => CompC
    - Để truyền dữ liệu sử dụng provider 
    - Để nhận dữ liệu từ thằng cha thì sử dụng Consumer 
## Sử dụng 
- Cần nắm 3 bước 
    - Tạo ra context 
    - Provider (Cung cấp dữ liệu)
    - Consumer (Nhận dữ liệu)
- Provider & Consumer thì nó là react component nên có thể dùng JSX để sử dụng nó 
    ```js
    export const ThemeContext = createContext()

    function App() {

        const [theme, setTheme] = useState('dark')

        const toggleTheme = () => {
            setTheme(theme === 'dark' ? 'light' : 'dark')
        }

        return (
            <ThemeContext.Provider value={theme}>
                <div style={{padding: 20}}>
                    <button onClick={toggleTheme}>Toggle Theme</button>
                    <Content/>
                </div>
            </ThemeContext.Provider>
            );
    }
    ```
    - Những component ở bên trong sẽ sử dụng được `theme` mà không cần truyền qua props (<Content theme={theme}/>)
    - Để component con sử dụng đươc thì đầu tiên cần export ra 
        ```js
        export const ThemeContext = createContext()
        ```
    - Sử dụng: 
        ```js
        function Paragraph() {
            const theme = useContext(ThemeContext)
            return (
                <p className={theme}>
                    Giúp đơn giản hóa việc truyền dữ liệu từ các component cha xuống các component con mà không cần sử dụng đến props
                </p>
            );
        }
        ```
    
