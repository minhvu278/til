# Navigation
- **Mục tiêu**: Học cách tạo menu điều hướng giúp người dùng di chuyển giữa các trang trong NextJs

# Tại sao cần menu điều hướng
- Hãy tưởng tượng bạn đang truy cập 1 website bán hàng. Nếu không có menu, bạn phải gõ URL thủ công mỗi lần muốn xem danh mục sản phẩm, giỏ hàng hoặc trang liên hệ
- Menu điều hướng giúp bạn chuyển trang dễ dàng chỉ bằng 1 cú click
- Trong NextJS, chúng ta sẽ sử dụng `Link` từ `next/link` để tạo menu mà không cần tải lại trang (Giống như ứng dụng di động, mượt hơn)

# Cách tạo navigation trong Next
- **Mục tiêu**: Tạo navigation đơn giản giúp chuyển giữa **Home** và **About**
## Tạo component Menu
- Bước 1: Mở thư mục `src/components` (Nếu chưa có thì tạo mới)
- Bước 2: Trong components, tạo file `Navbar.tsx`
- Bước 3: Mở file Navbar lên và thêm code
```ts
import Link from "next/link";

export default function Navbar() {
  return (
    <nav style={styles.navbar}>
      <ul style={styles.navList}>
        <li style={styles.navItem}>
          <Link href="/">Trang Chủ</Link>
        </li>
        <li style={styles.navItem}>
          <Link href="/about">Giới Thiệu</Link>
        </li>
      </ul>
    </nav>
  );
}

const styles = {
  navbar: {
    backgroundColor: "#0070f3",
    padding: "10px",
  },
  navList: {
    listStyle: "none",
    display: "flex",
    justifyContent: "center",
    gap: "20px",
    padding: 0,
    margin: 0,
  },
  navItem: {
    color: "white",
    fontSize: "18px",
  },
};
```

## Thêm navbar vào app
- Bước 1: Mở file `app/layout.tsx`
- Bước 2: Import component Navbar và đặt nó vào layout như sau
```ts
import Navbar from "../components/Navbar";

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="vi">
      <body>
        <Navbar /> {/* Thêm menu ở đây */}
        {children}
      </body>
    </html>
  );
}
```
## Chạy thử
- Hãy mở lên và chạy thử, chuyển đổi giữa Home và about
- Đặc biệt là khi chuyển trang sẽ không bị load lại
- Next chỉ thay đổi nội dung cần thiết, giúp tốc độ nhanh hơn

# Summary
- Cách tạo menu điều hướng bằng Link
- Cách tạo component Navbar và sử dụng `layout.tsx`
- Cách tạo CSS để làm đẹp menu
