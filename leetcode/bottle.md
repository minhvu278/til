## Trạng thái
- Đề:   
    - Cho bình nước có 2 trạng thái là có nước và rỗng 
    - Bình rỗng có thể được đổi thành bình có nước 
    - Tìm tối đa số lượng bình nước có thể uống 

- Ý tưởng 
    - Sử dụng vòng lặp 
    - Tính toán lại số lượng bình nước đầy và trống 
    - Kết thúc khi số lượng bình nước trống nhỏ hơn số lượng bình nước mà ta có thể đổi được 

- TH: 
    ```
    function numberWaterBottle(numberBottles, numberExchange) {
        int result;
        int emptyBottles

        emptyBottles = numberBottles  //  Vì các bình đã uống rồi nên nó trở thành bình trống
        result =  numberBottles   // Kết quả mà số bình mà ta đã uống 

        for(emptyBottles >= numberExchange) {
            numberBottles = emptyBottles / numberExchange   // Chia lấy phần nguyên 
            emptyBottles = emptyBottles % numberExchange   // Chia lấy phần nguyên 

            // Tiếp tục uống 
            emptyBottles += numberBottles 
            result += numberBottles 
        }
        return result;
    }
    ```
    - `numberBottles` : Số lượng bình nước đã uống 
    - `emptyBottles` : Số lượng bình trống 
    - `numberExchange` : Số lượng bình có thể đổi 

