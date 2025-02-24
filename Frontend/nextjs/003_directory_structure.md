# Cấu trúc thư mục và cách tạo trang đầu tiên trong Next.js
- **Mục tiêu**: Hiểu cách NextJs tổ chức thư mục và tạo trang web đầu tiên

##\ Hiểu về cấu trúc thư mục của Next
- Sau khi cài đặt xong, bạn sẽ thấy cấu trúc thư mục sẽ như sau
```
my-next-app
│── node_modules/        # Thư viện cài đặt từ npm
│── public/              # Chứa ảnh, favicon, các file tĩnh
│── src/                 # Chứa code chính của ứng dụng
│   │── app/             # Chứa các trang của Next.js (khi dùng App Router)
│   │── components/      # Chứa các component dùng chung
│   │── styles/          # Chứa file CSS để thiết kế giao diện
│── .gitignore           # File giúp bỏ qua các file không cần khi push code
│── package.json         # File chứa thông tin về dự án và các thư viện đã cài đặt
│── next.config.js       # File cấu hình cho Next.js
│── README.md            # File hướng dẫn sử dụng dự án
```

# Cách tạo trang web đầu tiên
- **Mục tiêu**: Tạo 1 trang web mới trong NextJs và hiển thị nội dung trên trình duyệt

## Cách NextJs tạo ra trang web như thế nào
- Trong NextJs, mỗi file trong thư mục `/app` sẽ tự động trở thành 1 trang web
- **Ví dụ thực tế**:
- Hãy tưởng tượng `/app` giống như một thư mục trên máy tính của bạn
  - Nếu bạn tạo file `app/about/page.tsx` thì nó sẽ xuất hiện trên trình duyệt là `http://localhost:3000/about`
  - Nếu bạn tạo file `app/about/contact.tsx` thì nó sẽ xuất hiện trên trình duyệt là `http://localhost:3000/contact`

## Tạo trang "Giới thiệu" (About page)
- Bây giờ chúng ta sẽ tạo ra 1 trang mới trong NextJs
- **Bước 1**: Mở thư mục `app/` và tạo thư mục mới có tên là `about/`.
- **Bước 2**: Trong thư mục `about/`, tạo 1 file có tên `page.tsx`.
- **Bước 3**: Mở thư mục page.tsx và nhập nội dung sau
```js
export default function AboutPage() {
  return (
    <div>
      <h1>Giới thiệu về chúng tôi</h1>
      <p>Chào mừng bạn đến với trang web của chúng tôi! Đây là trang giới thiệu.</p>
    </div>
  );
}
```

## Chạy thử trang mới
- Sau khi tạo xong trang, bạn mở trình duyệt và nhập
```sh
http://localhost:3000/about
```
- Bạn sẽ thấy trang `Giới thiệu về chúng tôi` sẽ xuất hiện

# Cách thêm CSS để làm đẹp trang web
- **Mục tiêu**: Thêm CSS vào NextJs để trang web trông đẹp hơn
- Bước 1: Mở thư mục `src/styles/` và tìm file `globals.css`
- Bước 2: Thêm CSS vào
```css
body {
  font-family: Arial, sans-serif;
  background-color: #f8f9fa;
  margin: 0;
  padding: 0;
}

h1 {
  color: #0070f3;
  text-align: center;
}

p {
  text-align: center;
  font-size: 18px;
}
```
- Bước 3: Mở trang web lên sẽ thấy trang đẹp hơn

# Summary
- Hiểu cấu trúc thư mục trong NextJs
- Biết cách tạo 1 trang mới trong NextJs
- Biết cách thêm CSS để trang web trông đẹp hơn
