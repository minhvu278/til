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
    
## Sitemesh decorator 
- Cách thức hoạt động: Dựa vào URL 
- Filter: Ví dụ là `/home` thì apply giao diện web còn `/admin` thì apply giao diện admin 


## SOLID
- S: Single responsibility principle
    - Giúp giảm sự phức tạp của 1 class: Mỗi class chỉ phục vụ cho 1 mục đích duy  nhất
    - Ví dụ thay vì xử lý 1 class ôm gồm 1 đống các xử lý 
        ```

            public class DBHelper {

                public Connection openConnection() {};

                public void saveUser(User user) {};

                public List<Product> getProducts() {};

                public void closeConnection() {};
            }
        ```
    - Thì ta nên tách riêng thành các class xử lý công việc riêng 
        ```
            public class DBConnection {

                public Connection openConnection() {};

                public void closeConnection() {};

            }

            public class UserRepository {

                public void saveUser(User user) {};
            }

            public class ProductRepository {

                public List<Product> getProducts() {};
            }
        ```
- O : Open/closed principle 
    - Khi triển khai các tính năng mới, thay vì sửa đổi code đã tồn tại thì ta nên mở rộng & kế thừa 
    - Ví dụ xử logic tính phí vận chuyển 
        ```
        public class Order {

            public long calculateShipping(ShippingMethod shippingMethod) {
                if (shippingMethod == GROUND) {
                    // Calculate for ground shipping
                } else if (shippingMethod == AIR) {
                    // Calculate for air shipping
                } else {
                    // Default
                }
            }
        }
        ```
        - Khi thêm 1 phương thức mới ta sẽ cần bổ sung thêm 1 case nữa vào -> khó quản lý
        - Vì thế nên ta nên tách rời vào 1 interface và các phương thức sẽ implement nó sẽ giúp code dễ nhìn và đọc hơn
            ```
            public interface Shipping {

                long calculate();
            }

            public class GroundShipping implements Shipping {

                @Override
                public long calculate() {
                    // Calculate for ground shipping
                }
            }

            public class AirShipping implements Shipping {

                @Override
                public long calculate() {
                    // Calculate for air shipping
                }
            }

            public class Order {

                private Shipping shipping;

                public long calculateShipping(ShippingMethod shippingMethod) {
                    // Find relevant Shipping implementation then call calculate() method
                }
            }
            ```
        
- Liskov substitution principle
    //NOTE: Đọc lại
    - Các đối tượng của class cha có thể được thay thế bởi các đối tượng của các class con mà không làm thay đổi tính đúng đắn của chương trình 
    ```
    public interface Animal {

        void fly();
    }

    public class Bird implements Animal {

        @Override
        public void fly() {
            // Flying...
        }
    }

    public class Dog implements Animal {

        @Override
        public void fly() {
            // Dog can't fly
            throw new UnsupportedOperationException();
        }
    }
    ```
    - class Dog đã vi phạm nguyên lý Liskov substitution.
    - Cách giải quyết ở đây sẽ là: tạo một interface FlyableAnimal như sau:
    ```
    public interface Animal {
    }

    public interface FlyableAnimal {

        void fly();
    }

    public class Bird implements FlyableAnimal {

        @Override
        public void fly() {
            // Flying...
        }
    }

    public class Dog implements Animal {
    }
    ```

- Interface segregation principle
    - Thay vì viết interface cho mục đích chung thì ta nên tách riêng ra nhiều interface nhỏ cho các mục đích riêng 
    - K nên bắt buộc implement các method mà client không cần đến
    - Ví dụ 
        - Chúng ta có một interface Animal như sau:
            ```
            public interface Animal {

                void eat();

                void run();

                void fly();
            }
            ```
            - Chúng ta có 2 class Dog và Snake implement interface Animal. Nhưng thật vô lý, Dog thì làm sao có thể fly(), cũng như Snake không thể nào run() được? Thay vào đó, chúng ta nên tách thành 3 interface như thế này:

            ```
            public interface Animal {

                void eat();
            }

            public interface RunnableAnimal extends Animal {

                void run();
            }

            public interface FlyableAnimal extends Animal {

                void fly();
            }
            ```

- Dependency inversion principle
    - Ý tưởng của nguyên lý này là các module cấp cao không nên phụ thuộc vào các module cấp thấp, cả hai nên phụ thuộc vào abstraction.

    - Ví dụ, chúng ta có 2 module cấp thấp BackendDeveloper và FrontendDeveloper và 1 module cấp cao Project sử dụng 2 module trên:

    ```
    public class BackendDeveloper {

        private void codeJava() {};
    }

    public class FrontendDeveloper {

        private void codeJS() {};
    }

    public class Project {

        private BackendDeveloper backendDeveloper = new BackendDeveloper();
        private FrontendDeveloper frontendDeveloper = new FrontendDeveloper();

        public void build() {
            backendDeveloper.codeJava();
            frontendDeveloper.codeJS();
        }
    }
    ```
    - Giả sử nếu sau này, dự án thay đổi công nghệ. Các backend developer không code Java nữa mà chuyển sang code C#. Các frontend developer không code JS thuần nữa mà nâng lên các JS framework. Rõ ràng chúng ta không những phải sửa code ở các module cấp thấp (BackendDeveloper và FrontendDeveloper) mà còn phải sửa code ở cả module cấp cao (Project) đang sử dụng các module cấp thấp đó. Điều này cho thấy module cấp cao đang phải phụ thuộc vào các module cấp thấp.

    - Lúc này, chúng ta sẽ bổ sung thêm một abstraction Developer để các module trên phụ thuộc vào:

    ```
    public interface Developer {

        void develop();
    }

    public class BackendDeveloper implements Developer {

        @Override
        public void develop() {
            codeJava();
            // codeCSharp();
        }

        private void codeJava() {};

        private void codeCSharp() {};
    }

    public class FrontendDeveloper implements Developer {

        @Override
        public void develop() {
            codeJS();
            // codeAngular();
        }

        private void codeJS() {};

        private void codeAngular() {};
    }

    public class Project {

        private List<Developer> developers;

        public Project(List<Developer> developers) {
            this.developers = developers;
        }

        public void build() {
            developers.forEach(developer -> developer.develop());
        }
    }
    ```
