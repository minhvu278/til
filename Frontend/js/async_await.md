# Xử lý bất đồng bộ 
## Callback
- Bài toán: Muốn gọi cho Nam nhưng không có số -> Gọi điện cho thằng bạn -> Xin số thằng Nam -> Gọi điện cho thằng Nam
    ```js
    const xinSoDt = () => {
    let soDt

    console.log('Gọi điện cho thằng bạn: Xin số thằng Nam ')
    console.log('Thằng bạn tìm số thằng Nam')

    setTimeout(() => {
        soDt = 841183345
        console.log('Đã tìm thấy số thằng Nam')
    }, 1000)

    return soDt
    }

    const soDtDaXin = xinSoDt()
    console.log(soDtDaXin
    ```
    - Output trả ra sẽ là
    ```
    Gọi điện cho thằng bạn: Xin số thằng Nam 
    Thằng bạn tìm số thằng Nam
    undefined
    Đã tìm thấy số thằng Nam
    ```
- Tại sao lại trả ra `undifined`? Đó là vì thằng setTimeout nó chỉ tạo ra lời hứa là ok khi tìm được số thì tao sẽ trả lại. Tuy nhiên 1s sau nó mới chạy nên nó sẽ trả về `soDt` trước khi nó tìm thấy 
- Để xử lý vấn đề trên thì có 1 cách sửa gọi là sửa tạm cho nó chạy được(Sửa xấu)
    ```js
    const xinSoDt = () => {
    let soDt

    console.log('Gọi điện cho thằng bạn: Xin số thằng Nam ')
    console.log('Thằng bạn tìm số thằng Nam')

    setTimeout(() => {
        soDt = 841183345
        console.log('Đã tìm thấy số thằng Nam')
    }, 1000)

    setTimeout(() => {
        console.log(soDt)
    }, 1500)
    }

    xinSoDt()
    ```
    - Với cách này thì hiển nhiên là setTimeout đầu tiên sau 1 giây thì nó sẽ trả về số điện thoại và sau 1s5 nữa thì nó sẽ trả ra số đt 
- Cách trên vẫn ok mà đúng không. Tuy nhiên thì thời gian đợi quá nhiều. Đó là 1 vấn đề của lập trình bất đồng bộ đặc biệt là làm việc với callback
- Để xử lý vấn đề trên thì ta sử dụng callback: 
    ```js 
    const xinSoDt = callback => {
    let soDt

    console.log('Gọi điện cho thằng bạn: Xin số thằng Nam ')
    console.log('Thằng bạn tìm số thằng Nam')

    setTimeout(() => {
        soDt = 841183345
        console.log('Đã tìm thấy số thằng Nam')
        callback(soDt)
    }, 1000)
    }

    const sauKhiNhanDuocSoDt = (soDtDaNhan) => {
        console.log(`Đây là số thằng Nam ${soDtDaNhan}`)
    }
    xinSoDt(sauKhiNhanDuocSoDt)
    ```
    - Logic chạy sẽ như sau: 
        - Hàm `xinSoDt` nhận vào 1 tham số là callback(callback ở đây không phải là số, chuỗi mà nó chính là function)
        - setTimeout `callback(soDt)` sau 1s khi đã tìm được số thằng Nam sẽ bốc điện thoại lên và gọi cho bạn (Nó sẽ tự động gọi lại và không cần care đến nó)
        - Hàm `sauKhiNhanDuocSoDt` sẽ trả ra số điện thoại 
        - Sau đó hàm `xinSoDt` sẽ gọi hàm sauKhiNhanDuocSoDt và trả ra số điện thoại
    - **xinSoDt(callback) -> callback(soDt) -> sauKhiNhanDuocSoDt(soDtDaNhan) -> xinSoDt(sauKhiNhanDuocSoDt)**
        - Khi gọi hàm `xinSoDt(sauKhiNhanDuocSoDt)` cứ hiểu nôm na là nó gọi vào thằng callback(soDt) để lấy ra số Dt rồi log ra số điện thoại 
    
- Tuy nhiên thì nếu có quá nhiều hàm callback thì sao
    - Vẫn với VD trên tuy nhiên thì sau khi xin được số thằng Nam thì cần sạc điện thoại rồi mới gọi cho Nam
    ```js 
    const xinSoDt = (hamGoiLaiSauKhiTimRa) => {
    let soDt

    console.log('Gọi điện cho thằng bạn: Xin số thằng Nam ')
    console.log('Thằng bạn tìm số thằng Nam')

    setTimeout(() => {
        soDt = 841183345
        console.log('Đã tìm thấy số thằng Nam')
        hamGoiLaiSauKhiTimRa(soDt, goiChoNam)
    }, 1000)
    }
    const sacPin = (soDt, hamGoiLaiSauKhiSacPin) => {
        console.log('Đợi tí, sạc pin phát')

        setTimeout(() => {
            console.log('Sạc pin xong. Bắt đầu gọi cho Nam')
            hamGoiLaiSauKhiSacPin(soDt)
        }, 2000)
    }

    const goiChoNam = (soDt) => {
        console.log(`Đang buôn với Nam sau khi gọi vào số ${soDt}`)
    }

    xinSoDt(sacPin)
    ```
    - Output
    ```
    Gọi điện cho thằng bạn: Xin số thằng Nam 
    Thằng bạn tìm số thằng Nam
    Đã tìm thấy số thằng Nam
    Đợi tí, sạc pin phát
    Sạc pin xong. Bắt đầu gọi cho Nam
    Đang buôn với Nam sau khi gọi vào số 841183345
    ```
- Đây mới chỉ là 3 callback mà nó khá lằng nhằng và mất nhiều thời gian - Đây chính là vấn đề của callback
    - Dễ rối
    - Khó viết
    - Khó debug