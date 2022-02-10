# Java Spring Boot

## Web service là gì 
- Là ứng dụng client-server có thể giao tiếp được với nhau thông qua HTTP/HTTPS
- Các loại webservice: SOAP web service & RESTful web service 
- Là giải pháp giúp ứng dụng giao tiếp với nhau không phụ thuộc vào ngôn ngữ nền tảng
- Khác nhau giữa web và web service
    - Web thì hiển thị giao diện 
    - Web service thì hiển thị dữ liệu dạng thô (Như kiểu ta bấm Ctr + u)

## SOAP web service 
- Là viết tắt của Simple Object Access Protocol. Là giao thức dựa trên XML để truy cập các web service 
- Có thể tương tác với ứng dụng, ngôn ngữ lập trình khác
- Bảo mật tốt
- Chậm, tuân thủ nhiều tiêu chuẩn 

## RESTful web service 
- REST viết tắt của Representational State Transfer 
- Nhanh và chiếm ít băng thông hơn SOAP 
- Cho phép trả về nhiều định dạng dữ liệu về nhiều format khác nhau: Text, XML, HTML, JSON (Nên dùng Json)

## Tạo 1 project mới 
- Trong file pom.xml có 3 điểm cần lưu ý , Spring Boot giúp bạn đơn giản hơn trong việc khai báo thư viện spring 
- `spring-boot-starter-parent`
    - Là 1 project có sẵn trong Spring Boot. Các thư viện phụ thuộc cơ bản đã được khai báo trong spring-boot-starter-parent và ta chỉ cần thừa kế nó 
    ```
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.0.0.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    ```

- `spring-boot-starter-web`
    - Hiểu đơn giản là khi cần phát triển 1 ứng dụng web cần phụ thuộc vào `spring-boot-starter-web`
    ```
    <dependencies>

    <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-test</artifactId>
       <scope>test</scope>
    </dependency>

    </dependencies>
    ```
- `spring-boot-maven-plugin`
    - Cung cấp thư viện cần thiết giúp project có thể chạy trực tiếp mà không cần triển khai trên web server. Nó giúp tạo 1 file jar có thể thực thi 
    ```
    <plugins>

    <plugin>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-maven-plugin</artifactId>
    </plugin>

        <!-- ... -->

    </plugins>
    ```

## Chạy Spring Boot project 
- Khá giống với việc khi chúng ta code chạy console, cần 1 hàm main để chạy 
    ```
    @SpringBootApplication
    public class NewsApplication {

        public static void main(String[] args) {
            SpringApplication.run(NewsApplication.class, args);
        }
    }
    ```
    - @SpringBootApplication giúp tự động cấu hình Spring, tự động Scan toàn bộ project để tìm ra các thành phần Pring (Controller, Bean, Service, ...)
    - @SpringBootApplication <=> @Configuration + @EnableAutoConfiguration + @ComponentScan

## Các thuộc tính thông dụng của Spring Boot 
- Spring Boot Common Properties
    - application.properties: 
        - Mặc định sẽ chạy ở cổng 8080. Muốn thay đổi thì vào `resource/application.properties` để định nghĩa cổng muốn chạy 
            ```
            server.port=8088
            ```
    //TODO: Note sau 

## Sử dụng Spring Boot và Thymeleaf
- Thymeleaf là gì?
    - Là 1 Java XML/XHTML/HTML5 Template Engine, nó có thể làm việc với cả 2 môi trường Web và môi trường không phải web 
    - Các file mẫu của Thymeleaf bản chất chỉ là 1 file văn bản thông thường có định dạng XML/XHTML/HTML5.
    - Có thể sử dụng để thay thế cho JSP trên tầng View của ứng dụng web mvc
- Tạo ứng dụng 
    - Các file HTML muốn sử dụng được thì cần khai báo Thymeleaf namespace 
    ```
    <html xmlns:th="http://www.thymeleaf.org">
    ```
    - Thymeleaf Marker (Các đánh dấu của Thymeleaf), chúng là các chỉ dẫn giúp Thymeleaf Engine phân tích file mẫu và và kết hợp dữ liệu với Java để generate 1 tài liệu mới 
    ```
    <tr th:each ="person : ${persons}">
            <td th:utext="${person.firstName}">...</td>
            <td th:utext="${person.lastName}">...</td>
    </tr>
    ```
    - Sử dụng Context-Path trong Thymeleaf 
    ```
    <!-- Example 1:  -->

    <a th:href="@{/mypath/abc.html}">A Link</a>

    Output: ==>

    <a href="/my-context-path/mypath/abc.html">A Link</a>


    <!-- Example 2:  -->

    <form th:action="@{/mypath/abc.html}"
            th:object="${personForm}" method="POST">

    Output: ==>

    <form action="/my-context-path/mypath/abc.html"  method="POST">
    ```

## Sử dụng Spring Boot, Apache Titles, JSP
- Apache Titles giúp định nghĩa ra 1 khuôn mẫu để ghép các phần lại với nhau (Dễ hiểu hơn là nó giống như cắt giao diện)
