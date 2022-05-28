# Variable 
 
 ## Khai báo 
 - Có 1 vài cách khai báo biến trong `go` như sau
    - `var i int = 10` - Vừa khai báo vừa khởi tạo 
    - `i := 10` - Cũng giống như trên nhưng gọn hơn 

    ```go
    k := 11;
    fmt.Printf("%v, %T", k, k)
    ```
    - Printf: Xuất theo chuỗi định dạng mà ta muốn 
    - %v: Xuất ra giá trị
    - %T: Xuất ra kiểu của biến đó

- Global scope 
    ```go
    var (
        n int = 10
        m int = 32
        h Stirng = 10
    )

    func main() {
        fmt.Println(n)
        fmt.Println(m)
        fmt.Println(h)
    }
    ```
    - Có thể sử dụng `var()` để khai báo gọn các biến 

- Shadow 
    - Ví dụ ta khai báo ở global biến `n = 10` vào trong func ta lại khai báo lại `n = 1000` thì khi in ra nó sẽ lấy giá trị là `1000` - Cái này nó sẽ gọi là shadow (Giá trị bên trong che giá trị của global)

- Trong go thì những biến khai báo nhưng không sử dụng thì chương trình sẽ bị lỗi 

- Export global scope 
    - Khi muốn các pakage khác có thể truy xuất vào biến global thì ta chỉ cần viết hoa tên biến là được 
        ```go
        var N = 10 

        func main() {
            fmt.Println(N)
        }
        ```

- Name convension 
    - Đặt tên theo kiểu camel convension 

- Convert type 
    ```go
    var i float32 = 10.5

    var j int = int(i)
    ```
    - Chuyển kiểu số sang string
        ```go
        var i int = 10

        var j string = strconv.Itoa(i)
        ```

# Hằng số 

## Khai báo
- Sử dụng từ khóa `const`
- Còn lại thì giống biến

- Tự động khởi tạo giá trị cho Enum bằng `iota`
     ```go
    const (
        n = iota
        m
        h
    )

    func main() {
        fmt.Println(n) //0
        fmt.Println(m) //1
        fmt.Println(h) //2
    }
    ```

- Sử dụng `_` để vẫn đưa giá trị nhưng không muốn đặt tên

    
