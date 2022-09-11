# Tìm hiểu SQL Transaction và cách sử dụng trong Laravel

## Transaction là gì 
- Là 1 nhóm các câu lệnh SQL xử lý có tuần tự thao tác trên CSDL 
- Nếu 1 transaction được thực hiện thành công thì tất các các dữ liệu được lưu vào DB
- Và chỉ cần 1 lỗi thì sẽ rollback lại, dữ liệu sẽ được khôi phục lại như ban đầu
- Transaction có 1 tiêu chuẩn gọi là `ACID`
    - **Atomicity(Tính tự trị)**: Đảm bảo tất cả hành động của 1 đơn vị transaction là thành công, ngược lại sẽ rollback quay lại thời điểm chưa xảy ra thay đổi
    - **Consistency(Tính nhất quán)**: Đảm bảo tất cả các thao tác trên CSDL được thay đổi thành công và không xảy ra lỗi
    - **Isolation(Tính cô lập)**: Đảm bảo transaction này không liên quan đến transaction khác (VD: Ông A đang chuyển tiền không liên quan đến ông B chuyển)
    - **Durability(Tính bền vững)**: Đảm bảo kết quả hoặc tác động của transaction vẫn luôn tồn tại kể cả khi hệ thống xảy ra lỗi

## Sử dụng transaction trong laravel 
- Sử dụng phương thức transaction trong DB facade 
    ```php 
    use DB;

    ......

    DB::transaction(function () {
        DB::table('users')->update(['votes' => 1]);

        DB::table('posts')->delete();
    });
    ```
    - Nếu 1 exception được bắn ra từ trong transaction Closure, transaction sẽ tự động rollback lại
    - Nếu Closure thực thi thành công, transaction sẽ được tự động commit
    - Laravel sẽ tự động rollback hoặc commit

- Xử lý Deadlocks
    - Method transaction sẽ có thêm 1 tham số thứ 2 là `số lần thực hiện transaction` nếu như tình trạng Deadlocks(Bế tắc) xảy ra
        ```php 
        use DB;

        ...

        DB::transaction(function () {
            DB::table('users')->update(['votes' => 1]);

            DB::table('posts')->delete();
        }, 5);
        ```

- Thực hiện transaction 1 cách thủ công 
    - Có thể quản lý transaction thủ công như khi nào mới rollback, commit 
        ```php 
        // Bắt đầu các hành động trên CSDL
        DB::beginTransaction();
        ...

        //Commit dữ liệu khi hoàn thành kiểm tra
        DB::commit();
        ...

        //Gặp lỗi nào đó mới rollback
        DB::rollBack();
        ...
        ```
    - VD 
        ```php 
        public function doAction()
        {
            DB::beginTransaction(); // Bắt đầu transaction
            try {
                DB::table('users')->update(['votes' => 1]);
                DB::table('posts')->delete();
                
                DB::commit();// Nếu thành công thì commit
            } catch (Exception $e) {
                DB::rollBack(); // Nếu lỗi thì nhảy vào catch và rollback quay trở về ban đầu
                
                throw new Exception($e->getMessage());
            }
        }
        ```
        - 



