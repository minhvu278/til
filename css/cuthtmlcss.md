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