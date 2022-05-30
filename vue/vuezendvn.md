# Install vue
- CP
    ```js
    npm install -g @vue/cli
    ```
# Vue instance 
- Quản lí 1 thành phần trong trang web 
    ```js
    <div id="app"></div>

    //Vue instance quản lí `app`
    var vueInstance  = new Vue({
        el: "#app"
    })
    ```

# Data Biding 
- Binding dữ liệu 
    ```js
    <div id="app">
        <p>{{title}}</p> //Hien thi abc
    </div>

    var vueInstance  = new Vue({
        el: "#app",
        data: {
            title: "abc"
        }
    })
    ```
- 1 số trường hợp là Attributes thì phải sử dụng `v:bind`
    ```js
    <div id="app">
        <a v-bind:href="url">{{title}}</a>  //Khi sử dụng v:bind thì nó sẽ coi url là 1 biến chứ không phải 1 chuỗi
    </div>

    var vueInstance  = new Vue({
        el: "#app",
        data: {
            title: "abc",
            url: "https://viblo.asia/p/xay-dung-api-voi-laravel-djeZ1RjGlWz"
        }
    })
    ```

# Sử dụng v-on để xử lý sự kiện 

- Không truyền tham số
    ```js
    <div id="app">
        <h1>Count: {{count}}</h1>
        <button v-on:click="handleClick">Click</button>
    </div>

    var vueInstance  = new Vue({
        el: "#app",
        data: {
            count: 0,
        },
        methods: {
            handleClick(e){
                this.count += 1
            }
        }
    })
    ```

- Truyền tham số
    ```js
    <div id="app">
        <h1>Count: {{count}}</h1>
        <button v-on:click="handleClick($event, 5)">Click</button>
    </div>

    //Script
    var vueInstance  = new Vue({
        el: "#app",
        data: {
            count: 0,
        },
        methods: {
            handleClick(e, number){
                this.count += number
            }
        }
    })
    ```
## Event modifier 
- Khi tạo form mà khi bấm submit không muốn chuyển hướng thì sẽ dùng `e.preventDefault`
- Còn sử dụng event modifier chỉ cần `.` sau tên sự kiện
    ```js
    <form action="/action_page.php" v-on:submit.prevent="handleSubmitForm">
    <label for="fname">First name:</label>
    <input type="text" id="fname" name="fname"><br><br>
    <input type="submit" value="Submit">
    </form>
    
    //Script
    var vueInstance  = new Vue({
        el: "#app",
        data: {
            count: 0,
        },
        methods: {
            handleSubmitForm(e){
               
            }
        }
    })
    ```

# Computed
- Khác nhau giữa `computed` và `method` 
    ```js
    <div id="app">
        <button v-on:click="a++">A = A + 1</button>
        <button v-on:click="b++">B = B + 1</button>
    </div>

    var vueInstance  = new Vue({
        el: "#app",
        data: {
            count: 0,
        },
        methods: {
            handleClick(e){
                this.count += 1
            }
        }
    })
    ```

