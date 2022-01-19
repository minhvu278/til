# Spring Framework
- Cấu trúc:
    - IoC Container: Là phần quan trọng nhất giữ vai trò cấu hình và quản lý vòng đời của đối tượng java 
    - DAO, 

## Code
- @Service: là 1 annotation để nói với Spring rằng đó là 1 Spring BEAN
- @Autowired: Được chú thích trên 1 field để nói với Spring hãy gán giá trị cho trường đó
- @Responsitory: Là 1 annotation được sử dụng để chú thích trên 1 class là 1 Spring BEAN 


# Tutorial

## Lesson 1: Cấu hình 
- Tạo maven project
- Cấu hình :
    - Version: 1.0
    - Packaging: war
- File pom.xml: 
    - Để định hình được là Spring MVC thì cần có thẻ <dependencies>
    - Để lấy các thư viện có sẵn của maven thì cần vào `Maven responstory`
    - Các thư viện cần có : 
        - Sping Mvc
        - Servlet(Java servlet api)

## Lesson 2: Tạo ứng dụng web
- Tạo controller cần khai báo ở đầu thêm @Controller để nó hiểu đó là controller 
    ```
    @Controller
    public class HomeController {

    }
    ```
- @RequestMapping : Để controller hiểu là muốn chuyển đến trang nào 
    ```
    @RequestMapping("/")
    
    public String Index() {
        return "index" // Trỏ đến file index.jsp ở trong webapp
    }
    ```
- Tuy nhiên thì đầu tiên khi chạy nó sẽ chạy vào web.xml trước nên ta cần khai báo trong web.xml trước
    ```
    <servlet>
        <servlet-name>diamond-config</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <load-on-startup>1</load-on-startup>
    </servlet>

    <servlet-mapping>
        <servlet-name>diamond-config</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
    ```
    

