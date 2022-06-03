# Dependency Injection 
- Là 1 mô hình lập trình tổ chức code sao cho các đoạn code, modul khác nhau các lớp không phụ thuộc vào nhau 1 cách cứng nhắc mà cần có 1 cơ chế thay đổi các thành phần phụ thuộc vào cả thời điểm chạy và biên dịch 
- Giải quyết vấn đề trong các project lớn sẽ có nhiều thành phần phụ thuộc vào nhau 

- VD: Tạo 2 lớp
    - `StockItem` biểu diễn mặt hàng trong kho 
    - `Product` : Mặt hàng bán trên web liên quan đến lưu trữ trong kho 
    
    ```php
    <?php

    class StockItem {

        private $quantity;
        private $status;

        public function __construct($quantity, $status){
            $this->quantity = $quantity;
            $this->status   = $status;
        }

        public function getQuantity(){
            return $this->quantity;
        }

        public function getStatus(){
            return $this->status;
        }

    }
    ```

    ```php
    <?php
    class Product {
        private $stockItem;
        private $code;

        public function __construct($code, $stockQuantity, $stockStatus){
            $this->stockItem  = new StockItem($stockQuantity, $stockStatus);
            $this->code        = $code;
        }

        public function getStockItem(){
            return $this->stockItem;
        }

        public function getCode(){
            return $this->code;
        }
    }

    $product = new Product("101010", 50, "Áo Dài");
    var_dump($product->getStockItem());
    ```
- Sử dụng DI 
    ```php
    <?php
    class Product {
        private $stockItem;
        private $code;

        public function __construct($code, StockItem $stockItem){
            $this->stockItem   = $stockItem;
            $this->code        = $code;
        }

        public function getStockItem(){
            return $this->stockItem;
        }

        public function getCode(){
            return $this->code;
        }
    }

    $stockItem = new StockItem(50, "Áo Dài");
    $product = new Product("101010", $stockItem);
    var_dump($product->getStockItem());
    ```
    - Đối tượng `StockItem` không còn khởi tạo bên trong constructor `Product` mà nó được truyền vào `Product` thông qua chính đối tượng `StockItem` vì thế khi thay đổi cách khởi tạo `StockItem`