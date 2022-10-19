# Đồng bộ và bất đồng bộ 
- Đồng bộ
    - 1 function sẽ chạy theo thứ tự từ trên xuống dưới - Tại 1 thời điểm chỉ thực thi được 1 dòng lệnh duy nhất 
    - 1 function mà dựa trên 1 kết quả của 1 function khác thì nó sẽ phải đợi đến khi function kia trả về kết quả thì nó mới thực hiện tiếp 
- Bất đồng bộ
    - Không theo thứ tự
    - Chạy song song
    - Có 3 cách để xử lý bất đồng bộ: Callback, promise, async await
    

## Callback 
- Là hàm 
- Truyền qua đối số 
- Được gọi lại trong hàm nhận đối số
- Muốn trì hoãn việc thực thi 1 function và chờ đến khi function khac thực thi và trả về kết quả 
    ```js
    function myFunction(param) {
        param('Ok bae')
    }

    function myCallback(value) {
        console.log('Value:', value)
    }

    myFunction(myCallback)
    ```
    - param sẽ được coi như là function myCallback 
    - Tuy nhiên thì cần check nếu là function thì mới thực thi. Chứ nếu truyền `myFunction(123)` thì nó sẽ không hiểu là hàm và sẽ báo lỗi ngay

# Promise (Lời hứa)
## Promise là gì? Cách hoạt động của nó
- Sinh ra để giải quyết 1 vấn đề nào đó trong quá trình lập trình bất đồng bộ
- Promise là 1 object contructor được thêm vào từ phiên bản es6
- Promise sẽ nhận vào contructor 1 function (Gọi là excutor) - function này sẽ được thực thi khi gọi promise này 
    ```js
    var promise = new Promise(
        // Excutor
        function (resolve, reject) {
            // Logic 
            // Thành công: resolve()
            // Thất bại: reject()
        }
    )
    ```
    - Gọi đến function trước khi **promise** nhận được
    - Nhận vào 2 đối số là resolve, reject (2 thằng này đều là hàm)
- Khi nhận được đối tượng **promise** thì nó sẽ trả ra 3 phương thức mà hay sử dụng (3 thằng này đều nhận vào 1 callback)
    - .then(function() {}) // Gọi khi resolve được gọi
    - .catch(function() {}) // Gọi khi reject được gọi
    - .finally(function() {}) // Khi 1 trong 2 được gọi thì callback này đều được gọi
- Có thể nhận nhiều thằng .then
    ```js
    var promise = new Promise(

        function (resolve, reject) {
            resolve()
        }
    )

    promise
            .then(funtion() {
                return 1
            })
            .then(funtion(data) {
                console.log(data) // 1
                return 2
            })
            .then(funtion(data) {
                console.log(data) // 2
            })
    ```
    - Kết quả trả về của function đằng trước sẽ là tham số đầu vào của function đằng sau
- Cần lưu ý là nếu thằng đằng trước (.then trước) trả về 1 promise thì phải đợi nó chạy xong thì mới chạy đến mấy thằng đằng sau
    ```js
    var promise = new Promise(

        function (resolve, reject) {
            resolve()
        }
    )

    promise
            .then(funtion() {
                return new Promise(function(resolve) {
                    setTimeout (resolve, 3000)
                })
            })
            .then(funtion(data) {
                console.log(data)
            })
    ```
    - Thằng then thứ 2 sẽ đợi thằng promise được giải quyết -> sau 3s mới chạy vào thằng then đằng sau

    ```js
    funtion sleep(ms) {
        return new Promise(function(resolve) {
            setTimeout (resolve, ms)
        })
    }

    sleep(1000)
            .then(funtion() {
                console.log(1)
                return sleep(1000)
            })
            .then(funtion() {
                console.log(2)
                return sleep(1000)
            })
            .then(funtion() {
                console.log(3)
                return sleep(1000)
            })
    ```
- Trong trường hợp 1 thằng promise nào ở giữa mà bị reject thì những thằng ở dưới sẽ không chạy 
    ```js
    funtion sleep(ms) {
        return new Promise(function(resolve) {
            setTimeout (resolve, ms)
        })
    }

    sleep(1000)
            .then(funtion() {
                console.log(1)
                return sleep(1000)
            })
            .then(funtion() {
                console.log(2)
                return new Promise(function(resolve, reject){
                    reject('Error)
                }) 
            })
            .then(funtion() {
                console.log(3)
                return sleep(1000)
            })
            .catch(function(err) {
                console.log(err)
            })
    ```
- `promise.resolve, promise.reject, promise.all`
    - Cách tạo promise thông thường
    ```js
    var promise = new Promise(

        function (resolve, reject) {
            resolve() 
            reject()
        }
    )

    promise
            .then(function () {

            })
            .catch(function(err) {
                console.log(err)
            })
    ```
- Khi xử lý mà ta biết trước nó sẽ trả về resolve() hoặc reject() thì ta chỉ cần khai báo 
    ```js
    var promise = Promise.resolve('success')

    promise
            .then(function(result) {
                console.log('Result: ', result)
            })
            .catch(function(err) {
                console.log(err)
            })
    ```
    - Mặc định sẽ nhảy vào .then
- Đối với reject cũng thế chỉ cần Promise.reject
- Promise.all: Giúp chạy song song các promise
    ```js
    var promise1 = new Promise(
        function(resolve) {
            setTimeout (function() {
                resolve([1]);
            }, 2000)
        }
    )

    var promise2 = new Promise(
        function(resolve) {
            setTimeout (function() {
                resolve([2, 3]);
            }, 5000)
        }
    )

    Promise.all([promise1, promise2])
            .then(funtion(result) {
                var result1 = result[0]
                var result2 = result[1]
            })

            console.log(result1.concat(result2))
    ```
    - Nếu mà viết như này sẽ tốn tận 7s. Thế nên nếu chạy song song thì ta chỉ mất 5s 
    - Nếu mà có 1 promise bị reject thì nó sẽ lọt vào thằng .catch luôn