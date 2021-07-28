## Bài 1: Dựng source base
- Tạo 2 file
    - base.css để cấu hình chung
    - main.css để css nhữn thành phần riêng
## Bài 2: Reset css
- Dùng normalize cdn (Thư viện reset css)
## Bài 3: Navbar

## Bài 5: Font-icon
- Download font-awesome
- Link vào head 
- Dùng <i> để thêm icon
```html
<i class="fab fa-facebook"></i>
```
## Header QR
- Có 2 cách để gọi phần tử đầu tiên
    - Dùng lớp giả :first-child
    - Dùng  :nth-child(1) (Cách fix cứng, sử dụng khi class không thay đổi)
    ```css
    header__qr-link:nth-child(1){

    }
    ```
```css
.header__navbar-item--has-qr:hover .header__qr {
    /* Css được viết trong đc apply vào header__qr khi hover vào cha của nó */
}
