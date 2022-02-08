# Note
## web.xml
- Để mặc định khi vào ứng dụng nó chạy vào trang nào luôn thì sử dụng `welcome-file-list`
    ```
    <welcome-file-list>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>    
    ```

## pom.xml
- 1 số thứ như version dùng chung thì ta có thể khai báo trong `properties` để có thể thay thế cho nhiều chỗ 
    ```
    <properties>
        <spring-version>2.0</spring-version>
    </properties>

    <!-- Sử dụng lại -->
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>jsp-api</artifactId>
      <version>${spring-version}</version>
    </dependency>
    ```

## Connect DB
- Add thư viện mysql vào file pom 
    ```
    <!-- mysql-connector-java -->
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>5.1.45</version>
    </dependency>
    ```
- Tiếp theo là dùng `Class.forName("com.mysql.jbdc.Driver");`
    ```
    public Connection getConnection() {
        try {
            Class.forName("com.mysql.jbdc.Driver");
            String url = "jdbc:mysql://45.252.251.17:3306/lniiftlt_vu";
            String username = "lniiftlt_minhvu";
            String password = "minhvu@123";
            return DriverManager.getConnection(url, username, password);
        } catch (ClassNotFoundException | SQLException e) {
            return null;
        }
    }
    ```
- Cơ chế của jdbc là nó sẽ execute 1 câu SQL. Để thực thi đc trong java ta sử dụng `PrepareStatement`
    ```
    String sql = "SELECT * FROM category";
        Connection connection = getConnection();
        PreparedStatement statement = null;

        if (connection != null) {
            try {
                statement = connection.prepareStatement(sql);
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    ```
    - Khi PrepareStatement thực thi câu query để lấy dữ liệu lên nó sẽ k trả về 1 kiểu dữ liệu cụ thể, nó sẽ trả về 1 đối tượng là `ResultSet `
        ```
        ResultSet resultSet = null;

        if (connection != null) {
            try {
                statement = connection.prepareStatement(sql);
                resultSet = statement.executeQuery(); // Lúc này mới được thực thi
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        ```
    - `ResultSet` nó như là 1 table tất cả dữ liệu sẽ đổ vào nó 
    - finally: Chạy xong hết tất cả mới bắt đầu chạy vào finally 

- Context Dependency injection(CDI) - Sử dụng java servlet weld  

## Connect Database jdbc 
- Đầu tiên cần tạo connection 
    - Để tạo connection thì cần load Class.forName để load driver `Class.forName("com.mysql.jbdc.Driver");`
    - Để sử dụng đc Class.forName thì add thư viện mysql vào file pom.xml 
- Để thực thi được câu lệnh sql thì ta cần sử dụng đối tương PrepareStatement 
    ```
    PreparedStatement statement = null;
    ```
    - Và khi trả về nó sẽ k trả về 1 đối tượng cụ thể nào cả mà nó sẽ trả về ResultSet

## Statement & Preparestatement khác gì nhau 
- Để sử dụng các câu sql thì cần dùng 2 cái trên 
- PrepareStatement thì có thể truyền tham số vào được `cat_id`
    ```
     String sql = "SELECT * FROM news WHERE cat_id = ?";
     ```
- Statement sẽ k support truyền tham số trực tiếp vào 

## Generic 
- Dùng khi cần viết các hàm chung 
- T là khi bên kia truyền vào gì thì bên này nhận là cái ấy
    ```
    public interface GenericDAO<T> {
        <T>List<T>
    }
    ```
- Object... parameters: Co the truyen bao nhieu tham so cung duoc
- Tạo mapper: 

## Bean.xml
- Quản lý đối tượng cho dependency này 
- Nó sẽ tạo ra 1 container 
    - Khi request đầu tiên vào VD `newService = new NewService()` nó sẽ khởi tạo vào trong container
    - Request thứ 2 vào nó sẽ kiểm tra nếu tồn tại newService rồi thì nó sẽ lấy ra dùng còn k thì nó sẽ khởi tạo mới

## JDBC transaction 
- Khi thao tác dữ liệu(CRUD)  JDBC sẽ cũng cấp 1 transaction
- Cũng có open transaction & close
- Commit & rollback 
    - Khi tất cả các transaction success thì lúc đó ta sẽ commit tất cả dữ liệu (Khi commit thì dữ liệu mới được ghi xuống DB)
    - Rollback khi 1 trong những cái success mà bị fails thì sẽ không cho commit & sẽ revert lại all 