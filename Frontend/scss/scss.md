# Scss là gì
- Là 1 bản nâng cấp của Sass giúp viết code 1 cách dễ dàng & dễ hiểu hơn 

## Quy tắc xếp chồng
- Ví dụ đoạn HTML
    ```html
     <div class="container">
        <div class="row">
            <div class="navbar col-12">
                <a class="brand">Viblo</a>
                <ul class="menu">
                    <li><a href="#">Menu 1</a></li>
                    <li><a href="#">Menu 2</a></li>
                </ul>
            </div>
        </div>
    </div>
    ```
    - Với css thuần thì ta phải viết khá là dài 
        ```css
        .navbar ul.menu {
            list-style: none;
        }
        .navbar ul.menu li {
            padding: 5px;
        }
        .navbar ul.menu li a {
            text-decoration: none;
        }
        ```
    - Còn với scss thì nhìn gọn và clear hơn 
        ```css 
        .navbar {
            ul.menu {
                list-style: none;

                li {
                    padding: 5px;

                    a {
                        text-decoration: none;
                    }
                }
            }
        }
        ```
## Biến 
- Khi trong code có nhiều chỗ sử dụng giống nhau(Ví dụ như màu chủ đạo trong code) thì ta nên đặt 1 biến để có thể sử dụng lại 
- Để khai báo thì sử dụng `$`
    ```css
    $whiteColor = #fff;

    .navbar {
        ul.menu {
            list-style: none;

            li {
                padding: 5px;

                a {
                    text-decoration: none;
                    color: $whitecolor
                }
            }
        }
    }
    ```

## Quy tắc mixin 
- Là 1 cơ chế khá phổ biến.
- Nó mang nhiều thuộc tính mà ta đã quy ước trong 1 `mix` nào đó rồi `@include` vào 1 thành phần bất kì mà không phải viết lại các thuộc tính đó
    ```css
    @mixin colorVsFont {
    color: #fff;
    font-size: 50px;
    }

    .navbar {
        ul.menu {
            list-style: none;

            li {
                padding: 5px;

                a {
                    text-decoration: none;
                    @include colorVsFont;
                }
            }
        }
    }
    ```
- Hoặc nếu không muốn lúc nào cũng là `#fff` thì ta có thể truyền thuộc tính vào mix như 1 tham số 
    ```css
    @mixin colorVsFont($color, $fontSize) {
    color: $color;
    font-size: $fontSize;
    }

    .navbar {
        ul.menu {
            list-style: none;

            li {
                padding: 5px;

                a {
                    text-decoration: none;
                    @include colorVsFont(#000, 50px);
                }
            }
        }
    }
    ```

## Extends
- Giống với OOP (Lớp con kế thừa lớp cha). Ta chỉ cần định nghĩa ra class rồi những tag nào cần sử dụng thì ta `extend` nó là được 
    ```css 
    .title-box {
        color: #dacb46;
        text-shadow: 1px 1px 1px #1a1a1a;
        display: inline-block;
        text-transform: uppercase;
    }

    .navbar {
        ul.menu {
            list-style: none;

            li {
                padding: 5px;

                a {
                    text-decoration: none;
                    @extend .title-box;
                }
            }
        }
    }
    ```

## Khi nào nên sử dụng @mixin và @extend 
- Sử dụng @mixin khi có nhiều thứ cần thay đổi 
- Sử dụng @extend khi ta biết chắc rằng nó sẽ không thay đổi thứ gì bên trong(Ví dụ như màu mặc định của trang web)


## Import 
- Khá giống với cách mà `require` hay `include` trong php 
- Khi css cho 1 trang web ta tách ra các phần riêng để dễ code, sửa, tìm kiếm hơn 
- Ví dụ code 3 phần `header, body, footer`: 
    - Tạo ra 3 file để code 
        - _header.scss
        ```css 
        #header {
            // code sass here
        }
        ```
        - _body.scss
        ```css 
        #body {
            // code sass here
        }
        ```
        - _footer.scss
        ```css 
        #footer {
            // code sass here
        }
        ```





