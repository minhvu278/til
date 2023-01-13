# Static type checking 
- Không cần chạy code mà nó đã phát hiện ra lỗi đó luôn rồi 
- Tìm ra lỗi ngay trong lúc code
- Lỗi hoa thường 
- Giúp nhắc code

# Ts compiler 
- Để compile ts sang js thì cần cài và sử dụng tsc 
- 1 số thứ trong tsconfig.json 
    - "outDir": "./dist"
        - Khi compiler nó sẽ tạo ra 1 thư mục mới chứa code được compiler sang js 
    - "allowJS": true
        - Nếu để là true thì nó sẽ compiler ra cả file js
    - noEmitOnError: true 
        - Nếu là true thì nó sẽ compiler kể cả khi có lỗi 

# 1 số type cơ bản trong TS 
- Explicit types: Khai báo kiểu tường minh 
    - Đây là cách khai báo rõ ràng nó là kiểu dữ liệu gì 
    ```js
    let count: number = 123
    let studentName: string = "Vu Do"
    const numberList: number[] = [1, 2, 3]
- Inferred types: Kiểu suy luận 
    - Typescript khá thông minh khi detect được kiểu dữ liệu tương ứng ngay cả khi không khai báo cụ thể kiểu dữ liệu
    - Tuy nhiên thì chỉ nên khai báo như thế này khi kiểu dữ liệu đơn giản, còn phức tạp hơn thì nên khai báo theo kiểu 1
    ```js
    const count = 123 // Nó sẽ tự nhận biết được là kiểu number (Có thể hover vào để xem)
- Eraised types: Sau khi compiler từ TS sang JS, tất cả các annotation sẽ bị xóa
    - Vì code sau cùng sẽ vẫn được compiler ra JS 
- Downleveling: 
    - Tuỳ vào target mà code sau khi được compile ra javascript sẽ khác nhau để đảm bảo target
environment có thể hiểu và thực thi được code mình viết bên typescript.

# Destructuring 
- Rút các dữ liệu từ object ra thành các biến khác nhau 
    ```js
    const bob = {
    id: 1,
    name: 'Bob',
    age: 18,
    gender: 'male'
    };
    // OLD WAY
    const id = bob.id;
    const name = bob.name;
    // NEW WAY
    const { id, name } = bob;
    ```

# Tổng quan về type system
- Nếu dùng kiểu *any* nó sẽ bỏ qua việc type checking 

# Type alias & interface 
- Type alias: Đặt tên lại cho bất kể kiểu dữ liệu nào khác 
    - Vd đặt tên mới cho kiểu dữ liệu string 
        ```js 
        type StudentName = string 
        ```
- Interface: Đặt tên lại cho object 

- Union type
    - Kết hợp giữa 2 hoặc nhiều kiểu dữ liệu lại với nhau để tạo ra 1 kiểu dữ liệu mới 
    - Cho phép giá trị có thể chấp nhận hoặc là kiểu dữ liệu này hoặc là kiểu dữ liệu kia
    ```js
    type Status = 'active' | 'inactive';
    type ProductStatus = 0 | 1 | 2 | 3;
    type StudentId = number | string;
    interface Student {
    id: number | string;
    name: string;
    gender: 'male' | 'female';
    grade: 'A' | 'B' | 'C' | 'D' | 'E';
    }
    ```
# Những điều cần lưu ý khi làm việc với function 
- Default function return type
    - Dựa vào giá trị trả về có thể suy ra được kiểu trả về 
        ```js
        function sayHello() {
        console.log('Hi Easy Frontend');
        }
        // ts: function sayHello(): void
        ```
        - Đối với hàm k có return sẽ trả về void (Hàm k trả về hoặc k cần care đến giá trị trả về)
- Explicit return type
    - Định nghĩa giá trị trả về
        ```js
        function sum(a: number, b: number): number {
        return a + b;
        }
        // ts: function sum(a: number, b: number): number
        ```