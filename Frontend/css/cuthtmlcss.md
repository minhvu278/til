# Kỹ thuật cắt HTML css
## Quy tắc chính
- Từ trên xuống dưới (Layout tổng quát, chia block)
- Từ ngoài vào trong
    - Dùng container hay container-fluid?
        - Container fluid: Full màn hình từ trái sang phải
        - Container: Bị giới hạn ở 1 khúc nào đấy và đẩy content vào giữa 
    - Nếu container thì dùng thêm row
- Từ trái sang phải (Xác định các columns, nếu có row)
## Quy tắc phụ
- Với Bootstrap: container->row->columns
- Với Flexbox: container->flex container->flex items
- Tách biệt chức năng: layout & content 

## Group các thẻ lại
```css
div.col
    div.about__content
        h1.about__title
        p.about__description
        button
```
- Nên bao các thẻ vào trong thẻ div để lúc css thì css vào div.about__content chứ k css vào div.col

## Những thứ cần nhớ 
- Để nội dụng của thẻ dài đến đâu thì chỉ dài đến đấy thì cho display = inline-block
- Khi 1 thẻ div có tính chất khối cho float vào thì nó sẽ mất đi tính kế thừa (mặc định thẻ div sẽ kế thừa hết chiều ngang mà nó có thể chiếm)
- padding-top: 50%  : Chiếm 50% chiều ngang của chính nó
- letter-spacing: 4px  : Khoảng cách cac chữ cách nhau 4px 
- Thêm !important thì nó sẽ có sẽ có độ ưu tiên nhất
    vd:
    ```css 
    .text-white {
        color: #fff !important // Thẻ nào đặt class là text-color sẽ được đổi thành màu trắng 
    }
    ```