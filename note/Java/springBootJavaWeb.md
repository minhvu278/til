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
- `@Column`: Tạo được column trong table 
    ```
    @Column
    private String userName;
    ```

    - Khi thiết kế tất cả các field thì cần có `@Column` ở đầu 
    - `@Column(name = "")`
        - name ở đây có nghĩa là trong MySql muốn tên là gì thì viết vào trong (Thực ra cũng không cần thiết là phải viết name)
        - Nếu không viết name thì nó sẽ dựa vào tên biến để cho vào CSDL 
            ```
            @Column(name = "title")
            private String title; // Nếu k viết name mặc định sẽ lấy biến title để ghi vào CSDL
            ```
- `@MappedSuperClass`: Với annotation này thì khi tạo table từ các entity thì nó sẽ hiểu là 

- Trong JBDC thì khi connect DB thì cần load driver, còn trong Spring boot thì chỉ cần khai báo vào trong file `pom.xml`
- Còn những cái như url, username, password thì ta phải khai báo trong `application.properties`
    ```
    spring.datasource.url = jdbc:mysql://localhost:3306/newspringboot
    spring.datasource.username = root
    spring.datasource.password = 1234

    #spring.jpa.hibernate.ddl-auto = none // Câu lệnh này hỗ trợ create table từ entity 
    spring.jpa.hibernate.ddl-auto = create-drop // Drop table cũ đi và tạo lại 

    spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.MySQL5Dialect // Tùy vào sử dụng CSDL gì 
    ```

- Với quan hệ many to many 
    - Với quan hệ này thì ta cần tạo 1 bảng chung gian 
        - Ví dụ như bảng user và bảng role quan hệ many to many thì phải tạo ra bảng trung gian là user_role 
        ```
        @ManyToMany(cascade = {
        CascadeType.PERSIST,
        CascadeType.MERGE
        })
        @JoinTable(name = "post_tag",
            joinColumns = @JoinColumn(name = "post_id"), // Khoá ngoại 
            inverseJoinColumns = @JoinColumn(name = "tag_id") // Khoá ngoại 
        )
        ```

## Thêm dữ liệu sử dụng spring data jpa và restful webservice 
- Packge `repository`
    - Nó sẽ tương tự như là DAO bên jdbc 
    ```
    public interface NewRepository extends JpaRepository<NewEntity, Long> { 
        //
    }
    ```
    - Cần truyền vào 2 tham số là bảng muốn thao tác và kiểu dữ liệu của primary key
- Để repository có thể @Autowired nhúng vào service thì trong repository phải khai báo `@Repository`
- Và ví dụ như tầng API muốn sử dụng service thì cũng phải @Autowired service vào api -> và để @Autowired thì trong service cũng phải có `@Service`

- Để service có thể sử dụng được repository thì ta phải nhúng nó vào 
    ```
        public class NewService implements INewService {
            @Autowired
            private NewRepository newRepository;
        }
    ```
- Để nhúng được thì thằng repository phải có kí hiệu là thằng repository nào muốn nhúng vào thằng service (Khai báo `@Repository` ở trước)

- Tuy nhiên ở trong Spring boot thì chúng ta không cần khai báo `@Repository` vì `JpaRepository` đã viết sẵn hết rồi
    - Do đó class nó implement là class nó implement từ thằng `JpaRepository`và trong đó nó đã khai báo sẵn `@Repository` rồi. Vì thế nên ta k cần khai báo nữa 

- Vì cái chúng ta nhận vào là newDTO(`public NewDTO save(NewDTO newDTO)`) mà cái lưu xuống DB là newEntity nên ta phải convert 

## Update dữ liệu 
- Khi update thì ta cần lấy lại dữ liệu cũ của nó 
- Trong data jpa thì có hỗ trợ sẵn hàm `findOne(id)` (Tương tự như câu sql: select * from new where id = 1)
    ```
    NewEntity oldNewEntity = newRepository.findOne(newDTO.getId());
    ```


## Restful api
