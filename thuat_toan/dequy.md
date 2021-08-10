## Đệ quy là gì
- Cần tìm hiểu phương thức trước 
    - Phương thức là tập hợp các lệnh với tham số truyền vào để máy tính thao tác các lệnh theo ý muốn người viết
    - Đệ quy xảy ra khi người viết các phương thức tự gọi (hoặc định nghĩa lại) chính nó
- VD: Tính luỹ từ 0 -> n
![](/css/img/tinhluy.png)
    - Truyền tham số n vào phương thức sum()
    - Chương trình sẽ chạy qua các lệnh điều kiện "if(n>=1)", giá trị n thay đổi theo từng vòng của điều kiện đến khi không còn thoả mãn
    - Khi chương trình "return n" thì n chính là giá trị đã được tính ở phương thức đã đặt điều kiện ở trên

- Có 2 yếu tố cần để tiến hành 1 phương thức đệ quy
    - Có điều kiện dừng: Xác đinh quy luật của phương thức và tìm giá trị cụ thể khi thoả mãn 1 điều kiện nhất định
    - Phương thức đệ quy: Sẽ gọi lại chính nó cho đến khi nó trả về điều kiện dừng ở bước 1

## Đệ quy đuôi và đầu
- Gọi là đệ quy đuôi khi phương thức đệ quy được đặt ở cuối, sau khi chương trình chạy qua điều kiện dừng 
- Còn lại là đệ quy đầu 😂
- VD: 
![](/css/img/dequy_dauduoi.png)
        