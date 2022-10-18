# Xử lý bất đồng bộ 
- Xử lý bất đồng bộ là 1 vấn đề khá là nhức nhối cho ae học js. Vậy bất đồng bộ là gì? Có nhất thiết phải sử dụng nó? Chúng ta cùng tìm hiểu nó ở bên dưới nhé 

- Trước khi vào phần giải thích thì có 1 ví dụ như này cho các bạn dễ hình dung
    - Gỉa sử trong 1 nhà hàng: 
        - Nhân viên đón khách vào ăn -> khách gọi món -> Nhân viên báo cho đầu bếp -> đầu bếp làm rồi đưa cho nhân viên -> Nhân viên mang ra cho khách -> Khách ăn xong -> Nhân viên dọn bàn -> Mời khách tiếp theo vào
        - Tuy nhiên thì trong thực tế thì nhân viên không đứng đợi như thế được mà phải làm liên tay liên chân  
    - Chắc qua ví dụ này thì mọi người cũng có thể hình dung ra sự bất tiện khi phải chờ đợi thời gian quá lâu từ khách, nhân viên hay đầu bếp (Trong js thì nó sẽ làm chậm website đi)
- Bất đồng bộ trong Js giúp ta không phải đợi 1 việc xong thì mới làm đến việc tiếp theo (Hay là như kiểu xử lý bài toán trên theo cách thực tế =)) ). 
    - Giải thích như trong VD cho dễ hình dung nhé 
        - Khi đầu bếp nấu xong thì bấm chuông báo cho nhân viên biết món đã xong để bê ra cho khách - Trong khoảng thời gian đợi đầu bếp nấu xong thì nhân viên đã làm được rất nhiều việc rồi
    - Trong JS cũng thế: Khi thực hiện lệnh 1 thì thực hiện được lệnh 2,3,4 rồi, lệnh 1 xong thì quay lại lấy dữ liệu rồi thực hiện tiếp lệnh 5,6
        - Việc này sẽ giúp cho website chạy nhanh hơn, đỡ hao phí tài nguyên hơn

## Sai lầm cơ bản khi xử lý 
- Function1(callback())
- Function2()
    - Vd function1 mất 5s thực hiện thì khi xong thì nó sẽ gọi hàm callback() - Hàm gọi lại
    - Thì ta không cần đợi hàm 1 thực hiện xong mới chạy hàm 2 
        






- Khó, kể cả học xong 
- Dần dần sử dụng sẽ biết 
- Nên quay lại đọc lại, xem lại, càng nhiều lần thì càng nhanh hiểu
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