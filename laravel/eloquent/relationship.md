# Eloquent ORM Relationship
- Cho phép định nghĩa các mối quan hệ với nhau từ đó có thể query, làm việc với các model được định nghĩa quan hệ 1 cách đơn giản 

## Định nghĩa relationship 
- Các eloquent relationship được định nghĩa trong model như 1 phương thức bình thường và có thể dùng nó để tạo ra các query builder khác nhanh và đơn giản bằng cách sử dụng chúng như method 

- 1 số kiểu quan hệ trong Eloquent
    - One To One: Là mối quan hệ đơn giản nhất (Vd 1 user chỉ có 1 số điện thoại duy nhất)
        - Để định nghĩa mối mốiquan hệ này ta sử dụng `hasOne` 
            ```php
            hasOne($relationModel, $foreignKey, $localKey');
            ```
        - VD: 
            ```php
            class User extends Model
            {
                public function phone()
                {
                    return $this->hasOne(Phone::class);
                }
            }
            ```
            - Model liên kết là phone 
            - Khóa ngoại là `user_id`(Mặc định sẽ là tên model hiện tại + `_id`)
            - Khóa chính là primary key của model hiện tại
