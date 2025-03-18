# Fetch Dữ Liệu Từ API Trong Next.js
- **Mục tiêu**: Học cách lấy dữ liệu từ API thay vì mock

# Tại sao cần fetch dữ liệu từ API
- Trong phần trước, chúng ta đã sử dụng mảng tĩnh để lưu thông tin sản phẩm. Nhưng trong thực tế, dữ liệu thường nằm trên backend hoặc server
- Ví dụ thực tế
  - Website bán hàng cần lấy danh sách sản phẩm từ backend
  - Một ứng dụng tin tức cần lấy bài viết mới nhất từ server
- Để làm điều này, chúng ta cần dùng `fetch()` để lấy dữ liệu từ API

# Cách fetch dữ liệu từ API
- Lấy dữ liệu từ 1 API giả lập để hiển thị sản phẩm

## Tạo API giả lập bằng JSONPlaceholder
- JSONPlaceholder là 1 api free giúp chúng ta test dữ liệu
- API test 
```
https://jsonplaceholder.typicode.com/posts
```
- Mỗi post sẽ đóng vai trò như 1 sản phẩm (title='tên sản phẩm', body='mô tả')

## Sửa trang product để fetch dữ liệu từ API
- Mở file `app/product/[id]/page.tsx` và thay thế bằng đoạn code sau
```tsx
type ProductPageProps = {
  params: { id: string };
};

export default async function ProductPage({ params }: ProductPageProps) {
  const res = await fetch(`https://jsonplaceholder.typicode.com/posts/${params.id}`);
  const product = await res.json();

  if (!product || !product.id) {
    return <h1 style={{ textAlign: "center" }}>Sản phẩm không tồn tại</h1>;
  }

  return (
    <div style={styles.container}>
      <h1>{product.title}</h1>
      <p>{product.body}</p>
    </div>
  );
}

const styles = {
  container: {
    textAlign: "center",
    padding: "20px",
    fontSize: "18px",
  },
};
```

# Fetch danh sách sản phẩm
- **Mục tiêu**: Thay vì xem 1 sản phẩm, chúng ta sẽ hiển thị danh sách sản phẩm trên trang `/product`
- Bước 1: Mở thư mục `app/product` và tạo file page.tsx
- Bước 2: Thêm code
```tsx
import Link from "next/link";

export default async function ProductList() {
  const res = await fetch("https://jsonplaceholder.typicode.com/posts");
  const products = await res.json();

  return (
    <div style={styles.container}>
      <h1>Danh sách sản phẩm</h1>
      <ul style={styles.list}>
        {products.slice(0, 10).map((product: any) => (
          <li key={product.id} style={styles.item}>
            <Link href={`/product/${product.id}`}>{product.title}</Link>
          </li>
        ))}
      </ul>
    </div>
  );
}

const styles = {
  container: {
    textAlign: "center",
    padding: "20px",
  },
  list: {
    listStyle: "none",
    padding: 0,
  },
  item: {
    marginBottom: "10px",
  },
};
```
- Qua các bước trên, trang của bạn đã hoạt động như 1 website thực tế

# Summary
- Cách fetch dữ liệu từ API bằng `fetch()`
- Cách hiển thị sản phẩm từ API thay vì dữ liệu tĩnh
- Cách hiển thị danh sách sản phẩm và liên kết đến trang chi tiết
