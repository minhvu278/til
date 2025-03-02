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

# Thử 1 dự án "DEMO BLOG CÁ NHÂN"
- Chúng ta sẽ thử tạo 1 ứng dụng nhỏ blog cá nhân, nơi người dùng có thể xem danh sách các bài viết và thêm bài viết mới

## Chuẩn bị
### Công cụ cần cài đặt
- Node.js
- npm
- VS Code

### Kiến thức cơ bản
- Không cần biết quá nhiều, nhưng nếu quen với JS thì sẽ dễ hơn

## Bước 1: Tạo dự án GrapQL cho server
- Tạo thư mục
```
mkdir my-graphql-blog
cd my-graphql-blog
npm init -y
```
- Cài đặt thư viện cần thiết
```
npm install @apollo/server graphql graphql-tag
```
  - `apollo-server`: Một thư viện giúp chạy server GraphQL dễ dàng
  - `graphql`: Thư viện cốt lõi để xử lý schema và truy vấn
- Cập nhật pakage.json
  - Thêm dòng "type": "module"
- Tạo file server. Tạo 1 file index.js
```ts
import { ApolloServer } from '@apollo/server';
import { startStandaloneServer } from '@apollo/server/standalone';
import { gql } from 'graphql-tag';

// Dữ liệu giả lập
let posts = [
  { id: '1', title: 'Bài viết đầu tiên', content: 'Chào mừng đến với blog!' },
  { id: '2', title: 'Học GraphQL', content: 'Hôm nay học GraphQL rất vui!' },
];

// Định nghĩa schema
const typeDefs = gql`
  type Post {
    id: String!
    title: String!
    content: String!
  }

  type Query {
    posts: [Post!]!
  }

  type Mutation {
    createPost(title: String!, content: String!): Post!
  }
`;

// Định nghĩa resolver
const resolvers = {
  Query: {
    posts: () => posts,
  },
  Mutation: {
    createPost: (parent, args) => {
      const newPost = {
        id: String(posts.length + 1),
        title: args.title,
        content: args.content,
      };
      posts.push(newPost);
      return newPost;
    },
  },
};

// Khởi chạy server
const server = new ApolloServer({ typeDefs, resolvers });

async function startServer() {
  const { url } = await startStandaloneServer(server, {
    listen: { port: 4000 },
  });
  console.log(`Server chạy tại: ${url}`);
}

startServer();
```

## Bước 2: Thử chạy với Apollo Sandbox
### Lấy danh sách posts
- Trong Apollo Sandbox, nhập truy vấn sau
```
query {
  posts {
    id
    title
    content
  }
}
```
- Nhấn run chúng ta sẽ thấy kết quả
```
{
  "data": {
    "posts": [
      {
        "id": "1",
        "title": "Bài viết đầu tiên",
        "content": "Chào mừng đến với blog!"
      },
      {
        "id": "2",
        "title": "Học GraphQL",
        "content": "Hôm nay học GraphQL rất vui!"
      }
    ]
  }
}
```

### Thêm post mới
- Thử gửi mutation
```
mutation {
  createPost(title: "Bài mới", content: "Viết cái gì đó vui vẻ") {
    id
    title
    content
  }
}
```
- Kết quả
```
{
  "data": {
    "createPost": {
      "id": "3",
      "title": "Bài mới",
      "content": "Viết cái gì đó vui vẻ"
    }
  }
}
```
- Chạy lại truy vấn `posts`, bạn sẽ thấy bài viết mới được thêm vào

## Bước 3: Tạo client để gọi GraphQL
- Bây giờ, giả sử bạn muốn làm 1 UI web đơn giản để hiển thị bài post. Chúng ta sẽ dùng HTML, JS để làm
- Tạo file index.html
```html
<!DOCTYPE html>
<html>
<head>
  <title>Blog GraphQL</title>
</head>
<body>
  <h1>Danh sách bài viết</h1>
  <ul id="post-list"></ul>

  <h2>Thêm bài viết</h2>
  <input id="title" placeholder="Tiêu đề" />
  <input id="content" placeholder="Nội dung" />
  <button onclick="addPost()">Thêm</button>

  <script>
    // Hàm lấy danh sách bài viết
    async function fetchPosts() {
      const response = await fetch('http://localhost:4000/graphql', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          query: `
            query {
              posts {
                id
                title
                content
              }
            }
          `,
        }),
      });
      const { data } = await response.json();
      const postList = document.getElementById('post-list');
      postList.innerHTML = '';
      data.posts.forEach(post => {
        const li = document.createElement('li');
        li.textContent = `${post.title}: ${post.content}`;
        postList.appendChild(li);
      });
    }

    // Hàm thêm bài viết
    async function addPost() {
      const title = document.getElementById('title').value;
      const content = document.getElementById('content').value;
      const response = await fetch('http://localhost:4000/graphql', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          query: `
            mutation {
              createPost(title: "${title}", content: "${content}") {
                id
                title
                content
              }
            }
          `,
        }),
      });
      await response.json();
      fetchPosts(); // Cập nhật danh sách sau khi thêm
    }

    // Load bài viết khi mở trang
    fetchPosts();
  </script>
</body>
</html>
```
- Mở thử file trên browser chúng ta sẽ thấy danh sách post và có thể thêm mới nữa

## Bước 4: Hiểu cách nó kết nối
- **Server**: Xử lý schema, resolver và cung cấp endpoint `/graphql`
- **Client**: Gửi query/mutation qua HTTP (ở đây dùng fetch) đến server, nhận dữ liệu & hiển thị
- **Ví dụ thực tế**: Nếu chúng ta làm ứng dụng khoai hơn 1 chút, GraphQL có thể giúp bạn lấy đúng thông tin bài viết (tiêu đề, nội dung) mà không cần load thông tin của author nếu không cần
