## Reset css
- import CDN của normalize
## Dựng base css
- Khai báo các màu hay dùng bằng các hàm 
```css
:root {
    --white-color: #fff;
    --black-color: #000;
    --text-color: #333;
}
```
- Ở trình duyệt thông thường font-size mặc định sẽ là 16px
- Set font-size: 62.5% thì mặc định sẽ là 10px
- Đặt line-height mặc định 
- box-sizing: inherit kế thừa thuộc tính border-box của html 


## Sử dụng css trong HTML 
- Có 3 kiểu 
    - Internal : Viết trong thẻ style 
    - External : Tạo file css bên ngoài và link vào 
    - Inline : Viết thẳng vào trong thẻ 

## Css selector
- Cách cách để gọi đến các phần tử trong css 
- Có 2 cách gọi: 
    - Id : Sử dụng `#` 
    - Class: Sử dụng `.`

## Các đơn vị trong CSS 
- rem: Phụ thuộc vào thẻ html
- em: Phụ thuộc vào thẻ gần nhất 

## Phân tích dự án 
- Header 
- Banner
    - Text
    - Login messeger
- Content 
    - Các khóa học 
    - Các khóa học khác
    - Banner 
    - Feedback 
    - Thống kê
    - Footer
- Footer 

## Header 
- Những thứ cần khi bắt đầu: 
    - Vị trí 
    - Kích thước (width, height)
    - Màu sắc
    - Kiểu dáng (Chữ, tròn, vuông,...)
- Đàu tiên thì cần reset css 
    ```css
    * {
        padding: 0;
        margin: 0;
        box-sizing: border-box;
    }
    ```
- 1 số css trong phần header
    - Căn lên cùng hàng 
        ```css
        display: inline-block 
        ```
    - Căn giữa cho chữ: Cho chiều cao bằng header thì nó sẽ tự căn giữa 
        ```css
        line-height: 46px;
        ```

## Nav 
- Để tác động lên thẻ cha mà không ảnh hưởng đến thẻ con sử dụng `>`
    ```css 
    #nav > li > a {
        color: #fff;
        text-transform: uppercase;
    }
    ```


## CSS Position (Tạo ra các vị trí cho element)
- Relative (Vị trí tương đối)
    - Không phụ thuộc vào thằng nào cả. Lấy chính nó làm gốc tọa độ 
    - Thường dùng để đè lên layout  

- Absolute (Vị trí tuyệt đối)
    - Phụ thuộc vào thẻ cha gần nhất có thuộc tính position 


- Fixed (Vị trí phụ thuộc vào khung trình duyệt)
- Sticky (Bám dính - Không đc nhiều trình duyệt hỗ trợ)

