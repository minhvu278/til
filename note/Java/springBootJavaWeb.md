# Note

- @Autowired: Tạo ngay khi chương trình chạy
- @Bean : Chạy ngay khi app được chạy 

## Viết api web service
- File pom.xml
    - <parent> : Kế thừa lại từ 1 project parent spring boot 
    ```
        <parent>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-parent</artifactId>
            <version>1.5.22.RELEASE</version>
        </parent>
    ```
- Tạo thử 
    - Tạo class `NewApplication.java`
        ```
        import org.springframework.boot.SpringApplication;
        import org.springframework.boot.autoconfigure.SpringBootApplication;

        @SpringBootApplication
        public class NewsApplication {

            public static void main(String[] args) {
                SpringApplication.run(NewsApplication.class, args);
            }

        }
        ```
    - Tạo class `NewAPI`
    ```
    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.RestController;

    @RestController
    public class NewAPI {
        @GetMapping("/test")
        public String testAPI() {
            return "Success";
        }
    }
    ```
- Mặc định sẽ chạy ở cổng 8080. Muốn thay đổi thì vào `resource/application.properties` để định nghĩa cổng muốn chạy 
    ```
    server.port=8088
    ```

## H2 Database
- In-memory Database, sử dụng để test trước (Không cần cài mysql)

## Tìm hiểu về 1 số cái @
- @RequestBody: nhận dữ liệu json được truyền từ client vào server
- @ResponseBody: trả kết quả json từ server về client
- @RestController = @Controller + @ResponseBody

- Sử dụng controller
    ```
    @Controller
    public class NewAPI {
        @RequestMapping(value = "/new", method = RequestMethod.POST)

        @ResponseBody
        public NewDTO createNew(@RequestBody NewDTO model) {
            return model;
        }
    }
    ```
- Sử dụng RestController:
    ```
    @RestController
    public class NewAPI {

        @PostMapping(value = "/new")
        public NewDTO createNew(@RequestBody NewDTO model) {
            return model;
        }
    }
    ```
## Spring data jpa 
- JDBC -> JPA -> Spring data jpa 
- JBDC phụ thuọc hoàn toàn vào database. Vì thế khi mà thay đổi thì gần như là phải đập đi xây lại 
- Spring data jpa sẽ không phụ thuộc vào database mà sẽ phụ thuộc vào entity (entity nó là java class) 
    - Ví dụ có 3 bảng new, user, comment -> thì ta sẽ tạo ra 3 java class: newentity, userentity, commententity
        - new sẽ mapping với newentity 
    - Khi phụ thuộc vào entity, nó sẽ xuất hiện 1 cái là HQL(Hiberbate query language) nghĩa là ta sẽ không sử dụng query thuần nữa
    - Tất cả dữ liệu sẽ đẩy hết vào entity và nhiệm vụ của data jpa cầm entity đấy lưu xuống là xong -> sẽ rất gọn 
- Khi làm việc với spring data jpa 
    - Gọi spring data jpa 
        ```
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
        ```
    - Khai báo mysql connector trong spring boot 
        ```
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.22</version>
        </dependency>
        ```
- Để nó hiểu đó là entity ta cần khai báo thêm `@Entity`
- Và để nó map được với DB thì cần sử dụng `@Table`
    ```
        @Entity
        @Table(name = "user") //user là tên bảng trong DB 
        public class UserEntity {
        }
    ```
- Muốn cho cái nào làm primary key thì ta chỉ cần cho `@Id` 
    - `@Id` sẽ có 2 chức năng là not null và primary key 
- Và để cho có thể tự động tăng thì ta sử dụng `@GeneratedValue`
    ```
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)\
    ```
- `@Column` - Note sau 