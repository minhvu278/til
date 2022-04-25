# Java Servlet/JSP
- Là chương trình chạy trên 1 web hoặc ứng dụng máy chủ
- Hành động như 1 lớp trung gian giữa request từ trình duyệt web hoặc client và CSDL hoặc các ứng dụng trên máy chủ HTTP

## Vòng đời của Servlet
- Tải lớp Servlet vào bộ nhớ 
- Tạo đối tượng Servlet 
- Gọi phương thức init() của Servlet
- Gọi phương thức service() của Servlet 
- Gọi phương thức destroy

- Request gửi đến nếu đối tượng chưa đc tạo thì sẽ tạo đối tượng mới bằng PT init() --> gọi vào hàm service

## Cấu hình Servlet bằng XML 
- File web.xml để cấu hình servlet -> tomcat sẽ đọc từ đây ra 
    ```
    -- thẻ servlet để map tên servlet đó với tên class 
    <servlet>
        <servlet-name>helloServlet</servlet-name>
        <servlet-class>com.example.demo.HelloServlet</servlet-class> -- tên package + tên class
    </servlet>

    <!-- Định nghĩa đường dẫn truy cập vào Servlet này -->
    <servlet-mapping>
        <servlet-name>helloServlet</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
    ```

## Tạo servlet bằng Annotation 
- Có thể sử dụng để định nghĩa đường dẫn 1 cách nhanh chóng 
- Viết ngay trong class
    ```
    @WebServlet(urlPatterns = {"/hello", "/xin-chao"})
    ```

## Request & response
- Req: Client gui len server
- Res: Serve tra ve client

## Servlet config
- Sử dụng init param 
    ```
    @WebServlet(urlPatterns = {"test-config"}, initParams = {
        @WebInitParam(name="name", value = "Minh Vu")
    })
    public class HelloServlet extends HttpServlet {

        @Override
        protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
            String name = super.getServletConfig().getInitParameter("name");
            resp.setContentType("text/html");

            PrintWriter writer = resp.getWriter();
    ```

## HTTP response code
- 100 : Tiếp tục
- 200 : Trả về thành công
- 301 : Chuyển hướng (Đường dẫn này chuyển sang đường dẫn khác)
- 401 : Yêu cầu xác thực
    - 403 : Tài nguyên bị hạn chế
    - 404 : Không tìm thấy 
- 500 : Serve lỗi

## Đọc giá trị gửi từ client -> url
- Nhập giá trị trên url & in ra màn hình sử dụng getParameter
    ```
    String ten = req.getParameter("ten");
    ```

## Redirect 
- Sử dung:
    - C1: resp.sendRedirect()
    - C2: 
        ```
        resp.setStatus(resp.SC_MOVED_PERMANENTLY);
        resp.setHeader("Location", "https://minhvu.com");
        ```

## Cookie 
- Là 1 file text lưu ở browser 
- Lưu duwosi dạng key/value 
- Req sẽ gửi thông tin Cookies trong header mỗi lần gọi
- Java Servlet hỗ trợ HTTP cookie 
- Có thời gian sống xác định 

## Session
- Lưu thông tin ở phía server
- HttpSession : là 1 interface trong Servlet giúp lưu thông tin người dùng qua servlet khác nhau 
    ```
    HttpSession session = request.getSession();
        -- getSession: Sẽ tạo ra 1 session mới nếu trên serve chưa có hoặc đọc lại nếu trên serve đã có 
    ```
- Cách hoạt động của session 
    - Set id vào cookie để nhận dạng
    - Set id vào 1 trường ẩn trong form (Đặt type="hidden")
    - Trên url : VD: http://minhvu278.com/file.html;sessionid=1334;

## Filter 
- Cũng có 3 hàm init, doFilter, destroy
- Dùng để kiểm tra trước khi gọi đến và kiểm tra cả khi trả về
- Là đối tượng dùng để xử lý request trước khi gọi đến servlet đích và res trả về kết quả từ servlet
- Thường dùng để : Logging, nén file, validate,...
    ```
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        System.out.println("Filter"); -- Xử lý req đến

        filterChain.doFilter(servletRequest, servletResponse); -- Kiểm tra xem có cho phép đi đến filter tiếp theo (Hay là servlet đích)

        servletResponse.setContentType("text/plain"); -- Xử lý res
    }
    ```
- Có thể sử dụng Java config
    ```
    @WebFilter(urlPatterns = {"/*"}) -- Mọi req gọi tới đều phải đi qua filter 
    ```

## Trả về trang error
- Cấu hình trong web.xml
    ```
    <error-page>
        <error-code>404</error-code>
        <location>/handle-error</location> -- Trang hien thi loi tra ve
    </error-page>

## Servlet context 
- Lấy đối tượng servlet context từ class cha

## Servlet dispatcher
- Phân phối request đến các nguồn tài nguyên khác 
- 2 phương thức chính là forward() và include()
    - forward(): Khi request gửi đến servlet 1 -> forward sang servlet 2 và từ servlet 2 trả về trực tiếp 
    - include(): Khi request gửi đến servlet 1 -> include sang servlet 2 và từ servlet 2 trả về cho servlet 1 rồi mới respose  

## Khái niệm về Principal và Role 
- Role: Là tập hợp các quyền(Permission) đối với 1 ứng dụng
- Principal có thể tạm hiểu là 1 chủ thể sau khi đăng nhập họ có thể làm điều gì đó trong hệ thống (Phụ thuộc vào phân quyền)


## Servlet 
- Là gì? 
    - Là chương trình chạy trên 1 web hoặc ứng dụng máy chủ 
    - Như 1 lớp trung gian giữa 1 yêu cầu từ 1 trình duyệt web 