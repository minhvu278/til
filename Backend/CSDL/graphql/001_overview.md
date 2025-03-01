# Graphql là gì?
- Graphql là 1 ngôn ngữ truy vấn (query language) dành cho API
- Được phát triển bởi Facebook vào năm 2012 và công bố rộng rãi vào 2015
- Nó không phải là CSDL hay công nghệ cụ thể nào mà là 1 cách để giao tiếp giữa client và server
- Không giống như REST - Một cách tiếp cận truyền thống trong API - Graphl cho phép client yêu cầu chính xác những dữ liệu mà nó cần, không hơn không kém.
  - Việc này giúp tránh việc nhận quá nhiều dữ liệu không cần thiết (over-fetching) hoặc phải gọi nhiều API khác nhau để lấy đủ dữ liệu (under-fetching)

# Graphl hoạt động như thế nào?
- Hãy tưởng tượng bạn đang đi ăn ở 1 nhà hàng
  - Với REST, bạn gọi món theo thực đơn cố định, bếp sẽ mang ra tất cả mọi thứ trong món đó, kể cả những thứ bạn không muốn ăn
  - Với GrapQL, bạn giống như được tự chọn: Tôi chỉ muốn ăn cơm, thịt và rau, không cần nước sốt. Bếp sẽ làm đúng yêu cầu của bạn
## Cụ thể, GrapQL hoạt động qua các phần chính sau:
- **Schema (Lược đồ)**: Đây là "menu" của dữ liệu, được định nghĩa ở phía server. Schema mô tả tất cả các loại dữ liệu (types) mà client có thể yêu cầu, ví dụ như User, Post, Comment cùng với các trường (field) của chúng ta ví dụ như name, age, title
  - Ví dụ
  ```ts
  type User {
    id: ID!
    name: String!
    age: Int
  }
  ```
  - Dấu `!` nghĩa là trường đó bắt buộc phải có giá trị
- **Query(Truy vấn)**: Client gửi request đến server dưới dạng 1 truy vấn, chỉ định rõ ràng dữ liệu mà nó muốn lấy. Ví dụ
```
{
  user(id: "1") {
    name
    age
  }
}
```
- Kết quả trả về
```
{
  "data": {
    "user": {
      "name": "Nguyen Van A",
      "age": 25
    }
  }
}
```
  - Lưu ý ở đây là chúng ta chỉ nhận được `name và age`, không có dữ liệu thừa nào khác

- **Mutation**: Ngoài việc lấy dữ liệu (query), GraphQL còn hỗ trợ việc thay đổi dữ liệu trên server, như thêm, sửa, xoá
```
mutation {
  createUser(name: "Do Minh Vu", age: 18) {
    id
    name
  }
}
```

- **Resolver**: Ở phía server, các hàm resolver sẽ xử lý logic để lấy hoặc thay đổi dữ liệu dựa trên query/mutation mà client gửi. Ví dụ, resolver của `user` có thể lấy thông tin từ CSDL và trả về

- **Một enpoint duy nhất**: Khác với REST thường có nhiền endpoint như (/users, /posts), GraphQL chỉ cần 1 endpoint duy nhất (thường là /graphql) và mọi request đều xử lý qua đó

# Ưu điểm
- **Linh hoạt**: Client quyết định dữ liệu cần lấy, không phụ thuộc vào server
- **Hiệu quả**; Giảm số lượng request & lượng dữ liệu thừa
- **Dễ bảo trì**: Khi dữ liệu thay đổi, schema được update & client tự điều chỉnh query

# Nhược điểm
- **Phức tạp cho server**: Cần xây dựng schema và resolver cần thận
- **Khó caching**: Không giống REST, caching ở GraphQL cần công cụ hỗ trợ như Apollo hoặc Relay

## Ví dụ thực tế
- Giả sử chúng ta làm 1 ứng dụng blog
  - Với REST, chúng ta có thể gọi `/users/1` và nhận toàn bộ thông tin user (name, age, address,...) mặc dù ở đây bạn chỉ cần tên
  - Với GraphQL, bạn gửi truy vấn chỉ lấy `name` và server trả về đúng cái đó
- **Nếu muốn tìm hiểu sâu hơn, chúng ta nên sử dụng GraphQL hoặc Apollo Sandbox để thử viết truy vấn hoặc đọc tài liệu chính thức tại `graphql.com`**
