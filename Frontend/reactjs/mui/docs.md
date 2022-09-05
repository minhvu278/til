# Typography
- Các cặp thẻ trong HTML sẽ được định nghĩa trong này sử dụng cặp thẻ `<Typography>`
- Trong thẻ này ta có thể sử dụng `variant` để có thể định nghĩa được các cặp thẻ từ `h1->h6`
    ```js
    <Typography 
        variant={"h1"}
        color="primary"
        align="center"
    >
          Create page
    </Typography>
    ```
    - Và cũng có thể căn chỉnh màu, căn giữa,...

# Button
- Ta dùng thẻ `<Button>` và cũng có thể style trực tiếp vào trong nó
    ```js 
    <Button type="submit"
            color="secondary"
            variant="container"
        >
            Submit
    </Button>
    ```
- Nếu có nhiều button ta cũng có thể group chúng lại rồi style: Sử dụng `<ButtonGroup>`

# Icon
- Cần cài thêm pakage svg icon 
    ```
    npm install @material-ui/icons
    ```
- Khi cần dùng icon nào thì ta vào thư viện và import icon mà ta muốn dùng, và cũng có thể style cho nó luôn
    ```
    {/*Icon */}
        <AcUnitOutlined color="secondary" fontSize="large" />
    ```
- Có thể dùng icon để chèn vào đầu và cuối **button**
    ```js
    <Button type="submit"
            color="secondary"
            variant="contained"
            startIcon={<AcUnitOutlined />} // Icon hiển thị ở đầu 
            endIcon={<AcUnitOutlined />} // Icon hiển thị ở cuối
    >
        Submit
    </Button>
    ```

# makeStyles Hook (Customer css)
- Để sử dụng nó thì cần import `makeStyles`
- VD: 
    ```js
    const useStyles = makeStyles({
        btn: {
            fontSize: 60,
            backgroundColor: 'violet',
            '&:hover': {
                backgroundColor: 'blue'
            }
        },
        title: {
            textDecoration: 'underline',
            marginBottom: 20
        }
    })

    export default function Create() {

    const classes = useStyles()

    return (
        <Container>
        <Typography
            variant="h6"
            color="textSecondary"
            component="h2"
            gutterBottom
        >
            Create page
        </Typography>

            <Button className={classes.btn}
                    type="submit"
                    color="secondary"
                    variant="contained"
                    startIcon={<AcUnitOutlined />}
                    endIcon={<AcUnitOutlined />}
            >
                Submit
            </Button>
        </Container>
    )
    }
    ```
    - Sử dụng thuộc tính nào thì ta chỉ cần `.` đến nó