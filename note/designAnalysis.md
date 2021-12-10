## Use-case 
- Là 1 chức năng của hệ thống, mang lại 1 ý nghĩa nhất định đối với người dùng 
- 1 use case là 1 chuỗi các hành động mà hệ thống thực hiện mang kết quả lại đối với actor (Hành động mà actor không nhìn thấy được thì không được coi là use-case)

- Có 2 loại quan hệ 'include' & 'extend' 

    - Include: Để thực hiện use-case A thì chắc chắn phải thực hiện use-case B (Bắt buộc phải làm theo chức năng kế tiếp)
        - Vd như mua sản phẩm mới thanh toán được, đăng kí tài khoản mới đăng nhập được, ...

    - Extend: Thực thi A, B thực hiện cũng được mà không cũng được (Không nhất thiết phải sư dụng B)

    - VD:
        use-case A --include---> use-case B

## Activity - Diagram 
- Vẽ ra các luồng đi, logic ,.. của hệ thống 
- Các kí hiệu: 
    - Start: Hình tròn đen -- Điểm bắt đầu của luồng xử lý 
    - Activity: Kí hiệu là ô vuông - có tên hoạt động bên trong
    - Transition: Kí hiệu là mũi tên - biểu thị chiều của luồng xử lý 
    - Decisition : Kí hiệu là hình thoi 
        - Branch: 1 điều kiện vào -> 2 trường hợp ra 
        - Merge: Có 2 hoặc nhiều điều kiện đi vào -> chỉ có 1 trường hợp ra (Thỏa mãn nhiều điều kiện cùng lúc thì nó mới đi ra luồng còn lại)
    - Synchronization bar: Kí hiệu dòng kẻ ngang đậm - Mô tả dòng điều khiển thực hiện song song 
        - Fork 1 dòng đi vào, 2 dòng đi ra - Không quan tâm thứ tự (VD: Trời mưa 2 người cùng đi mua áo mưa)
        - Join: 2 hoặc nhiều dòng đi vào và chỉ có 1 dòng đi ra (VD: 2 người mua xong áo mưa - cùng đi chơi )
    - End: Cũng là hình tròn đen giống start nhưng có thêm vòng bao ngoài 