# Xử Lý Form Nhập Liệu (Form Handling) Trong Next.js
- **Mục tiêu**: Học cách xử lý form nhập liệu, lưu dữ liệu, gửi dữ liệu lên server

# Tại sao cần xử lý form
- Trong ứng dụng web, form giúp người dùng nhập liệu & gửi dữ liệu lên server
- Ví dụ thực tế
  - Trang đăng ký tài khoản (Email, password)
  - Form bình luận
  - Form đặt hàng
- NextJs cung cấp cách xử lý form đơn giản, hiệu quả

# Tạo form đơn giản trong Next
- **Mục tiêu**: Tạo 1 form nhập tên sản phẩm và mô tả sản phẩm
- Bước 1: Tạo file mới `add/add-product/page.tsx`
- Bước 2: Thêm các đoạn code sau
```tsx
"use client";
import { useState } from "react";

export default function AddProductPage() {
  const [title, setTitle] = useState("");
  const [description, setDescription] = useState("");
  const [message, setMessage] = useState("");

  const handleSubmit = async (event: React.FormEvent) => {
    event.preventDefault(); // Ngăn trang reload

    // Kiểm tra dữ liệu nhập vào
    if (!title || !description) {
      setMessage("Vui lòng nhập đầy đủ thông tin.");
      return;
    }

    // Gửi dữ liệu lên API giả lập
    const response = await fetch("https://jsonplaceholder.typicode.com/posts", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ title, body: description }),
    });

    if (response.ok) {
      setMessage("Sản phẩm đã được thêm thành công!");
      setTitle("");
      setDescription("");
    } else {
      setMessage("Có lỗi xảy ra, vui lòng thử lại.");
    }
  };

  return (
    <div style={styles.container}>
      <h1>Thêm Sản Phẩm Mới</h1>
      <form onSubmit={handleSubmit} style={styles.form}>
        <input
          type="text"
          placeholder="Tên sản phẩm"
          value={title}
          onChange={(e) => setTitle(e.target.value)}
          style={styles.input}
        />
        <textarea
          placeholder="Mô tả sản phẩm"
          value={description}
          onChange={(e) => setDescription(e.target.value)}
          style={styles.textarea}
        />
        <button type="submit" style={styles.button}>Thêm Sản Phẩm</button>
      </form>
      {message && <p style={styles.message}>{message}</p>}
    </div>
  );
}

const styles = {
  container: {
    textAlign: "center",
    padding: "20px",
  },
  form: {
    display: "flex",
    flexDirection: "column",
    gap: "10px",
    maxWidth: "400px",
    margin: "auto",
  },
  input: {
    padding: "10px",
    fontSize: "16px",
  },
  textarea: {
    padding: "10px",
    fontSize: "16px",
    height: "100px",
  },
  button: {
    padding: "10px",
    fontSize: "16px",
    backgroundColor: "#0070f3",
    color: "white",
    border: "none",
    cursor: "pointer",
  },
  message: {
    marginTop: "10px",
    fontSize: "16px",
  },
};
```

# Giải thích code xử lý form
## Các bước xử lý form
- **useState()**: Lưu trữ giá trị nhập vào của tên sản phẩm và mô tả
- **onChange()**: Cập nhật giá trị khi người dùng typing
- **handleSubmit()**
  - Ngăn chặn trang web bị reload - e.preventDefault()
  - Kiểm tra dữ liệu có bị bỏ trống không
  - Gửi dữ liệu lên API (fetch(..., {method: "POST"}))
  - Hiển thị thông báo thành công hoặc lỗi
