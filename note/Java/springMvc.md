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
- Tiếp theo là cần tạo 1 file bean. Vd tạo spring bean có tên là `diamond-config.xml`
    - `web.xml` sẽ chạy vào `diamond-config.xml`. File `diamond-config.xml` sẽ quét toàn bộ các pakage ở trong src/main/java
    - Để quét được thì ta cần sử dụng `context:component-scan`
    ```
    xmlns:context="http://www.springframework.org/schema/context" //Lưu ý là phải khai báo những thằng này thì mới chạy được
    xsi:schemaLocation="http://www.springframework.org/schema/context/spring-context-4.3.xsd"

    <context:component-scan base-package="DiamondShop" />
    ```
- Để có thể cho mặc định khi chạy ứng dụng vào luôn file nào thì ta sử dụng `InternalResourceViewResolver`
    ```
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/views/"></property>
        <property name="suffix" value=".jsp"></property>
    </bean>
    ```

- Sử dụng `decorator` . Tạo file `decorators.xml` (Để sử dụng được decorator thì phải có sitemesh)
    ```
    <decorators defaultdir="/WEB-INF/views/layouts"> // Đường dẫn mặc định 
        <decorator name="user" page="user.jsp"> // Khi là user thì sẽ sử dụng master layout là user.jsp
            <pattern>/*</pattern>
        </decorator>

        <decorator name="admin" page="admin.jsp"> 
            <pattern>/admin/*</pattern>
        </decorator>
    </decorators>
    ```
- Sử dụng sitemesh cần vào maven responstory để lấy 
    - Cần cấu hình filter ở `web.xml`
    ```
    <filter>
        <filter-name>sitemesh</filter-name>
        <filter-class>com.opensymphony.sitemesh.webapp.SiteMeshFilter</filter-class>
        <init-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>/WEB-INF/diamond-config-servlet.xml</param-value>
        </init-param>
    </filter>

    <filter-mapping>
        <filter-name>sitemesh</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
    ``` 

## Lesson 3: Tạo giao diện trang chủ
- Thêm thư viện jstl  
    ```
    <!-- jstl/jstl -->
    <dependency>
      <groupId>jstl</groupId>
      <artifactId>jstl</artifactId>
      <version>1.2</version>
    </dependency>
    ```
- Để sử dụng được ta cần 1 cái taglib 
    ```
    <%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
    ```
    - Sử dụng trong các link như bootstrap, js, img,...
        ```
        <link href="<c:url value="/assets/user/css/bootstrap.css" />" rel="stylesheet"/>
        ```
    - Tuy nhiên để nhận được thì cần thêm 1 annotation driven nữa 
        ```
        <mvc:annotation-driven />
        <mvc:resources mapping="/assets/**" location="/assets/" />
        ```
## Lesson 4: Tạo cấu trúc thư mục dự án 
- Dao: Tương tác với DB 
- Entity: Map với DB (Tức là table có các field, column nào nó sẽ map vào đây)
- Service tương tác với Dao 
- Dto: Dùng trong các trường hợp như khi muốn tương tác với các bảng join với nhau 
## Lesson 5: Kết nối với MySql 
- Sử dụng `jdbc` và mysql connector để kết nối
    ```
    <!-- spring-jdbc -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>${spring-version}</version>
    </dependency>
    ```
    
    - Khai báo các thông số 
        ```
        <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
            <property name="driverClassName" value="com.mysql.jdbc.Driver"></property>
            <property name="url" value="jdbc:mysql://45.252.251.17:3306/lniiftlt_diamondshop"></property>
            <property name="username" value="lniiftlt_minhvu"></property>
            <property name="password" value="minhvu@123"></property>
        </bean>
        ```
- Vd tương tác với DB sliders có các field tương ứng `id`, `img`, `caption`, `content`
    - Đầu tiên cần tạo ra 1 file để tương tác với các filed trong DB trong Entity
        ```
        public class Sliders {
            private int id;
            private String img;
            private String caption;
            private String content;

            public Sliders() {
                super();
            }

            public int getId() {
                return id;
            }

            public void setId(int id) {
                this.id = id;
            }

            public String getImg() {
                return img;
            }

            public void setImg(String img) {
                this.img = img;
            }

            public String getCaption() {
                return caption;
            }

            public void setCaption(String caption) {
                this.caption = caption;
            }

            public String getContent() {
                return content;
            }

            public void setContent(String content) {
                this.content = content;
            }
        }
        ```
    - Tiếp theo cần tạo 1 Mapper để nhận các dữ liệu của DB
    ```
    public class MapperSliders implements RowMapper<Sliders> {

        @Override
        public Sliders mapRow(ResultSet rs, int i) throws SQLException {
            Sliders sliders = new Sliders();
            sliders.setId(rs.getInt("id"));
            sliders.setImg(rs.getString("img"));
            sliders.setCaption(rs.getString("caption"));
            sliders.setContent(rs.getString("content"));
            return sliders;
        }
    }
    ```
    - RowMapper dùng để chuyển đổi dữ liệu từ câu lệnh query select -> các đối tượng mong muốn

    - Tiếp theo cần tạo ra file Dao để lấy dữ liệu ra
    ```
    @Repository
    public class SliderDao{
        @Autowired
        public JdbcTemplate _jdbcTemplate;

        public List<Sliders> GetDataSlider() {
            List<Sliders> list = new ArrayList<Sliders>();
            String sql = "SELECT * FROM sliders";
            list = _jdbcTemplate.query(sql, new MapperSliders());
            return list;
        }
    }
    ```
    - Lấy dữ liệu ra ở controller 
    ```
    public class HomeController {
        @Autowired
        SliderDao sliderDao ;

        @RequestMapping(value = {"/", "/home"});

        public ModelAndView mv = new ModelAndView("user/index");

        mv.addObject("sliders", sliderDao.GetDataSlider());
        return mv;
    }
    ```

## Lesson 6: Hiển thị dữ liệu động 
- Sử dụng forEarch. VD lấy ra danh sách các slider
    ```
    <c:forEach var="item" items="${ sliders }" varStatus="index">
        <c:if test="${ index.first }">
            <div class="item active">
        </c:if>
        <c:if test="${ not index.first }">
            <div class="item">
        </c:if>
        <img style="width: 100%"
                src="<c:url value="/assets/user/img/slider/${ item.img }"/>"
                alt="bootstrap ecommerce templates">
        <div class="carousel-caption">
            <h4>${ item.caption }</h4>
            <p>
                <span>${ item.content }</span>
            </p>
        </div>
        </div>
    </c:forEach>
    ```
    - var="item" : Mỗi item là 1 phần tử trong slider 
    - items="${sliders}": Danh sách sliders 
    - varStatus="" : Biến tự tăng bắt đầu bằng 0
    
- Vì 1 Dao chỉ tương tác được với 1 table vì thế cần phải gọi vào service -> từ service gọi sang Dao 
    - Tạo 1 interface `IHomeService`
        ```
        public interface IHomeService {
            @Autowired
            public List<Sliders> GetDataSlider();
        }
        ```
    

