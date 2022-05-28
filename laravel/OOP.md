## OOP
- Class mô tả hành động, trạng thái của đối tượng đó
    ```
    class sinhVien {
        // Class này đại diên cho đối tượng sinh viên
    }
    ```
- Thuộc tính của lớp 
    - VD class sinhVien gồm có: Tên, tuổi 
        ```
        class sinhVien {
            var $ten;
            var $tuoi;
        }
        ```
- Phương thức là những hành động của đối tượng đó ví dụ như động vật ăn, chạy, ngủ
    ```
    class DongVat {
        var $mat;
        var $mui;
        var $chan;

        // Phương thức 
        function an($thuc_an) {

        }

        function chay() {

        }
    }
    ```

- Khởi tạo và gán 
    - Cần phân biết được khởi tạo đối tuợng và khai báo đối tượng 
        - Khai báo là tạo ra 1 class của đối tượng đó 
        - Khởi tạo là tạo 1 hình tượng của lớp mà ta đã khai báo. Cú pháp `$ten_bien = new ClassName();`
    ```
    class DongVat {
        var $mat;
        var $mui;
        var $chan;

        // Phương thức 
        function an($thuc_an) {

        }

        function chay() {

        }
    }
    // Khởi tạo lớp động vật mới 
    $conheo = new DongVat();
    $conlon = new DongVat();
    ```

- Truy xuất đến các thuộc tính của đối tượng 
    - Sử dụng `->` . `$className->method`
    ```
    $conheo = new DongVat($thuc_an);

    // Gán giá trị cho thuộc tính
    $conheo->mat = 'Mắt to';
    $conheo->mui = 'Mui lợn';

    echo $conheo->mat;
    ```

- Gọi các phương thức của đối tượng
    - Ta cũng dùng `->` . `$className->function()`
    ```
    class DongVat {
        function an($thuc_an) {
            echo 'Hôm nay ănl' . $thuc_an;
        }
    }

    $conheo->an('Cam');
    ```

## Kế thừa trong PHP 
- Đơn giản chỉ là lớp con kế thừa lớp cha 
- Gọi các phương thức và thuộc tính của lớp cha
    - Gọi bên trong lớp con 
        - Sử dụng từ khóa $this->thuoctinh, $this->phuongthuc 
        - Tuy nhiên để phân biệt được hàm nào hàm cha, hàm nào hàm con thì ta sử dụng từ khóa `parent::thuoctinh`
        ```
        class DongVat
        {
            // Thuộc tính
            var $mat = '';
            var $mui = '';
        
            // Phương Thức
            function an()
            {
                echo 'Dong Vat Dang An';
            }
        }
        
        // Lớp Con Trâu
        class ConTrau extends DongVat
        {
            function gioi_thieu()
            {
                $this->mat = 'Đây là cái mặt';
                $this->mui = 'Đây là cái mũi';
                parent::an(); // xuất ra chuỗi "Động Vật Đang Ăn"
            }
        }

        $contrau = new ConTrau();

        // Gọi đến hàm gioi_thieu trong lớp Con Trâu
        // nên xuất ra màn hình chuỗi "Động Vật Đang Ăn"
        $contrau->gioi_thieu();

        // Trong hàm giới thiệu có gán giá trị cho 2
        // thuộc tính mắt và mũi, giờ ta xuất ra màn hình
        // xem giá trị nó là gì

        echo $contrau->mat;
        echo $contrau->mui;
        ```

## Các mức độ truy cập 
- Private : Chỉ dành cho nội bộ lớp 
    - Tránh truy cập từ bên ngoài 
    - Có những hàm SET và GET để lấy dữ liệu 
    ```
    class Xe
    {
        private $loaixe;
    
        function getLoaixe()
        {
            return $this->loaixe;
        }
    
        function setLoaixe($loaixe)
        {
            $this->loaixe = $loaixe;
        }
    }
    
    // Khởi tạo một lớp đối tượng xe
    $xe = new Xe();
    
    // Gán giá trị cho thuộc tính loại xe
    // nhưng sai tại vì loaixe đang ở mức private
    // nên không thể truy xuất bên ngoài
    $xe->loaixe = 'Wave S';
    
    // Lấy giá trị thuộc tính loại xe
    // cũng sai vì loaixe là private
    echo $xe->loaixe;
    ```
- Protected : Truy xuất nội bộ trong lớp và lớp kế thừa 
    - Bên ngoài không truy cập được
    - Thường dùng cho những phương thức và thuộc tính có khả năng bị lớp con định nghĩa lại 
        ```
        class Xe
        {
            protected $loaixe;
        }
        
        // Kế thừa từ lớp xe
        class XeHonda extends Xe
        {
            function hienThiThongTin()
            {
                // Lệnh này đúng vì loaixe đang ở
                // mức protected nên nó được kế thừa
                $this->loaixe = 'Wave S';
            }
            protected function suaChuaXe()
            {
                // Lệnh
            }
        }
        
        // ------------------//
        // Chuong Trình Chính//
        // ------------------//
        
        $honda = new XeHonda();
        
        // Lệnh này sai vì loaixe đang
        // ở mức protected nên ở bên ngoài lớp
        // không được truy xuất vào
        $honda->loaixe = 'Wave Tàu';
        
        // Lệnh này đúng
        $honda->hienThiThongTin();
        
        // Lệnh này sai vì: function suaChuaXe đang
        // ở mức protected nên ko thể truy xuất
        // từ ngoài lớp XeHonDa
        $honda->suaChuaXe();
        ```

## Tính đa hình 
- Là sự đa hình của mỗi hành động cụ thể của mỗi đối tượng khác nhau 
    - Ví dụ như hành động ăn của của động vật hoàn toàn khác nhau (Lợn ăn cám, bò ăn cỏ,...)
- Còn sự đa hình trong lập trình thì được hiểu là lớp con sẽ viết lại các phương thức của lớp cha (ovewrite)
    
## Abstract 
- Giống với tính kế thừa theo bề ngoài. 
- Lớp abstract sẽ định nghĩa lại các phương thức mà từ đó lớp con sẽ kế thừa và overwrite lại 
- Không được khai báo ở mức private 
- Lớp abstract có thể có thuộc tính nhưng thuộc tính không được khai báo là abstract 
    ```php
    // Đúng
    public $name;
  
    // Sai vì các thuộc tính không được để ở dạng abstract
    abstract public $title;
    ```

- Không thể khởi tạo 1 biến của lớp Abstract 
    ```php
    abstract class BaseClass
    {
        abstract protected function hello();
    }
      
    // Sai vì BaseClass là lớp Abstract nên không
    // khởi tạo mới được
    $base = new BaseClass();
    ```

    ```
    // Đúng
    public $name;
  
    // Sai vì các thuộc tính không được để ở dạng abstract
    abstract public $title;


- Khai báo lớp abstract 
    ```php
    abstract class BaseClass
    {
        // phương thức ở mức protected
        abstract protected function hello();
    }
    ```

- Hàm và lớp final 
    - Lớp final là lớp được khai báo là lớp cuối cùng, không lớp nào có thể kế thừa lại nó 
    - Tương tự như hàm Final trong abstract hoặc trong kế thừa chỉ để gọi sử dụng không được overwrite lại 

## Interface 
- Là 1 template 


### Interface không phải là lớp cụ thể mà là khuôn mẫu cụ thể cho 1 đối tượng implement nó. Còn abstract là 1 lớp cụ thể có đầy đủ các tính chất của 1 đối tượng 
