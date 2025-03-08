# Kỹ năng tầm trung với Playwright
- Sau khi đã nắm được các khái niệm cơ bản như cài đặt, mở browser, redirect page, screenshot - chúng ta cần nâng cao kỹ năng để xử lý các tình huống phức tạp hơn

# Async/Await (Xử lý bất đồng bộ)
- PL sử dụng mô hình bất đồng bộ (asynchronous) vì các thao tác với trình duyệt (Như load trang, click, điền form) cần thời gian. Js dùng `async/await` để quản lý các tác vụ này
## Tại sao cần hiểu bất đồng bộ?
- Nếu không dùng đúng, script có thể chạy trước khi trang load xong, dẫn đến lỗi
- Ví dụ cơ bản
```js
const { chromium } = require('playwright');

(async () => {
  const browser = await chromium.launch();
  const page = await browser.newPage();
  await page.goto('https://example.com');
  console.log('Trang đã tải xong!');
  await browser.close();
})();
```
- Ví dụ nâng cao
```js
const { chromium } = require('playwright');

(async () => {
  const browser = await chromium.launch();
  const page = await browser.newPage();
  await page.goto('https://example.com');
  await page.waitForSelector('h1'); // Chờ thẻ <h1> xuất hiện
  const title = await page.textContent('h1');
  console.log('Tiêu đề:', title);
  await browser.close();
})();
```
- **Mẹo**: Luôn dùng `await` trước các hàm trả về Promise (như goto, click, waitForSelector) trong hàm `async`

# Locators nâng cao
- Locators là cách PL tìm và tương tác với các phần tử trên trang. Cần biết các chọn phần tử linh hoạt & xử lý các trang web động
- **CSS Selectors**
  - Chọn theo ID: `#id`
  - Chọn theo class: `.class`
  - Chọn theo thuộc tính: `[attribute=value]`
- **Text-based Locators**: Chọn phần tử dựa trên nội dung văn bản
- **XPath**: Dùng khi CSS không đủ mạnh
- Ví dụ
