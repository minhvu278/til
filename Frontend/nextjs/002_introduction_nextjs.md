# NextJs là gì?
- **Mục tiêu**: Hiểu NextJs là gì, tại sao dùng và nó khác gì so với các công nghệ khác

## Ví dụ thực tế
- Hãy tưởng tượng bạn muốn mở 1 **cửa hàng bán quần áo online**. Bạn có 2 cách để hiển thị sản phẩm trên website
- **Cách 1: Truyền thống (Client-side Rendering - CSR)**
  - Khi người dùng vào trang web, họ sẽ thấy 1 màn hình trắng, và trình duyệt sẽ gửi yêu cầu lên server để lấy dữ liệu
  - Khi có dữ liệu, trang web mới hiển thị đầy đủ sản phẩm. Điều này làm tốc độ tải chậm và người dùng phải đợi lâu
- **Cách 2: NextJs (Server side Rendering - SSR hoặc Static Site Generation - SSG)**
  - Khi khách hàng vào trang web, server đã sẵn sàng chuẩn bị 1 trang web đầy đủ sản phẩm rồi, chỉ cần gửi về cho người dùng
  - Người dùng sẽ thấy trang ngay lập tức. Load nhanh hơn, trải nghiệm mượt hơn

## NextJs giúp gì cho bạn
- **Tốc độ nhanh hơn**: Vì nội dung có thể được tạo sẵn trước
- **Tối ưu SEO**: Google có thể đọc nội dung dễ dàng hơn để xếp hạng cao hơn trên kết quả tìm kiếm
- **Có backend sẵn**: Không cần sử dụng thêm 1 server khác (Vd Express, Laravel,...), NextJs có thể xử lý API ngay trong ứng dụng

# Cách cài đặt NextJs
- **Mục tiêu**: Cài đặt NextJs trên máy và chạy trang web đầu tiên

## Chuẩn bị trước khi cài đặt
- Trước khi cài, bạn cần kiểm tra máy tính của mình đã có node hay chưa. Nếu chưa có -> lên trang chủ download
- 
## Cài đặt NextJs
- Khi đã có node, có thể tạo 1 dự án NextJs bằng lệnh sau
```js
npx create-next-app@latest my-next-app
```