# Note 

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