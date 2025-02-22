# Hiểu và tổng quan về Playwright
- Playwright là gì? (Thư viện automation testing hộ trợ đa trình duyệt: Chromium, Firefox, Webkit)
- So sánh với Selenium và Cypress
- Cách Playwright hoạt động (cơ chế không headless, handless, execution context,...)

# Cài đặt và thiết lập môi trường
- Cài đặt Nodejs
- Cài đặt Playwright
```sh
npm init playwright@latest
```
- Chạy thử 1 mẫu test
```sh
npx playwright test
```

# Viết script đơn giản để điều khiển trình duyệt
- Mở trang web, nhập dữ liệu vào input , click vào button
```js
const { chromium } = required('playwright')

(async () => {
  const brower = await chromium.launch();
  const page = await browser.newPage();
  await page.goto('https://example.com');
  await page.fill('#username', 'admin');
  await page.click('#login-button');
  await browser.close();
})();
```
- Chạy script
```js
node test.js
```

# Học cách viết test cases
- Dùng Playwright Test Runner
- Cấu trúc 1 file test trong Playwright
```js
import { test, expect } from '@playwright/test'

test('Login thanh cong', async ({ page }) => {
  await page.goto('https://example.com');
  await page.fill('#username', 'admin');
  await page.fill('#password', 'password123');
  await page.click('#login-button');
  await expect(page.locator('#welcome-message')).toContainText('Welcome')
})
```
- Chạy test
```node
npx playwright test
```
# Làm việc với các thành phần web
- Chờ (waiting strategies): `waitForSelector`, `waitForLoadState`
- Tương tác với các phần tử
  - Click, nhập dữ liệu, chọn dropdown
  - Xử lý iframe, popup, dialog

# Chạy test trên nhiều browser
- Cấu hình chạy test trên nhiều browser
```js
use: { browserName: 'chromium' } // Hoặc các browser khác như firefox, webkit
```
- Chạy test trên Chromium, Firefox, Webkit
```js
npx playwright test --browser=firefox
```

# Tích hợp CI/CD và báo cáo kết quả
- Tạo report với `allure-playwright` hoặc Playwright HTML report
- Tích hợp Playwright và Github Actions, Jenkins

# Mock API và làm việc với Network
- Chặn request & mock dữ liệu
```js
await page.route('https://api.example.com/user', async route => {
  await route.fulfill({ json: { id: 1, name: 'Tesst User'}})
})
```
- Xử lý upload và download

# Lộ trình để trở thành chuyên gia
## Kiến thức cơ bản
- **Mục tiêu**: Hiểu tổng quan về Playwright, cách cài đặt & chạy test cơ bản
- Playwright là gì? Tại sao lại chọn Playwright thay vì Selenium, Cypress?
- Cài đặt môi trường (NodeJs, Playwright, VS Code, Playwright Test Runner)
- Viết script đơn giản: Mở trang web, nhập dữ liệu, click button
- Chạy web trên nhiều browser
- Tìm hiểu về **headless mode** và **headed mode***
- **Bài tập thực hành**: Viết script đăng nhập vào 1 trang web, kiểm tra nội dung sau khi đăng nhập

## Làm chủ các API của Playwright (Intermediate)
- **Mục tiêu**: Sử dụng thành thạo các API để thao tác với giao diện web
- Xử lý các phần tử web
  - `page.click(), page.fill(), page.selectOption(), page.waitForSelector()`,...
  - Làm việc với iframe, popup, modal
  - Xử lý alerts, confirm, prompt
  - Upload, download file
  - Chạy test trên nhiều trình duyệt cùng lúc
- **Bài tập thực hành**: Viết test tự động đăng nhập, điền form, chọn dropdown và tải file

## Viết testcase chuyên nghiệp (Intermediate - Advanced)
- **Mục tiêu**: Viết test chuẩn theo best practices, giảm flakiness (test không ổn định)
- Sử dụng locators hiệu quả: `page.locator()`, `getByRole()`, `getByText()`, `getByTestId()`
- Viết test có độ tin cậy cao, tránh flakiness bằng `waitForLoadState()`
- Chạy test song song (parallel testing) để tăng tốc độ
- Xử lý retry test khi thất bại
- Tạo báo cáo test với HTML Report và Allure Report
- **Bài tập thực hành**: Viết bộ test kiểm thử giao diện của 1 trang web phức tạp với nhiều popup, AJAX request

## Làm chủ Mock API & Network Testing (Advanced)
- **Mục tiêu**: Hiểu cách chặn request, mock API để test nhanh hơn
- Chặn API request bằng `page.route()`
- Giả lập response JSON cho API để kiểm thử offline
- Kiểm tra request và response bằng `page.waitForResponse()`
- **Bài tập thực hành**: Tạo 1 bộ test kiểm thử FE mà không cần BE bằng cách mock API

## Tích hợp Playwright vào CI/CD (Expert)
- **Mục tiêu**: Tích hợp Playwright vào pipeline CI/CD để chạy test tự động
- Chạy Playwright trong Docker
- Cấu hình Playwright trong Github action, Gitlab CI/CD, Jenkins
- Gửi report test tự động qua Slack, Email
- Chạy test trên Cloud với Playwright Test Runner
- **Bài tập thực hành**: Thiết lập Github Actions để chạy Playwright sau mỗi lần push code

## Viết test trên thiết bị Mobile & API Testing (Expert)
- **Mục tiêu**: Kiểm thử trên mobile và kiểm thử API backend
- Chạy test trên Iphone, Android (Chế độ giả lập mobile)
- Kiểm thử API backend bằng Playwright
- **Bài tập thực hành**: Viết test đăng nhập trên giao diện mobile & kiểm tra phản hồi API

## Tạo Framework kiểm thử tự động hoàn chỉnh (Master level)
- **Mục tiêu**: Tạo 1 framework Playwright hoàn chỉnh cho dự án lớn
- Tạo cấu trúc test có thể tái sử dụng: Page Object Model (POM)
- Viết custom helper function để giảm lặp code
- Viết custom reporter gửi kết quả test qua Slack
- Sử dụng Typescript để code mạnh hơn
- **Bài tập thực hành**: Xây dựng 1 framework test hoàn chỉnh cho 1 trang web lớn

# Summary
- Nếu học theo lộ trình này sẽ đạt được:
  - Thành thạo Playwright từ cơ bản đến nâng cao
  - Viết test tự động chuyên nghiệp, tối ưu hiệu suất
  - Tích hợp test vào quy trình DevOps (CI/CD)
  - Xây dựng framework test hoàn chỉnh cho dự án thực tế
