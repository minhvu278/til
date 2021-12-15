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

## Group by
- Agreeate Function
    - AVG(): Tính trung bình 
    - FIRST(): Phần tử đầu tiên
    - LAST(): Phần tử cuối cùng 
    - MAX(): Là phần tử lớn nhất theo số 
    - MIN(): Là phần tử nhỏ nhất theo số 
    - ROUND(): Làm tròn
    - SUM(): Tổng 

- String function 
    - CHARINDEX: Tìm 1 phần tử có tồn tại trong chuỗi không 
    - CONCAT(): Cắt chuỗi 
    - LEFT(): Lấy bên trái bao nhiêu phần tử
    - LEN/LENGTH(): Độ dài 
    - LTRIM(): Cắt khoảng trắng bên trái
    - RTRIM(): Cắt khoảng trắng bên phải
    - SUBSTRING(): Lấy ra chuỗi con

- Having giống như where của select nhưng giành cho group by 

## View 
- View là 1 bảng ảo
- Tạo view từ câu truy vấn
    ```
    CREATE VIEW testView as  -- Dữ liệu bên trong bảng view sẽ giống bảng giáo viên 
    SELECT * FROM GiaoVien
    ```
- Khi thay đổi giá trị bất kì ở cột nào của bảng GiaoVien thì bảng testView cũng thay đổi theo 
- Để create được tên bảng có dấu và dấu cách - cho vào trong []

- Sửa view
    ```
    ALERT VIEW testView as 
    SELECT HoTen FROM GiaoVien
    ```
- Xóa view
    ``` 
    DROP VIEW testView
    ```

## Check 
- Cho nằm trong khoảng điều kiện mong muốn
    - VD: 
        ```
        CREATE TABLE TestCheck (
            Id int 
            Luong int CHECK(Luong > 2000 AND LUONG < 5000)
        )
        ```

## Indexes (Đánh index)
- Tăng tốc độ tìm kiếm (Chậm tốc độ thêm xóa sửa)
    ```
    CREATE INDEX IndexName ON NguoiThan(giaovien_id)

    SELECT * FROM NguoiThan
    WHERE giaovien_id = '01' AND Ten = 'Vu Do'
    ```

## Declare và sử dụng biến
- Biến bắt đầu bằng kí hiệu @
- Tạo ra biến & tái sử dụng lại 
    ```
    DECLARE @MinSalaryMaGv CHAR(10)

    SELECT @MinSalaryMaGv = MaGv FROM GiaoVien WHERE Luong = (SELECT Min(Luong) FROM GiaoVien)

    SELECT YEAR(GETDATE()) - YEAR(NgSinh) FROM GiaoVien 
    WHERE MaGv = @MinSalaryMaGv
    ```

- 1 số kiểu khởi tạo dữ liệu 
    ```
    DECLARE @i INT

    -- Khởi tạo với giá trị mặc định 
    DECLARE @j INT = 0

    -- Set dữ liệu cho biến 
    SET @i = @i + 1
    SET @i += 1
    SET @j *= @i

    -- Set thông qua câu SELECT 
    DECLARE @MaxLuong int 
    --

    SELECT @MaxLuong = MAX(Luong) FROM GiaoVien 
    ```

## Store Procedure 
- Tái sử dụng code 
- Tạo bản sao để lần sau k cần chạy lại từ đầu ( Kiểu như cache)
- Giới hạn quyền user nào đc sử dụng user nào k 
- Cấu trúc
    ```
    CREATE PROC <Tên store>  
        [Param nếu có]
    AS
    BEGIN 
        <Code xử lý>
    END

    -- VD
    CREATE PROC StoreTest  
        @MaGv NVARCHAR(10)
    AS
    BEGIN 
        SELECT * FROM GiaoVien WHERE MaGv = @MaGv 
    END

    -- C1:
    EXEC StoreTest @MaGv = N'VuDo'
    --C2:
    EXEC StoreTest N'VuDo'

## Function
- Function 
    ```
    -- Tạo func k có param
    CREATE FUNCTION UF_SelectAllGiaoVien()
    RETURN TABLE
    AS RETURN SELECT * FROM GiaoVien

    SELECT * FROM UF_SelectAllGiaoVien()

    -- Tạo function  có parameter
    CREATE FUNCTION UF_SelectLuongGiaoVien(@MaGv char(10))
    RETURN int
    AS
    BEGIN
        DECLARE @Luong int
        SELECT @Luong = Luong FROM GiaoVien WHERE MaGv = @MaGv
        RETURN @Luong
    END

    SELECT UF_SelectLuongGiaoVien(MaGv) FROM GiaoVien

    ```

## Trigger 
- Can thiệp vào các sự kiện thêm sửa xóa
- Mặc định trong trigger sẽ có 2 bảng là inserted (Chứa những trường đã insert | update vào bảng) & deleted (Chứa những trường đã bị xóa khỏi bảng )
    ```
    CREATE TRIGGER UTG_ InsertGiaoVien
    ON GiaoVien 
    FOR INSERT, UPDATE 
    AS
    BEGIN
        ROLLBACK TRAN -- Hủy bỏ, thay đổi, cập nhật bảng 
        PRINT 'Trigger2'
    END

## Transaction 
- Tran 
    ``` 
    BEGIN TRANSACTION 
    DELETE GiaoVien WHERE TEN = 'VuDo'
    ROLLBACK - Hủy bỏ TRANSACTION

    BEGIN TRANSACTION 
    DELETE GiaoVien WHERE TEN = 'VuDo'
    COMMIT - Chấp nhận TRANSACTION

