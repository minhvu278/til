# Const
- Hằng số cũng có tính năng shadow 

# Array slice 
- Cú pháp khai báo: 
    - C1: Khai báo mảng với 3 phần tử 
        ```go
        points := [3]int{5, 8 ,2}
        ```
    - C2: Khai báo bao nhiêu phần tử thì cấp phát bằng đó 
        ```go
        points := [...]int{5, 8 ,2, 5}
        ```
- Để không tốn bộ nhớ ta có thể trỏ thẳng đến vùng nhớ 
    ```go
    a := [3]int[2, 5, 10]
    b := &a
    b[1] = 20
    ```
    - Khi ta thay đổi b thì a cũng thay đổi theo (b trỏ tới vùng nhớ của a)

## **Slice**
- Giống với các đặc điểm của mảng nhưng được cái nó có kích thước động 
- Khai báo slice
    - Khi ta không khai báo kích thước trong [] thì mảng đó sẽ được hiểu là slice
    - Khi sử dụng slice thì ta không cần phải trỏ đế `&a` như ở array nữa
    ```go
    a := []int[2, 5, 10]
    b := a
    b[1] = 20
    ```
- Khác nhau giữa slice và array 
    - VD có 1 mảng `a = 1, 2, 4, 5, 7, 8, 10, 3` tính từ 4 -> 8
        - Nếu dùng len thì sẽ là 4 phần tử 
        - Còn dùng cap thì sẽ là 6 phần tử
- Toán tử `:` trong slice dùng để thay đổi con trỏ đầu và con trỏ cuối của slice
    - 1 cách dễ hiểu hơn là để cắt mảng từ đoạn nào đến đoạn nào 
        ```go 
        a := []int[2, 5, 10, 12, 45, 50]
        b := a[:] // lấy tất cả dữ liệu của a đổ vào b 
        c := a[3:] // Lấy từ phần tử thứ 3 đổ đi `12 -> 50`
        d := a[:5] //Cắt từ đầu đến index số 4
        e := a[3:5] // Cắt từ index 3 đến đến index 4

- `Lưu ý khi dùng slice :` Khi ta thay đổi 1 phần tử trong mảng thì các phần tử 
- **Từ khóa make trong slice**
    - Là 1 hàm make dùng để khai báo 1 slice mà có thể xác định được len và cap 
        ```go
        a := make([]int, 5) // Cả len và cap đều có độ dài bằng 5
        a := make([]int, 5, 10) // len có độ dài là 5 và cap đều có độ dài bằng 10
        ```
    - Sử dụng append để thêm phần tử vào mảng 
        - Thay đổi kích thước của slice đồng thời thay đổi các kích thước mảng của slice
        ```go
        a := make([]int, 0)
        a = append(a, 1) // slice có 1 phần tử là 1
        ```
    - Hiện thực cho cấu trúc dữ liệu ngăn xếp và hàng đợi

# Map struct