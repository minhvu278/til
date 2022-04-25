## Spring
- Trước khi ra đời spring framework thì trước đây sử dụng JEE (Gồm những thứ như JSP, Servlet, JDBC,...)
- Spring framework ra đời khắc phục các nhược điểm của JEE 

## Spring framework
- Về phía phát triển web thì gồm có:
    - Spring MVC thuần túy 
    - Spring Boot (Có thể tạo ra được Spring MVC)

- Webservice: Gồm 2 nền tảng web và app. Ví dụ khi ta mua hàng trên web thì nó sẽ tự động đồng bộ vào app

- Spring data: 
    - Từ các version 3. đổ xuống thì muốn truy vấn dũ liệu thì phải tích hợp JPA, hibernate,...
    - Còn từ version 4. trở lên thì có sẵn công nghệ Spring Data JPA (Do spring framework cải tạo và phát triển riêng)

## MVC
- SpringWebApplication: implement từ WebApplication (Lấy các thông tin trong class này để init ứng dụng)
- ApplicationContexConfig: Sử dụng để khai báo Spring Bean. Chú thích bởi @Configuration 
- @ComponentScan("helloSpr.*"): Spring sẽ tìm kiếm các Spring khác và các controller trong các pakage `helloSpr`
- WebMvcConfig: Sử dụng để cấu hình các tài nguyên sử dụng trong MVC (Chẳng hạn như các nguồn tài nguyên tĩnh như css, js)
- 



















- Tạo `MyResponsitory`
    ```
    @Repository
    public class MyRepository {

        public String getAppName() {
            return "Hello Spring App";
        }

        public Date getSystemDateTime() {
            return new Date();
        }
        
        
    }
    ```
- `MyComponent`
    ```
    @Component
    public class MyComponent {
    
        @Autowired
        private MyRepository repository;

        public void showAppInfo() {
            System.out.println("Now is: "+ repository.getSystemDateTime());
            System.out.println("App Name: "+ repository.getAppName());
        }

    }
    ```
