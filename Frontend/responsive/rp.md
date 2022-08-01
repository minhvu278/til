# Responsive 
- Là kĩ thuật giúp website hiển thị tương thích với nhiều kích thước màn hình khác nhau(Mobile, Tablet, PC, ...)
- Tối ưu trải nghiệm người dùng
    - Hiển thị rõ ràng các thành phần(hình ảnh, cỡ chữ,...)
    - Ẩn/ Hiện các thành phần phù hợp với kích thước màn hình 

## Viewport 
- Nếu k có thẻ này thì 1 số trình duyệt k hỗ trợ sẽ bị tự zoom lên 
    ```css
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    ```
    - `width=device-width`: Chiều ngang của thiết bị 
    - `initial-scale=1.0` : Tỉ lệ đúng của nó k bị zoom 

## Media query 
- Chuỗi truy vấn để chọn ra được kích thước của màn hình 
    ```css
    @media keyword mediatype and (max-width: 600px) {
        body {
            background-color: lightblue;
        }
    }
    ```
    - Đầu tiên là về keyword gồm có 4 phần: 
        - not: Lọai trừ 
        - only: chỉ
        - and
        - or 

    - Mediatypes : Trường hợp muốn css cho việc gì
        - print: css cho chế độ in 
        - screen: Cho màn hình
        - speech: Màn hình nói được 
        - all- default: Áp dụng cho tất cả
    
    - Media Features: 
        - Sử dụng `min-width` và `max-width` để xác định kích thước màn hình 

## Breakpoints 
- Là những điểm/vị trí mà bố cục website sẽ thay đổi - thích ứng để tạo nên giao diện responsive 


## 1 số thứ cần lưu ý
- Khi code các màn response thì sẽ có 1 số phần bi lặp lại thì xem có thể viết chung lại được không

## Grid system
- Thành phần chính (Làm việc với css)
    - **Grid (Lưới)**: Thường là phần cha, chứa `row` và `column`
    - **Row (Dòng)**: Chiều ngang, chứa column 
    - **Column (Cột)**: Chứa nội dung thành phần website

# Tạo thư viện grid system
## Tạo đối tượng Grid 
- Tạo class 
    - grid: full-width, chiếm hết chiều ngang đối tượng cha 
    - wide: Chiều ngang tối đa 1200px 

## Tạo row 
- Chứa các colunn giúp column nằm theo chiều  ngang
- Khi chiều ngang vượt quá kích thước row, cho column xuống hàng
- Loại bỏ khoảng thừa do gutters tạo ra ở 2 phía 
- Column padding bao nhiêu thì row sẽ margin âm bấy nhiêu

## Column 
- Chứa các thành phần trên website
- Tạo ra các khoảng padding để tạo ra các rãnh giữa các column
    ```css
    .col {
        padding-left: 4px;
        padding-right: 4px;
    }
    ```
- Không nhất thiết là phải chia làm 12 thẻ div tương ứng với 12 cột. Chỉ cần chia làm sao cho đủ 12 cột là được
- `col` sẽ đi với các `.c-0  -> .c-12`
    ```css
    .c-1 {
        flex: 0 0 8.33333%;
        max-width: 8.33333%;
    }
    ```
    - Trong trường hợp thẻ cha dùng `flex-description: row` thì kích thước item chiều ngang là `8.33333%`
    - `max-width`: Giới hạn chiều ngang tối đa của item

- 1 số từ viết tắt trong thư viện 
    - Column: .col 
    - Prefix class: 
        - c - mobile 
        - m - tablet
        - l - pc

- Column offset 