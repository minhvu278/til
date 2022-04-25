## Spring data jpa
- Những thứ cần làm với spring data jpa
    - Gọi spring data jpa
    - Khai báo mysql connect trong file `pom`

## Các annotation
- `@Controller`: Định nghĩa 1 controller 
- `@RequestMapping(path = "categories")` <=> http:localhost:8080/categories
- Trong phần model 
    - `@Entity`: Cho biết bảng đó tương ứng với bảng nào trong CSDL 
    - `@Table(name = "categories")`: Class đó tương ứng với bảng nào trong DB 
    - `@Id`: Id bảng 
    - `@Column(name = "")`: Sử dụng trong trường hợp tên bảng trong model khác với tên bảng trong DB  
- `@Autowired`: Tự động tìm đến `reponsitory` mà ta khai báo mà không cần khởi tạo nó (Trong trường hợp không thấy thì nó sẽ tự động tạo mới, còn có rồi thì nó sẽ sử dụng lại)

## Truyền dữ liệu từ controller ra view 
- Truyền name = "Zu" vào view 
    ```
    @Controller
    @RequestMapping(path = "categories")
    public class CategoryController {
        @RequestMapping(value = "", method = RequestMethod.GET)
        public String getAllCategories(ModelMap modelMap) {
            modelMap.addAttribute("name", "Zu");
            return "category";
        }
    }
    ```
- Sang bên view in ra thì cần sử dụng thư viện jstl 
    - `${name}`

- Pakage responsetories: Lấy dữ liệu từ CSDL lên 
    - Tạo interface CategoryResponsetory extends từ `CrudResponsitory`