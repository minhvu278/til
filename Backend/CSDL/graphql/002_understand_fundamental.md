# Giai đoạn 1: Hiểu nền tảng cơ bản
- Giả sử bây giờ chúng ta sẽ xây dựng 1 ứng dụng Todo-list

## Mục tiêu
- Hiểu GraphQL là gì, nó khác gì với REST
- Biết cách viết Query, Mutation, Schema và Resolver
- Tạo được 1 dự án GraphQL cơ bản chạy được

# Lý thuyết
## GrapQL là gì? So với REST
- **GraphQL**: Là ngôn ngữ truy vấn cho API, giúp bạn yêu cầu chính xác dữ liệu mình cần. Giống như việc đi siêu thị chỉ lấy đúng thứ bạn cần thay vì mua full giỏ không cần thiết
- **REST**: Là cách truyền thống để lấy dữ liệu, thường cố định ở từng endpoint.
  - Ví dụ `/todos` trả về danh sách công việc nhưng có thể kèm các dữ liệu thừa (Ví dụ ngày tạo mà chúng ta không cần)
### Ví dụ thực tế
- Với REST. Chúng ta gọi `todos/1`, server sẽ trả về
```
{
  "id": 1,
  "title": "Mua sữa",
  "completed": false,
  "createdAt": "2025-02-28",
  "updatedAt": "2025-02-28"
}
```
- Bạn chỉ cần title và completed, nhưng vẫn nhận thêm createdAt, updatedAt (gọi là over-fetching)
- Với GraphQL, bạn gửi query
```
{
  todo(id: "1") {
    title
    completed
  }
}
```
- Server sẽ trả về những thứ mà bạn cần
```
{
  "data": {
    "todo": {
      "title": "Mua sữa",
      "completed": false
    }
  }
}
```
## Các khái niệm cơ bản
- **Query**: Dùng để lấy dữ liệu
  - VD: Lấy danh sách công việc hôm nay
- **Mutation**: Dùng để thay đổi dữ liệu (CUD)
  - VD thêm 1 công việc mới (Mua pánh mì)
- **Schema**: Định nghĩa cấu trúc dữ liệu, giống như menu của API
  - Ví dụ: Một công việc (Todo) có id, title, completed
- **Resolver**: Hàm xử lý logic để trả về dữ liệu query/mutation
  - Ví dụ bạn yêu cầu 1 todo list, resolver sẽ lấy từ mảng hoặc DB

# Thực hành cơ bản: Xây dựng ứng dụng Quản lý blog với GraphQL + MongoDB
- Như ở phần Overview, chúng ta dùng giữ liệu mock. Bây giờ hãy cùng nâng cấp lên 1 chút là thao tác với CSDL, ở đây chúng ta sẽ đùng MongoDB - Vì nó phổ biến và dễ bắt đầu
- Chúng ta sẽ xây dựng 1 ứng dụng Quản lý Blog phức tạp hơn với các relationship giữa User & Post

## Mục tiêu
- Kết nối GraphQL với MongoDB
- Ứng dụng gồm có
  - User đăng bài viết (post)
  - Mối quan hệ: Mỗi bài post thuộc về 1 user
  - Tính năng: Lấy danh sách bài viết, thêm bài viết, lấy bài viết theo người dùng

