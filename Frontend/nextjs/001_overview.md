# Hiểu về NextJs và cách cài đặt
- **Mục tiêu**: Biết NextJs là gì, tại sao dùng Next thay cho React, cách tạo dự án NextJs đầu tiên

## NextJs là gì
- Là 1 framework dựa trên React, giúp xây dựng các ứng dụng web nhanh hơn, tối ưu hơn và dễ quản lý hơn. Nó cung cấp nhiều tính năng mạnh mẽ như
  - **Server-side rendering (SSR)**: Render trang trên server trước khi gửi về browser, giúp load nhanh hơn
  - **Static site generation (SSG)**: Tạo trang tĩnh để load cực nhanh
  - **API Routers**: Tạo backend trong NextJs mà không cần server riêng như Express hoặc NestJs

## Cài đặt NextJs
- Cần có `Node` trong máy
- Cài bằng lệnh sau
```bash
npx create-next-app@latest my-next-app
cd my-next-app
npm run dev
```
- Cách này sẽ tạo 1 dự án Next và chạy nó trên `localhost:3000`

# Kiến thức cơ bản
- **Mục tiêu**: Hiểu cách tổ chức file, component, trang trong NextJs

## Cấu trúc thư mục
- `/app`: Chứa toàn bộ trang web (Dùng trong App Router - NextJs 13+)
- `/components`: Chứa các thành phần giao diện (Button, navbar,...)
- `/public`: Chứa ảnh, favicon, file tĩnh
- `/style`: Chứa file CSS

## Tạo trang tĩnh với NextJs
- Trong thư mục `/app`, mỗi file `.tsx` sẽ tự động trở thành 1 trang (Không cần router thủ công như React)
```ts
export default function Home() {
  return <h1>Chào mừng đến với Next.js!</h1>;
}
```
- Truy cập `localhost:3000` sẽ hiển thị nội dung này

## Tạo component NextJs
- NextJs sử dụng component giống React
```ts
function Button() {
  return <button>Bấm vào đây</button>;
}

export default Button;
```
- Có thể import vào trang
```ts
import Button from "@/components/Button";

export default function Home() {
  return <Button />;
}
```

# Routing trong Next
- **Mục tiêu**: Hiểu cách điều hướng giữa các trang web

## Tạo nhiều trang
- Nếu bạn có file `/app/about/page.tsx`, truy cập vào `localhost:3000/about` sẽ hiển thị nội dung đó
- Chuyển trang với `<Link>` thay vì dung `<a href="/">`
```ts
import Link from "next/link";

export default function Home() {
  return (
    <div>
      <h1>Trang chủ</h1>
      <Link href="/about">Đi đến trang About</Link>
    </div>
  );
}
```

# Server-side Redering (SSR) và Static Site Generation (SSG)
- **Mục tiêu**: Hiểu sự khác nhau giữa SSR và SSG để tối ưu website

## SSR - Render trên server mỗi lần có request
- Sử dụng `async function` trong NextJs
```ts
export default async function Page() {
  const res = await fetch("https://jsonplaceholder.typicode.com/posts/1");
  const data = await res.json();

  return <div>{data.title}</div>;
}
```
- Dữ liệu được fetch mỗi khi người dùng vào trang

## SSG - Render trước khi build website
- Sử dụng `generateStaticParams` để lấy dữ liệu 1 lần
```ts
export async function generateStaticParams() {
  const res = await fetch("https://jsonplaceholder.typicode.com/posts");
  const posts = await res.json();
  return posts.map((post) => ({ id: post.id.toString() }));
}
```
- SSG giúp trang web tải nhanh hơn

## API Routes - Viết BE trong NextJs
- **Muc tiêu**: Hiểu cách NextJs có thể thay thế Express hoặc NextJs để tạo API

## Tạo API endpoint
- NextJs cho phép tạo API trong `/app/api`
```ts
export async function GET() {
  return Response.json({ message: "Hello from API!" });
}
```
- Truy cập `localhost:3000/api/hello` sẽ trả về
```js
{ "message": "Hello from API!" }
```

## Xử lý dữ liệu trong API
- Có thể lấy dữ liệu từ database hoặc xử lý form
```js
export async function POST(req) {
  const body = await req.json();
  return Response.json({ received: body });
}
```
- Gửi dữ liệu từ FE sẽ nhận được phản hồi

# Quản lý state và tương tác với server
- **Mục tiêu**: Hiểu cách dùng useState, useEffect và fetch API
- Sử dụng useState
```js
import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Tăng</button>
    </div>
  );
}
```
- Fetch API với useEffect
```js
import { useEffect, useState } from "react";

export default function FetchData() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/posts/1")
      .then((res) => res.json())
      .then((data) => setData(data));
  }, []);

  return <div>{data?.title}</div>;
}
```

# Authentication & Authorization
- **Mục tiêu**: Học cách đăng nhập, đăng xuất, bảo vệ route

## Sử dụng NextAuth.js để xác thực
- NextAuth giúp dễ dàng đăng nhập bằng Google, Facebook,...
```js
import { getServerSession } from "next-auth";

export default async function Page() {
  const session = await getServerSession();
  return session ? <p>Chào {session.user.name}</p> : <p>Vui lòng đăng nhập</p>;
}
```

## Bảo vệ route chỉ cho user đăng nhập
```js
export default function ProtectedPage() {
  const session = useSession();
  if (!session) return <p>Bạn chưa đăng nhập!</p>;
  return <p>Chào {session.user.name}, bạn có thể xem nội dung này.</p>;
}
```

# Kết hợp NextJs với BE
- **Mục tiêu**: Hiểu cách kết nối NextJs với BE để thuận tiện lưu dữ liệu
- Gửi request từ FE đến NestJs
```js
async function getData() {
  const res = await fetch("http://localhost:3000/api/users");
  const users = await res.json();
  return users;
}
```
- Xử lý dữ liệu trên BE (NestJs)
```js
@Get()
findAll() {
  return this.userService.findAll();
}
```

# Summary
- Học cách tạo trang, component, route trong NextJs
- Hiểu cách NextJs render dữ liệu với SSR, SSG
- Viết API trong NextJs hoặc kết nối với BE khác
- Quản lý state với useState, useEffect và fetch API
- Xác thực đăng nhập với NextAuth
- Bảo mật và tối ưu hiệu suất ứng dụng NextJs
