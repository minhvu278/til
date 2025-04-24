# Creating REST API requests with Postman
## Postman Collections

- Có thể tạo collection để chia các API khác nhau riêng đỡ bị lẫn lộn

## Storing configuration in collection variables

- Chúng ta sẽ đặt variable trong collection cho các đường dẫn trùng lặp như url để nếu sau này có thay đổi thì ta không cần phải sửa tay tất cả những request khác
- Lưu ý rằng nếu không trong collection mà vẫn sử dụng variable đã tạo trong collection thì sẽ bị lỗi

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9a9d30aa-4822-4cd2-ade5-57a403553962/1eacc56e-8d3d-45be-ab50-4e35fa53cfc4/image.png)

- Và để sửa variable thì chúng ta sẽ vào edit của colllection
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9a9d30aa-4822-4cd2-ade5-57a403553962/2fabf2a3-4f41-45f5-94e5-66f2528e6502/image.png)
    
    - Initial value là giá trị khởi tạo ban đầu - mục đích là để share collection, còn current value sẽ là giá trị chúng ta sử dụng thực (sẽ sửa ở current)
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9a9d30aa-4822-4cd2-ade5-57a403553962/2b27e13a-2c99-4fc1-8752-568e5a275145/image.png)
    

## QUIZ3

- Một số lợi ích của việc sử dụng bộ sưu tập Postman là gì?
    - Để sắp xếp và nhóm các yêu cầu API liên quan.     x
    - Để theo dõi số lượng yêu cầu API bạn đã thực hiện hôm nay
    - Để cung cấp mã hóa hai đầu cho các yêu cầu API
    - Để tăng tốc độ thực thi yêu cầu API
    - Tất cả những điều trên Không có điều nào ở trên
- Lý do nào sau đây là hợp lý cho việc sử dụng biến trong Postman?
    - Để sử dụng lại các giá trị chung trong các yêu cầu của Người đưa thư.
    - Để lưu trữ thông tin nhạy cảm như mật khẩu hoặc khóa API.
    - Để giảm việc nhập thủ công và lỗi chính tả.
    - Tất cả những điều trên.     x
    - Không có điều nào ở trên.
- Bạn muốn sử dụng biến Postman có tên productionURL làm giá trị cho URL cơ sở trong một trong các yêu cầu Postman của bạn. Bạn nên sử dụng cú pháp nào?
    - {productionURL}
    - {{ProductIONURL}}
    - {{productionUrl}}
    - $productionURL {
    - {productionURL}}     x
    - ${{productionURL}}
- Yêu cầu của bạn không hoạt động. Bạn mở bảng điều khiển Postman để hiểu chuyện gì đang xảy ra.
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9a9d30aa-4822-4cd2-ade5-57a403553962/59feb1d1-ae08-4a67-a63e-9ab850cf02c7/image.png)
    
- Bạn có thể rút ra kết luận nào từ thông tin này?
    - API đang ngoại tuyến hoặc đang được bảo trì.
    - Máy chủ DNS không thể truy cập được.
    - Không thể tìm thấy điểm cuối và máy chủ đã trả về 404 Không tìm thấy.
    - Tường lửa hoặc phần mềm chống vi-rút đang chặn yêu cầu.
    - Không thể giải quyết biến Postman được sử dụng trong yêu cầu.    x
    - Chứng chỉ SSL không hợp lệ.
    - Phiên bản Postman bạn sử dụng đã lỗi thời
- Bạn đã cấu hình biến bộ sưu tập Postman như hiển thị bên dưới:
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9a9d30aa-4822-4cd2-ade5-57a403553962/e05f950b-3b13-4967-9615-53ced7787633/image.png)
    
- Giá trị nào sẽ được Postman sử dụng khi gửi yêu cầu nếu bạn bao gồm biến username trong yêu cầu được lưu trong cùng một bộ sưu tập?
    - username
    - defaultuser
    - INITIAL VALUE
    - CURRENT VALUE
    - jamiesmith     x
    - Biến sẽ không được giải quyết.
- Bạn muốn xóa biến bộ sưu tập Postman khỏi bộ sưu tập của mình. Làm thế nào bạn có thể làm điều đó?
    - Chỉnh sửa bộ sưu tập và từ tab "Biến", hãy xóa biến.     x
    - Xóa biến khỏi tất cả các yêu cầu.
    - Nhấp chuột phải vào biến trong bất kỳ yêu cầu nào và chọn "Xóa" từ menu ngữ cảnh
- Điều gì xảy ra khi bạn xóa biến bộ sưu tập Postman đang được tham chiếu trong yêu cầu?
    - Biến bị xóa nhưng yêu cầu vẫn hoạt động.
    - Biến sẽ bị xóa và yêu cầu rất có thể sẽ không thành công.    x
    - Biến không bị xóa. Người đưa thư sẽ ngăn bạn xóa một biến nếu nó vẫn đang được sử dụng.

## GET request

- URL viết tắt của Uniform Resource Locator, vì vậy nói cách khác, nó là một cách để định vị tài nguyên. Danh sách sản phẩm này là tài nguyên mà chúng tôi có thể tìm thấy vì chúng tôi có ở đây đúng URL, đúng địa chỉ

## Visualizing responses in Postman

- Pretty: Trông sẽ đẹp hơn
- Raw: Dạng JSON thô nên khó đọc hơn
- Preview: Dạng xem trước không phải kiểu JSON

## Query parameters

- Query parameters sẽ bắt đầu sau dấu hỏi chấm: `{{baseUrl}}/products?category=milk`
- Và khi nếu không muốn truy vấn nữa thì chúng ta chỉ cần bỏ tích phần category đi là nó sẽ mất ở trên Url mà không cần xoá thủ công
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9a9d30aa-4822-4cd2-ade5-57a403553962/859f8527-9adc-46d5-9421-3a7929242f79/image.png)
    
- Và hãy lưu ý rằng với việc hoa thường sẽ cho ra kết quả khác nhau
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9a9d30aa-4822-4cd2-ade5-57a403553962/edbd32c1-bead-45cf-8d03-8372f1f076bb/image.png)
    
- Như ở đây category là không required nên khi viết là `Category` nó sẽ lấy ra danh sách products và bỏ qua Category

## QUIZ 4: Query parameters

- Điểm cuối trong API REST là gì?
    - Một địa chỉ (URL) cụ thể đóng vai trò là điểm vào để tương tác với một tài nguyên hoặc tập hợp tài nguyên cụ thể.     x
    - Một tập hợp các hướng dẫn được xác định trước về cách khách hàng (như Postman) nên tương tác với API.
    - Một cách để gửi và truy xuất dữ liệu bằng định dạng JSON.
    - Tất cả những điều trên.
- Thông thường khi sử dụng API, các tham số truy vấn phân biệt chữ hoa chữ thường.
    - True.      x
    - False
- Thuật ngữ "resource" đề cập đến điều gì trong ngữ cảnh của API REST và Người đưa thư?
    - Điểm cuối nơi thực hiện các yêu cầu API.
    - Một đối tượng dữ liệu (ví dụ: sản phẩm, khách hàng, đơn đặt hàng) hoặc tập hợp các đối tượng dữ liệu (ví dụ: danh sách khách hàng) có sẵn để truy xuất hoặc thao tác thông qua API.        x
    - Máy chủ hoặc cơ sở hạ tầng đám mây mà API đang chạy trên đó.
    - Tất cả những điều trên
- Bằng cách sử dụng điểm cuối /products của API Cửa hàng tạp hóa đơn giản, bạn muốn nhận tất cả các sản phẩm sữa và trứng. Bạn sẽ tiếp cận tình huống này như thế nào?
    - Gửi hai yêu cầu riêng biệt tới API, một yêu cầu cho mỗi danh mục sản phẩm. Các yêu cầu được sử dụng sẽ là: /products?category=dairy /products?category=eggs                          x
    - Gửi một yêu cầu duy nhất tới API với cả hai danh mục sản phẩm. Các yêu cầu được sử dụng sẽ là: /products?category=dairy&category=eggs
    - Gửi một yêu cầu duy nhất tới API với cả hai danh mục sản phẩm. Các yêu cầu được sử dụng sẽ là: /products?category[]=dairy&category[]=eggs
    - Gửi một yêu cầu duy nhất tới API với cả hai danh mục sản phẩm. Các yêu cầu được sử dụng sẽ là: /products?category=dairy,Eggs
    - Tất cả những yêu cầu trên.
- Bạn đang gửi yêu cầu có tham số truy vấn và API phản hồi bằng mã trạng thái sau: `404 Bad Request`. Bạn sẽ làm gì tiếp theo?
    - Gửi lại yêu cầu tương tự vì đây có thể là sự cố tạm thời với máy chủ.
    - Xác minh điểm cuối để đảm bảo nó được viết chính xác.
    - Kiểm tra nội dung phản hồi để tìm bất kỳ lỗi hoặc gợi ý nào khiến yêu cầu không thành công.     x
    - Hãy thử một giá trị khác cho tham số truy vấn bạn đã sử dụng.
- API [example.com](http://example.com/) chấp nhận tham số truy vấn tùy chọn có tên là Ngôn ngữ và cho phép các giá trị phân biệt chữ hoa chữ thường sau: en, fr, de, it. Máy khách gọi URL sau: [`https://example.com/api/orders?language=DE`](https://example.com/api/orders?language=DE) . API nhận được giá trị nào cho tham số truy vấn có tên là Ngôn ngữ?
    - 400 Yêu cầu không hợp lệ.
    - Không có giá trị nào được đặt cho tham số truy vấn Ngôn ngữ.      x
    - DE
    - de
    - Tham số truy vấn Ngôn ngữ chứa giá trị không hợp lệ.
- Câu nào sau đây mô tả đúng nhất yêu cầu đối với tham số truy vấn HTTP trong API REST?
    - Nếu tài liệu điểm cuối đề cập đến chúng thì chúng là bắt buộc và phải được đưa vào yêu cầu.
    - Chúng luôn là tùy chọn và có thể được bỏ qua nếu không cần thiết.
    - Yêu cầu đối với các tham số truy vấn khác nhau tùy thuộc vào điểm cuối API được gọi      x
    - Không có mục nào ở trên.
- Nội dung phản hồi được mã hóa JSON sau đây biểu diễn điều gì? `[]`
    - Cơ sở dữ liệu API trống và không chứa dữ liệu.
    - Danh sách trống.
    - Chỉ ra rằng các tham số truy vấn không hợp lệ đã được gửi.
    - Mã trạng thái 400 Yêu cầu không hợp lệ.
- Nếu bạn gọi điểm cuối /available-tools của API, bạn sẽ nhận được danh sách các công cụ sau:
    
    ```jsx
    [
        {
            "id": 4643,
            "category": "plumbing",
            "name": "PEX Clamp Tool",
        },
        {
            "id": 1225,
            "category": "power-tools",
            "name": "1/2 in. Brushless Hammer Drill",
        },
        {
            "id": 2177,
            "category": "ladders",
            "name": "Cosco Three Step Steel Platform",
        },
        {
            "id": 6543,
            "category": "electric-generators",
            "name": "GENMAX 3200 Watt Inverter Generator",
        },
        ...
    ]
    
    ```
    
- Bạn sẽ làm gì tiếp theo nếu chỉ quan tâm đến các công cụ thuộc danh mục "plumbing"?
    - Sửa đổi điểm cuối API và chuyển tham số truy vấn danh mục: /available-tools?category=plumbing
    - Nghiên cứu tài liệu API để xem liệu có cách nào lọc kết quả bằng cách chỉ định một danh mục hay không.       x
    - Sửa đổi điểm cuối API và chuyển tham số truy vấn Category : /available-tools?Category=plumbing
- Điểm cuối /products của API Simple Grocery Store hỗ trợ tham số truy vấn có tên là available (là giá trị boolean, nghĩa là chỉ chấp nhận giá trị true hoặc false). Tuy nhiên, trong nội dung phản hồi, tính khả dụng của sản phẩm được chỉ ra bằng thuộc tính inStock:
    
    ```jsx
    [
        {
            "id": 4643,
            "category": "coffee",
            "name": "Starbucks Coffee Variety Pack, 100% Arabica",
            "inStock": true
        },
        ...
    ]
    ```
    
- Điều này có nghĩa là gì?
    - Bạn có thể sử dụng khóa tham số truy vấn available hoặc inStock .
    - Bạn chỉ có thể sử dụng khóa tham số truy vấn available .    x
    - Bạn chỉ có thể sử dụng khóa tham số truy vấn inStock .
- Bạn đang gửi yêu cầu với Postman và API phản hồi bằng mã trạng thái sau: `404 Not Found` . Bạn sẽ làm gì tiếp theo?
    - Gửi lại yêu cầu tương tự vì đây có thể là sự cố tạm thời với máy chủ.
    - Kiểm tra nội dung phản hồi để tìm bất kỳ lỗi hoặc gợi ý nào khiến yêu cầu không thành công.
    - Tham khảo tài liệu API và xác nhận rằng điểm cuối API đã được viết chính xác.   x

## Path variables

- https://github.com/vdespa/Postman-Complete-Guide-API-Testing/blob/main/simple-grocery-store-api.md#Get-a-product
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9a9d30aa-4822-4cd2-ade5-57a403553962/e4aae159-64a3-4eb3-b5cf-1a7f131ddc98/image.png)
    
- Để lấy được id của 1 sản phẩm, chúng ta sử dụng path variables để làm tham số truy vấn. Lưu ý là nó sử dụng `:` và phải cần nhập value vào nếu không khi send sẽ gửi url là `:productId`

## Query params vs Path variables

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9a9d30aa-4822-4cd2-ade5-57a403553962/381ebb47-adfc-47b9-bdf5-bcca4ec35fbc/image.png)

## QUIZ 6: Path variables

- Câu nào sau đây mô tả đúng nhất mục đích của việc sử dụng các biến đường dẫn trong điểm cuối API REST?
    - Để lọc kết quả theo một tham số cụ thể.
    - Để chỉ định một mã định danh duy nhất cho một tài nguyên     x
    - Để chỉ định phương thức yêu cầu HTTP được sử dụng.
    - Để chỉ định định dạng mong muốn cho nội dung phản hồi (JSON, XML, HTML)
- Sau đây là ví dụ về cách sử dụng điểm cuối cụ thể của API. Kiểm tra URL và xác định biến đường dẫn. https://api.vdespa.com/profiles/jamie
    - vdespa, profiles, jamie
    - api, profiles, jamie
    - profiles, jamie
    - jamie   x
    - :jamie
- Điểm khác biệt giữa tham số truy vấn và biến đường dẫn là gì?
    - Các biến đường dẫn là một phần của đường dẫn và luôn bắt buộc. Các tham số truy vấn có thể là tùy chọn hoặc bắt buộc.    x
    - Các tham số truy vấn là một phần của đường dẫn và luôn bắt buộc. Các biến đường dẫn có thể là tùy chọn hoặc bắt buộc.
    - Các tham số truy vấn là một phần của đường dẫn và luôn bắt buộc. Các biến đường dẫn luôn là tùy chọn.
    - Các biến đường dẫn là một phần của đường dẫn và luôn bắt buộc. Các tham số truy vấn luôn là tùy chọn.
- Bạn đang gọi điểm cuối /products/:productId của API Simple Grocery Store nhưng bạn nhận được mã trạng thái 400 Yêu cầu không hợp lệ.
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9a9d30aa-4822-4cd2-ade5-57a403553962/99ac5605-e0ee-46fe-8604-90ffa3f0c8aa/image.png)
    
- Nguyên nhân có thể xảy ra nhất cho việc này là gì?
    - Yêu cầu không chỉ định giá trị cho biến đường dẫn ProductId.
    - URL chứa các ký tự đặc biệt không mong muốn (dấu cách).
    - Điểm cuối không chính xác và không thể tìm thấy tài nguyên.
    - Yêu cầu không chỉ định giá trị cho tham số truy vấn ProductId.
- Sau đây là ví dụ về cách sử dụng điểm cuối cụ thể của API. Kiểm tra URL và xác định các biến đường dẫn. `https://api.example.com/users/jamie/lists/6xlglibyla?fields=all
    - jamie, 6xlglibyla     x
    - jamie, 6xlglibyla, fields
    - jamie, 6xlglibyla, all
    - users, lists, fields
    - jamie

## POST request

- Để tạo mới, chúng ta sẽ sử dụng POST, đổi method từ GET → POST trong postman

## JSON format explained

- Lý do sử dụng JSON là để chuyển đổi dữ liệu. Ví dụ, chúng ta có các hệ thống khác nhau và chúng cần giao tiếp với nhau. Hầu hết sẽ sử dụng JSON để làm điều đó coi như là 1 quy ước chung
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9a9d30aa-4822-4cd2-ade5-57a403553962/c424e28d-7d27-4cc0-8a10-cedad2185231/image.png)
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9a9d30aa-4822-4cd2-ade5-57a403553962/df2ee91f-ace3-4210-b4cb-4950e5560061/image.png)
    
- Hãy bắt đầu thực hành thêm item
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9a9d30aa-4822-4cd2-ade5-57a403553962/91519bef-e454-4d99-be3c-9f66f34a6831/image.png)
  