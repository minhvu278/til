# Một chút về js 

## Arrow function
- Function thông thường 
    ```js
    function logger(log) {
        //
    }
    ```
- Expession function 
     ```js
    const logger = function logger(log) {
        //
    }
    ```
- Arrow function 
     ```js
    const logger = (log) => {
        //
    }
    ```

## Module 
- Chỗ nào cần dùng module thì import vào
- Còn file nào muốn cho dùng phải export ra 

## Enhanced object literals 
- Định nghĩa key: value cho object 
- Định nghĩa method cho object 
    ```js
    var name = 'Javascript';
    var price = 100

    var course = {
        name: name,
        price: price ,
        // Viết kiểu thông thường 
        getName: function() {
            return name;
        }
        // Viết kiểu Enhanced
        getName() {
            return name;
        }
    }
    ```
- Định nghĩa key cho object dưới dạng biến 
    ```js
    var filedName = 'new-name';

    const course = {
        name: 'Javascript',
        [filedName] : 'Javascript'
    }
    ```
## Spread, rest
- Rest
    - Lấy ra phần còn lại sau `...`
        ```js
        function logger(...params) {
            console.log(params)
        }

        logger(1,2,4,5) // Sẽ in ra 1,2,4,5
        --
        function logger(a,b,...params) {
            console.log(params)
        }

        logger(1,2,4,5) // Sẽ in ra 4,5
        ```
- Spread
    - Gọi là toán tử dải 
    - Thường dùng để nối chuỗi 
        ```js
        var array1 = ['JS', 'PHP', 'Ruby']

        var array2 = ['Dart', 'Flutter']

        var array3 = [...array2, ...array1]
        ```
        - `...array2`: Sẽ bỏ `[]` và chỉ lấy `'Dart', 'Flutter'`
    
## var let const 
- `var`: Có thể khai báo lại và cập nhật gía trị(Tuy nhiên thì cái khai báo lại có thể xảy ra rất nhiều lỗi và không biết lỗi ở đâu)
- `let`: Có thể cập nhật và không thể khai báo lại
- `const`: Không thể cập nhật và khai báo lại
    - Tuy nhiên thì những cái được gán ở bên trong thì có thể chỉnh sửa thoải mái
        ```js
        const buaAn = {
            anTrua: 'com,
            anToi: 'Pho
        }

        buaAn.anTrua = 'bun dau'
        ```
        - Có thể sử dụng trong array & object

## Tham số mặc định 
- Tham số mặc định khi không truyền vào trong ES6
    ```js
    const Cong = (x, y = 2) => return x + y

    const tong = Cong(4) // Output: 6
    ```
## Template Literals
- Nối chuỗi trong ES5
    ```js
    const ten = 'Vu'
    const ho = 'Do'

    const.log('Ten toi la' + ho + '' + ten)
    ```
- Nối chuỗi trong ES6
    ```js
    const ten = 'Vu'
    const ho = 'Do'

    const.log(`Tao ten la ${ho} ${ten}`)
    ```

## Destructure 
- d
    ```js
    const buaAn = {
        buaSang: 'Banh My',
        buaTrua: 'Thit Cho'
    }

    const traiCay = ['Tao', 'Nho']

    console.log(`Sáng nay tao ăn ${buaAn.buaSang}`)
    console.log(`Trưa nay tao ăn ${buaAn.buaTrua}`)

    console.log(`Quả số 1 là: ${traiCay[0]}`)
    console.log(`Quả số 2 là: ${traiCay[1]}`)
- Làm như trên thì nó bị lặp lại `buaAn` va `traiCay` khá nhiều
- Sử dụng destructure
    ```js
    const {buaSang, buaTrua} = buaAn

    console.log(`Sáng nay tao ăn ${buaSang}`)
    console.log(`Sáng nay tao ăn ${buaTrua}`)

    const [Tao, Nho] = traiCay
 
    console.log(`Quả số 1 là: ${Tao}`)
    ```
    - Bẻ bữa ăn ra và lấy các giá trị của properties và gán vào từng biến

# Reduce
- Là dạng kiểu vòng lặp nhưng viết ngắn gọn hơn 
    ```js

    function coinHandler(accumulator, currentValue) {
        return accumulator + currentValue.coin
    }

    var totalCoin = courses.reduce(coinHandler, 0) //Initial value
    ```
    - accumulator: Là giá trị mà truyền biến thứ 2 của **reduce**
    - currentValue: Trả đúng thứ tự array 
- Có thể viết theo dạng es6
    ```js
    var totalCoin = courses.reduce((a, b) => {
        a + b.coin, 0
    })
    ```

# Filter
- Lọc ra các phần tử thỏa mãn điều kiện