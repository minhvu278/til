# Viết Script Playwright Đầu Tiên

# Playwright script là gì?
- Một script trong PL là một đoạn code giúp tự động hoá các thao tác trên trình duyệt như
  - Mở trang web
  - Nhập dữ liệu vào form
  - Click vào nút
  - Kiểm tra nội dung trên trang
- Có thể hình dung script trong PL giống như 1 con robot ảo, có thể thao tác như 1 người dùng thật

# Cài đặt Playwright
## Bước 1: Tạo 1 dự án mới
- Mở terminal và chạy
```sh
mkdir playwright-demo  # Tạo thư mục dự án
cd playwright-demo  # Di chuyển vào thư mục
```

## Bước 2: Khởi tạo dự án
```sh
npm init -y  # Tạo file package.json
```
## Bước 3: Cài đặt Playwright
```sh
npm i -D @playwright/test  # Cài đặt Playwright
```
- Lệnh này sẽ tải thư viện Playwright để bạn có thể chạy test tự động

## Bước 4: Cài đặt browser
- Sau khi cài đặt Playwright, bạn cần download các browser để chạy test
```sh
npx playwright install
```
- Lệnh này sẽ tải về Chromium, FireFox, Webkit để test trên nhiều browser khác nhau

# Viết script đầu tiên
- Viết 1 đoạn script để
  - Mở trình duyệt
  - Truy cập trang web
  - Chụp ảnh màn hình
```js
const { chromium } = require('playwright'); // Import Playwright

(async () => {
    // Mở trình duyệt Chromium
    const browser = await chromium.launch({ headless: false });

    // Mở tab mới
    const page = await browser.newPage();

    // Truy cập trang web
    await page.goto('https://example.com');

    // Chụp ảnh màn hình và lưu thành file screenshot.png
    await page.screenshot({ path: 'screenshot.png' });

    // Đóng trình duyệt
    await browser.close();
})();
```
- Chạy script này bạn sẽ thấy trình duyệt mở lên, truy cập trang web, chụp ảnh màn hình rồi tự động tắt

# Tự động nhập dữ liệu và click
- Bâu giờ hãy viết script tự động nhập dữ liệu vào form và click nút đăng nhập

## Bước 1: Tạo script login
- Tạo file login.js và thêm code
```ts
const { chromium } = require('playwright');

(async () => {
    const browser = await chromium.launch({ headless: false });
    const page = await browser.newPage();
    
    // Mở trang web
    await page.goto('https://example.com/login');

    // Nhập email
    await page.fill('#email', 'user@example.com');

    // Nhập mật khẩu
    await page.fill('#password', 'password123');

    // Click nút đăng nhập
    await page.click('#login-button');

    // Đóng trình duyệt
    await browser.close();
})();
```
- Chạy `node login.js` để test

# Kiểm tra kết quả (Assertions)
- Giả sử bạn muốn kiểm tra sau khi đăng nhập, trang web có đổi URL không
```js
const { expect } = require('@playwright/test');

(async () => {
    const browser = await chromium.launch({ headless: false });
    const page = await browser.newPage();
    
    await page.goto('https://example.com/login');

    await page.fill('#email', 'user@example.com');
    await page.fill('#password', 'password123');
    await page.click('#login-button');

    // Kiểm tra xem có chuyển sang trang dashboard không
    await expect(page).toHaveURL('https://example.com/dashboard');

    await browser.close();
})();
```
- Nếu URL không đúng, script sẽ báo lỗi