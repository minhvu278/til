# Css module 
- Sử dụng để tạo ra các css độc lập và không ảnh hưởng đến nhau (Có thể trùng class)
- Thêm .module vào sau file css: `header.css -> header.module.css`
- Webpack sẽ nhận diện và lấy content của **header.module.css** để xử lý và nó sẽ export ra 1 object & có thể đặt tên cho nó 
    ```js
    import styles from './header.module.css'
    ```
- Để sử dụng thì chỉ cần chọc vào đúng cái key của nó 
    - File css 
    ```css 
    .paragraph {
        color: lightseagreen;
    }
    ```
    - Sử dụng: 
    ```js
    <p className={styles.paragraph}>Ok baeeee</p>
    ```
## Lưu ý
- Không sử dụng với tag name: *, h1,... sẽ ảnh hưởng đến tất cả (Dùng scss đi qua 1 cấp cha thì mới không bị ảnh hưởng)
- Đặt tên theo camelCase 
- Không kế thừa được
## Thư viện clsx và classnames
- Để có thể sử dung được nhiều class khi dùng css module: 
    ```css 
    .paragraph {
        color: lightseagreen;
    }
    .active {
        background-color: green
    }
    ```
    - Sử dụng: 
    ```js
    <p className={`${styles.paragraph} ${styles.active}`}>Ok baeeee</p>
    ```
- Sử dụng thư viện clsx nó sẽ gọn hơn
    ```js
    <p className={clsx(styles.paragraph, styles.active)}>Ok baeeee</p>
    ```
- Có thể sử dụng để ẩn hiện 
    ```css 
    .paragraph {
        color: lightseagreen;
    }
    .active {
        background-color: green
    }
    ```
    - Sử dụng: 
    ```js
    <p className={clsx(styles.paragraph, {
        [styles.active]: true //false se an di
    })}>
    Ok baeeee
    </p>
    ```