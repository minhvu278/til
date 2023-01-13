# Set get giá trị các thuộc tính element 
- Cách get set giá trị
    ```js
    $('#link').attr('href', 'google.com.vn');

    //HTML 
    <a href='#' id="link">Click here</a>
- Khác nhau giữa attr() và prop() - properties
    - Đều set get sử dụng như nhau 
        - prop() trong trường hợp trả về true false (vd radio, checkbox,...)
        - attr() trả về giá trị bên trong thuộc tính đó (như vd trên trả về **google.com.vn**)
- Các phương thức: 
    - text(): Gán hoặc lấy nội dung thuần văn bản từ phần tử 
    - html(): Gán hoặc lấy về nguyên phần giá trị của HTML
    - val(): Gán hoặc lấy giá trị của trường - Lấy giá trị value trong html