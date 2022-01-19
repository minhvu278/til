- Servlet là gì
    - Là công nghệ được sử dụng để tạo ra ứng dụng web
    - Là 1 API cung cấp các interface và lớp bao gồm các tài liệu 
    - Là 1 thành phần web được triển khai trên máy chủ để tạo ra web động

- Vòng đời của 1 servlet 
    - Có 5 bước: 
        - Load class Servlet vào bộ nhớ (-- Bước 1,2,3 được thực thi 1 lần duy nhất khi Servlet được chạy lần đầu)
        - Tạo đối tượng servlet 
        - Phương thức init()
        - Phương thức service() (-- Thực thi nhiều lần mỗi khi có đòi hỏi từ user đến servlet)
            - service sẽ gọi 1 trong 2 phương thức là doGet() hoặc doPost()
        - Phương thức destroy() (-- Thực thi khi gỡ bỏ servlet)

- Tìm hiểu về web.xml trong servlet 
    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <welcome-file-list>
        <welcome-file>index.html</welcome-file>
        <welcome-file>index.jsp</welcome-file>
        <welcome-file>hello.html</welcome-file>
        <welcome-file>hello.jsp</welcome-file>
    </welcome-file-list>
    </web-app>
    ```
    - Khi chạy ứng dụng, không nhập gì vào url thì nó sẽ tìm 1 trong những file có trong thẻ <welcome-file-list> để hiển thị ra 

- Tạo servlet 
    - Ta cần extends Servlet 
        ```
        public class HelloServlet extends HttpServlet {
            //Code
        }
        ```

    - Để có thể truy cập vào servlet thì có 2 casch:
        - C1: Khai báo trong web.xml
            ```
            <servlet>
                <servlet-name>helloServlet</servlet-name> -- Tên của servlet
                <servlet-class>org.o7planning.tutorial.servlet.HelloServlet</servlet-class> -- tên package + tên class
            </servlet>

            <!-- Định nghĩa đường dẫn truy cập vào Servlet này -->
            <servlet-mapping>
                <servlet-name>helloServlet</servlet-name>  -- Tên của servlet
                <url-pattern>/hello</url-pattern>  -- URL của servlet
            </servlet-mapping>
            ```
        - C2: Ngắn gọn hơn tạo bằng Annotation (Với cách viết này ta có thể viết nó ngay trong class)
             ```
            @WebServlet(urlPatterns = {"/hello", "/xin-chao"}) -- Có thể truyền đươc nhiều url
            ```
    - Gửi dữ liệu về phía người dùng ta có thể sử dụng ServletOutputStream hoặc PrintWrite 
        - ServletOutputStream
            ```
            	ServletOutputStream out = response.getOutputStream();

                out.println("<html>");
                out.println("<head><title>Init Param</title></head>");
            ```
        - PrintWrite  
            ```
            PrintWriter printWriter = resp.getWriter();

            printWriter.println("<form action='login' method='post'>");
            printWriter.println("Username: <input type='text' name='username'>");
            printWriter.println("Password: <input type='password' name='password'>");
            printWriter.println("<input type='submit' value='login'>");
            printWriter.println("'</form>'");

            printWriter.close();
            ```

- Servlet config 
    - Truyền tham số khởi tạo sử dụng initParams
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

- URL Pattern
    ```
    http://localhost:8080/ServletTutorial/spath/abc/mnp?date=today
    ```
    - ServletTutorial --> contextPath
    - spath  --> servletPath
    - abc/mnp  --> pathInfo
    - date=today  --> queryString

    - Khi người dùng nhập vào 1 đường dẫn trên trình duyệt nó sẽ được gửi đến WebContainer. WebContainer sẽ quyết đinh Servlet nào sẽ phục vụ yêu cầu từ phía người dùng

    - Tạo Servlet với url pattern có dấu * 
        ```
        @WebServlet(urlPatterns = {"/hello/*"})
        public class testFilter extends HttpServlet {

            @Override
            protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
                resp.setContentType("text/html");

                System.out.println("Vu dZ");

            }
        }
        ```
        - Các url này đều sẽ gọi đến url hello
            - http://localhost:8080/hello/hihi
            - http://localhost:8080/hello/zz
            - http://localhost:8080/hello/kaka

- Forward (Chuyển tiếp)
     -Thường được dùng trong 1 số tình huống : VD như cần vào trang Welcome nhưng bắt login trước thì sẽ chuyển về trang login
     - RequestDispatcher: Ta có 2 cách để lấy ra đối tượng RequestDispatcher
        ```
        Dispatcher dispatcher = req.getServletContext().getRequestDispatcher(url);
        Dispatcher dispatcher = req.getRequestDispatcher(url);
        ```
        - req.getServletContext().getRequestDispatcher(url): Trả về vị trí tương đối với contextPath(Có vị trí tương đối với thư mục gốc của website) :  http://localhost:8080/ServletTutorial
        - req.getRequestDispatcher(url): Vị trí tương đối với trang hiện tại :  http://localhost:8080/ServletTutorial/other/forwardDemo
    
    - Chú ý: 
        - Redirect(Chuyển hướng): Cho phép chuyển hướng đến các trang bao gồm cả trang nằm ngoài website 
        - Forward (Chuyển tiếp) : Chỉ cho phép chuyển đến các trang nằm trong website, đồng thời chuyển dữ liệu 2 trang thông qua request.Attribute 

- Session 
    - Đối tượng HttpSession mô tả phiên làm việc của người dùng 
    - Khi người dùng vào trang web sẽ nhận được id duy nhất để phân biệt với người dùng khác (Id thường được lưu trong cookie hoặc tham số của request)
    - Truy cập vào đối tượng của session
        ```
        protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {

            HttpSession session = request.getSession();
        }
        ```
    - Có thể lưu các giá trị vào đối tượng session và lấy chúng ra, có thể lấy từ trang khác 
        ```
        // Lấy ra đối tượng HttpSession
        HttpSession session = request.getSession();

        // Giả sử người dùng đã login thành công.
        UserInfo loginedInfo = new UserInfo("Tom", "USA", 5);

        // Lưu trữ thông tin người dùng vào 1 thuộc tính (attribute) của Session. 
        // Bạn có thể lấy lại thông tin này bằng phương thức getAttribute.
        session.setAttribute(Constants.SESSION_USER_KEY, loginedInfo);
        ```

    - Lấy ra thông tin đã lưu trữ session ở 1 trang nào đó
        ```
        // Lấy ra đối tượng HttpSession.
        HttpSession session = request.getSession();

        // Lấy ra đối tượng UserInfo đã được lưu vào session
        // sau khi người dùng login thành công.
        UserInfo loginedInfo = (UserInfo) session.getAttribute(Constants.SESSION_USER_KEY);
        ```

## Servlet Filter
- Filter làm được gì 
    - Đôi khi ta chỉ quan niệm là Filter sử dụng để chuyển yêu cầu đến 1 trang khác, hay ngăn chặn truy cập vào 1 trang web nào đó nếu không có quyền hoặc ghi log
    - Thực tế thì Filter dùng để mã hóa(encoding)trang web. VD như set đặt mã hóa UTF-8 cho trang, mở đóng kết nối DB

- Ví dụ servlet-filter
    - Servlet-Filter là 1 class thi hành interface javax.servlet.Filter. Class LogFilter ghi lại thời giạn và đường dẫn yêu cầu gửi tới WebApp
    ```
    public class LogFilter implements Filter {

	public LogFilter() {
	}

	@Override
	public void init(FilterConfig fConfig) throws ServletException {
		System.out.println("LogFilter init!");
	}

	@Override
	public void destroy() {
		System.out.println("LogFilter destroy!");
	}

	@Override
	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
			throws IOException, ServletException {

		HttpServletRequest req = (HttpServletRequest) request;

		String servletPath = req.getServletPath();

		System.out.println("#INFO " + new Date() + " - ServletPath :" + servletPath //
				+ ", URL =" + req.getRequestURL());

		// Cho phép request được đi tiếp. (Vượt qua Filter này).
		chain.doFilter(request, response);
	}

    }
    ```
    - Cần đăng kí đường dẫn đi qua filter trong web.xml
    ```
        <!--Khai báo một filter có tên logFilter-->
    <filter>
        <filter-name>logFilter</filter-name>
        <filter-class>org.o7planning.tutorial.servletfilter.LogFilter</filter-class>
    </filter>

    <!--
    Khai báo các đường dẫn (của trang) sẽ chịu tác dụng của logFilter
    /* có nghĩa là mọi đường dẫn.
    -->
    <filter-mapping>
        <filter-name>logFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
    ```

    - Có thể sử dụng Annotation để cấu hình cho filter

# JSP
## Mối quan hệ giữa JSP và Servlet 
- Ví dụ khi người dùng gửi request -> 1 trang JSP. Ví dụ hello.jsp
    - Lần đầu tiên WebServer sẽ chuyển trang hello.jsp -> hello_jsp.java và dịch nó thành file class hello_java.class. Đây là 1 servlet, nó sẽ tạo ra HTML trả về phía người dùng
    - Từ req thứ 2 trở đi nó sẽ kiểm tra hello.jsp có gì thay đổi không nếu k nó sẽ gọi đến hello_java.class & trả dữ liệu HTML về phía người dùng. Trong trường hợp có thay đổi nó sẽ tạo file hello_jsp.java và biên dịch lại ra file hello_jsp.class
    - Như vậy khi thay đổi file jsp không cần chạy lại server 

## Một số biến có sẵn 
- Khai báo import
    ```
    <!-- Khai báo import -->
    <%@ page import="java.util.*, java.text.*"  %>  

    <%@ page import="java.util.List, java.text.*" %>
    ```

- 1 số biến có sẵn 
    - request: javax.servlet.http.HttpServletRequest
    - response: javax.servlet.http.HttpServletResponse
    - out: javax.servlet.jsp.JspWriter
    ```
        <%
        // Ví dụ sử dụng biến out.
        out.println("<h1>Now is "+ new Date()+"</h1>");
        // Ví dụ sử dụng biến request
        String serverName= request.getServerName(); 
        // Ví dụ sử dụng biến response
        response.sendRedirect("http://eclipse.org");
        %>
    ```

## Viết Java trong HTML 
- Sử dụng <% %>
    ```
    <%@ page import="java.util.Random,java.text.*"%>
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Java In HTML</title>
    </head>
    <body>
    <%
        Random random = new Random();
        // Trả về ngẫu nhiên (0, 1 hoặc 2).
        int randomInt = random.nextInt(3); 
        if (randomInt == 0) {
    %>
    <h1>Random value =<%=randomInt%></h1>
    <%
        } else if (randomInt == 1) {
    %>
    <h2>Random value =<%=randomInt%></h2>
    <%
        } else {
    %>
    <h3>Random value =<%=randomInt%></h3>
    <%
        }
    %>
    <a href="<%= request.getRequestURI() %>">Try Again</a>
    </body>
    </html>
    ```

## Định nghĩa phương thức trong JSP
- Sử dụng <%! %>
- Bản chất  JSP cuối cùng cũng được dịch thành Servlet. Vì thế JSP cũng cho phép tạo ra các method bên trong nó
    ```
    <%!
    public int sum(int a, int b) {
        return a + b;
    }
    %>
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Method in JSP</title>
    </head>
    <body>
    <h1>
        1 + 2 =    <%=sum(1, 2)%>
    </h1>
    </body>
    </html>
    ```

## JSP Directive (Các chỉ thị JSP)
- <%@page ... %>: Dùng để định nghĩa 1 vài thuộc tính như: Error, import, buffet,...
    Vd: Sử dụng thuộc tính errorPage trong Directive <%page ...%>
        ```
        <% @ page errorPage="error.jsp"%>
        ```

- <%@ include ... %>
    - JSP cho phép nhúng nội dung nào đó vào JSP tại thời điểm trang JSP chuyển về Servlet 
    ```
    <!-- Cú pháp -->
    <%@ include file="url" %> 
    <!-- Ví dụ -->
    <%@ include file = "header.html" %> 
    <%@ include file = "footer.html" %> 
    <!-- Bạn cũng có thể nhúng một trang Jsp khác -->
    <%@ include file = "fragment.jsp" %>
    ```

- <%@ taglib .. %>
    - Sử dụng JSP mở rộng hoặc các thẻ tùy biến của bạn sẽ được sử dụng trong trang JSP này
    //TODO: Tìm hiểu về JSP Standard Tag Library(JSTL)

## JSP Standard Actions
- Là các hành động được xây dựng sẵn trong JSP mà không cần phải khai báo TAGLIB thông qua directive(<%@ tablib ...%>)
- 1 số JSP Action:
    - jsp:include ..: Cho phép nhúng file JSP tại thời điểm request. Khác với Directive <%@ include %> nhúng 1 file vào JSP tại thời điểm biên dịch JSP thành servlet 

## JSP Expression Language (Ngôn ngữ biểu thức của JSP)
- Giúp dễ dàng truy cập vào dữ liệu của ứng dụng 

