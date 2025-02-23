# Viết test case chuyên nghiệp
- Phần này chúng ta sẽ học
  - Cách tổ chức file testcase đúng chuẩn
  - Viết test đảm bảo tính ổn định và đáng tin cậy
  - Cách sử dụng `locators` để tìm phần tử UI
  - Chạy test song song để tăng tốc
  - Tạo report kết quả trước khi

# Cấu trúc test trong Playwright
## Test case là gì
- Là 1 tập hợp các bước kiểm thử để đảm bảo 1 tính năng hoạt động đúng. Ví dụ
  - `Test case đăng nhập`: Kiểm tra xem người dùng có đăng nhập vào hệ thống không
  - `Test case tìm kiếm sản phẩm`: Kiểm tra xem khi nhập từ khoá vào ô tìm kiếm, danh sách sản phẩm hiển thị đúng không
- Trong PL, chúng ta sẽ sử dụng **Playwright Test** để viết test case thay vì tự tạo script như ở phần 2

# Tạo file test đầu tiên
- Tạo file test - Mở thư mục dự án, vào thư mục `tests/`, tạo file `login.spec.js`
- Định dạng file `.spec.js` giúp PL tự nhận diện file test

## Viết test đơn giản
```js
// Import thư viện Playwright Test
const { test, expect } = require('@playwright/test');

// Định nghĩa test case
test('Kiểm tra đăng nhập thành công', async ({ page }) => {
    // Mở trình duyệt và truy cập trang login
    await page.goto('https://example.com/login');

    // Nhập email và mật khẩu
    await page.fill('#email', 'user@example.com');
    await page.fill('#password', 'password123');

    // Click nút đăng nhập
    await page.click('#login-button');

    // Kiểm tra xem có chuyển đến trang dashboard không
    await expect(page).toHaveURL('https://example.com/dashboard');
});
```
- Chạy test trên terminal, chạy lệnh
```sh
npx playwright test login.spec.js
```
- Nếu test thành công, bạn sẽ thấy kết quả
```
✓ Kiểm tra đăng nhập thành công (passed)
```
- Nếu thất bại, chúng ta sẽ thấy lỗi mô tả vấn đề

# Cách viết test đáng tin cậy (Avoid Flaky Test)
## Vấn đề với test không ổn định
- Giả sử bạn viết 1 test case kiểm tra xem 1 sản phẩm có hiển thị trên trang web không. Nhưng thỉnh thoảng test thành công và thỉnh thoảng sẽ thất bại vì:
  - Trang web load chậm, PL tìm phần tử khi nó chưa hiển thị
  - Request API chưa hoàn thành, dữ liệu chưa xuất hiện
- Để khắc phục, chúng ta cần sử dụng `waitForSelector` hoặc `waitForLoadState`
### VD 1: Test bị lỗi do không chờ phần tử xuất hiện
```js
await page.click('#search-button');
await page.click('.product-item');  // ❌ Lỗi nếu sản phẩm chưa load xong
```
- Cách sửa đúng
```js
await page.click('#search-button');
await page.waitForSelector('.product-item');  // ✅ Đợi sản phẩm hiển thị
await page.click('.product-item');
```
### VD 2: Chờ trang web tải xong
```js
await page.waitForLoadState('networkidle'); // ✅ Chờ tất cả request hoàn thành
```

# Tìm phần tử UI chính xác (Locators)
- Cách tìm phần tử UI (Selector). Có nhiều cách để tìm phần tử trong PL
```
ID (#id) | VD: #username - Dùng khi có ID duy nhất
Class (.class) | VD: .button-primary - Dùng khi class không bị trùng
Text(getByText()) | VD: getByText('Đăng nhập') - Dùng khi button có nội dung rõ ràng
Role (getByRole()) | VD: getByRole('button', {name: 'Đăng nhập'}) - Dùng khi muốn đảm bảo tính truy cập
```
- Ví dụ chọn phần tử bằng nhiều cách
```ts
await page.fill('#username', 'admin');  // Bằng ID
await page.click('.login-button');  // Bằng class
await page.click('text="Đăng nhập"');  // Bằng nội dung text
await page.getByRole('button', { name: 'Đăng nhập' }).click();  // Bằng role
```
- Tốt nhất nên dùng `getByRole()` để test không bị ảnh hưởng khi UI thay đổi

# Chạy test song song để tăng tốc
- **Vấn đề**: Nếu có 100 test, chạy từng test 1 sẽ mất nhiều thời gian
- **Giải pháp**: PL hỗ trợ chạy test song song tự động
- Chạy test song song trên 3 browser
```ts
npx playwright test --workers=3
```
- Lệnh này giúp tăng tốc test lên gấp 3 lần
- Chúng ta cũng có thể chạy với `--workers=2` và `--workers=4` để so sánh thời gian

# Tạo report kết quả khi test
- Sau khi chạy test, bạn có thể xem báo cáo HTML để phân tích lỗi
- Tạo report HTML
```sh
npx playwright test --reporter=html
```
- Mở report
```sh
npx playwright show-report
```
- Bạn sẽ thấy UI trực quan

# Summary
- Qua bài này chúng ta đã tìm hiểu được
  - Cách viết test theo chuẩn Playwright Test
  - Tránh lỗi test không ổn định bằng `waitForSelector()`
  - Chọn các phần tử UI chính xác bằng `getByRole()`
  - Chạy test song song để tăng tốc
  - Xem báo cáo test trực quan

