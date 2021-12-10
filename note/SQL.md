# Table
- Drop: Xóa bảng luôn
- Truncate: Chỉ xóa dữ liệu trong bảng 

- Sửa bảng & thêm cột ngày sinh 
ALERT TABLE HocSinh ADD NgaySinh Date

## Kiểu dữ liệu 
- char : Kiểu kí tự, độ nhớ được phát cứng  (Thêm n vào trước có thể lưu tiếng việt)
    VD: 
        char(10) -> Cấp 10 ô nhớ và không ai được động vào  
- varchar: Cấp phát bộ nhớ động
- date: Lưu trữ ngày, tháng, năm 
- time: Giờ phút giây 
- bit: lưu giá trị 0 và 1

## Primary key (Khóa chính)
- UNIQUE : Duy nhất. Trường nào có từ khóa unique thì không thể có 2 giá trị trùng nhau 
- NOT NULL : Trường không được phép nul
- CONSTRAINT : Đặt tên cho khóa để xóa cho dễ 

- Set khóa chính cho bảng 
    ```
    ALERT TABLE nhanvien 
    ADD CONSTRAINT PK_key (Đây là tên khóa được đặt)
    ```

- Đặt nhiều khóa chính 
    ```
    CREATE TABLE nhansu (
        ID1 INT NOTNULL, -- Không được đặt là PRIMARY 
        ID1 INT NOTNULL

        Name VARCHAR(100) 

        PRIMARY KEY (ID1, ID2)
    )
    ```

## Khóa ngoại 
- Tham chiếu tới khóa chính 
- Cùng kiểu dữ liệu 
- Cùng số lượng trường có sắp xếp 
- Đảm bảo toàn vẹn dữ liệu, không có trường hợp tham chiếu đến dữ liệu không tồn tại 
- Tạo khóa ngoại trong khi tạo bảng 
    ```
    CREATE TABLE BoMon(
        Id CHAR(10) NOT NULL,
        Name VARCHAR(100) 
    )



    CREATE TABLE GiaoVien(
        Id CHAR(10) NOT NULL,
        Name VARCHAR(100) 
        
        BoMon_id CHAR(10)

        FOREIGN KEY (BoMon_id) REFERENCES BoMon(id)
    )


    -- Tạo khóa ngoại sau khi tạo bảng 
    ALERT TABLE GiaoVien ADD CONSTRAINT FK_GV FOREIGN KEY(BoMon_id) REFERENCES BoMon(Id)
    ```

- Hủy khóa 
    ```
    ALERT TABLE GiaoVien DROP CONSTRAINT FK_GV
    ```

## Truy vấn với điều kiện 
- COUNT(*): Đếm số lượng tất cả record 
- COUNT(tên trường): Đếm số lượng tên trường đó 
    ```
    SELECT COUNT(*) FROM GiaoVien 
    ```

## Tìm kiếm gần đúng với like 
- Tìm ra tên giáo viên bắt đầu bằng chữ v
    ```
    SELECT * FROM GiaoVien
    WHERE Hoten like 'v%'
    ```
    - %v: kết thúc bằng v
    - %v%: Có chữ v 

## Inner join 
- Kết hợp 2 bảng lại & lấy ra các trường thỏa mãn điều kiện 
```
-- Inner join cũ 

SELECT * FROM
    GiaoVien inner join Bomon (-- Có thể viết tắt là join thay vì inner join)
    ON Bomon.id = GiaoVien.bomon_id

--Inner join mới

SELECT * FROM
    GiaoVien,Bomon
    WHERE Bomon.id = GiaoVien.bomon_id
```

## Full outer join
- Gom 2 bảng lại (Giống như join) theo điều kiện, bên nào không có dữ liệu thì để null 

## Cross join 
- Là tổ hợp mỗi record của bảng A với all record của bảng B

## Left & right join 
- Left join: 
    - Bảng bên phải gom vào bảng bên trái 
    - Record ở bảng bên phải k có thì để null
    - Record ở bảng bên trái k có thì không điền vào

## Union 
- Gom 2 bảng lại với nhau nếu A không tồn tại trong B thì sẽ tự thêm vào (A thiếu B đắp)
    ```
    SELECT id FROM GiaoVien
    Where Luong < 2000
    UNION 
    SELECT giaovien_id FROM NguoiThan 
    Where Sex < 'Nu'
    ```

## Select into
- Dùng để tạo bảng mới từ dữ liệu đã có sẵn (Dùng để backup là chủ yếu)

    ```
    SELECT * INTO Vu
    FROM GiaoVien
    ```
    - Lấy hết dữ liệu của bảng GiaoVien đưa vào Vu

## Into select 
- Coppy dữ liệu từ 1 bảng đã tồn tại 


## Truy vấn lồng 
- Truy vấn lồng trong FROM
    ```
    SELECT * FROM 
    GiaoVien, (SELECT * FROM DeTai) AS DT
    ```
    - Phải dùng AS để có thể tái sử dụng được  
