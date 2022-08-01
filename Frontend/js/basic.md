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