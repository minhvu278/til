# Playwright là gì?
- Là 1 thư viện automation testing mạnh mẽ , giúp kiểm thử giao diện web trên nhiều trình duyệt khác nhau như `Chromium, Firefox, Webkit`

## Ưu điểm của Pl
- Hỗ trợ trình duyệt đa nền tảng
- Chạy test song song, nhanh hơn Selenium
- Có thể kiểm thử cả web và mobile emulator
- Hỗ trợ mock api và chặn request

## So sánh với Selenium
```js
Tiêu chí	Playwright	Selenium
Đa trình duyệt	✅ Chromium, Firefox, WebKit	✅ Chrome, Firefox, Safari, Edge
Chạy song song	✅ Rất tốt	❌ Chậm hơn
Hỗ trợ Mobile	✅ Có giả lập	❌ Không có sẵn
Mock API	✅ Có hỗ trợ	❌ Không hỗ trợ
```

# Cài đặt môi trường
## B1: Cài đặt NodeJs (nếu chưa có)
- Tải nodejs từ trang chủ

## B2: Cài đặt Pl
- Mở terminal và chạy lệnh sau
```sh
npm init playwright@latest
```
- Chọn các option
  - Chọn Ts hoặc Js
  - Cài đặt browser: `Yes`
  - Cấu hình Github Actions: `No` (Có thể thêm sau)
- Sau khi cài xong, kiểm tra bằng lệnh
```js
npx playwright test --help
```

# Chạy test mẫu
- Playwright đã tự tạo sẵn 1 số test mẫu. Bạn có thể chạy thử bằng lệnh
```js
npx playwright test
```
- Mở báo cáo test
```js
npx playwright show-report
```
