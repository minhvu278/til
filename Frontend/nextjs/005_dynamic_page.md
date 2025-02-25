# Tạo Trang Động (Dynamic Pages) Trong Next.js
- **Mục tiêu**: Học cách tạo trang có nội dung thay đổi linh hoạt theo tham số URL

# Trang động là gì?
- Bình thường, mỗi file trong thư mục `app/` tương ứng với 1 file cố định (VD /about, /contact)
- Nhưng đôi khi, chúng ta cần tạo 1 trang có nội dung thay đổi theo tham số URL, Ví dụ
  - http://localhost:3000/product/1 → Hiển thị sản phẩm số 1.
  - http://localhost:3000/product/2 → Hiển thị sản phẩm số 2.
- Thay vì tạo thủ công `product-1.tsx`, `product-2.tsx`,..., chúng ta có thể dùng `Dynamic Routing` để tạo 1 trang động có thể hiển thị nhiều sản phẩm khác nhau

# Cách tạo trang động trong Next
- Tạo 1 trang chi tiết sản phẩm (`product/:id)` để hiển thị bất kỳ sản phẩm nào

## Tạo thư mục và file động
- Bước 1: Mở thư mục `app/` và tạo 1 thư mục có tên là `product`
- Bước 2: Trong thư mục product, tạo 1 thư mục có tên là `[id]` (Chú ý dấu [])
  - `[]` là cách Next nhận diện 1 trang động  (Dynamic Page)
- Bước 3: Trong [id], tạo 1 file mới có tên là `page.tsx`

## Viết code để lấy tham số động
- Mở file `app/product/[id]/page.tsx` và thêm đoạn code sau
```tsx
type ProductPageProps = {
  params: { id: string };
};

export default function ProductPage({ params }: ProductPageProps) {
  return (
    <div style={styles.container}>
      <h1>Chi tiết sản phẩm</h1>
      <p>Đây là thông tin của sản phẩm có ID: {params.id}</p>
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
- `params: { id: string }`: NextJs tự động lấy giá trị id từ URL
- `{params.id}`: Hiển thị giá trị ID của sản phẩm trên trang
- Nếu bạn vào `http://localhost:3000/product/10`, nó sẽ hiển thị
```
Đây là thông tin của sản phẩm có ID: 10
```

## Kiểm tra trang động 
- Mở trình duyệt và thử nhập các URL
- Bạn sẽ thấy trang hiển thị đúng ID theo URL

# Dữ liệu mock: Hiển thị chi tiết sản phẩm
- **Mục tiêu**: Thay vì chỉ hiển thị ID, chúng ta sẽ lấy thông tin sản phẩm từ danh sách mock
- Trong `app/product/[id]/page.tsx`
```tsx
type ProductPageProps = {
  params: { id: string };
};

const products = [
  { id: "1", name: "iPhone 15", price: "25,000,000 VND" },
  { id: "2", name: "MacBook Pro", price: "50,000,000 VND" },
  { id: "3", name: "Apple Watch", price: "12,000,000 VND" },
];

export default function ProductPage({ params }: ProductPageProps) {
  const product = products.find((p) => p.id === params.id);

  if (!product) {
    return <h1 style={{ textAlign: "center" }}>Sản phẩm không tồn tại</h1>;
  }

  return (
    <div style={styles.container}>
      <h1>{product.name}</h1>
      <p>Giá: {product.price}</p>
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

# Summary
- Cách tạp trang động bằng [id]
- Cách lấy tham số từ URL bằng `params.id`
- Cách hiển thị dữ liệu động dựa trên ID sản phẩm
- Cách xử lý trường hợp nếu không thấy dữ liệu