## Collection 
- Là tập hợp các lớp dùng để lưu trữ danh sách và có khả năng tự co dãn khi danh sách đó thay đổi
- Lưu trữ, truy xuất, tương tác với dữ liệu và truyền dữ liệu với các phương thức với nhau 
- Không cần phải khai báo trước số lượng phần tử vì thế hạn chế được về kích thước khi khai báo mảng 

- Interface Collections 
    - List, set, sortedSet, Map, SortedMap

- Class Collection
    - LinkedList
    - ArrayList
    - HashSet
    - TreeSet 
    - HasMap
    - TreeMap 

## List Interface
- Để khai báo 1 list cần dùng đến các class để triển khai nó. Sử dụng phổ biến nhất là `ArrayList` và `LinkedList`
    ```
    public static void main(String[] args) {
        // khai báo List Interface tên listString có kiểu là String
        // và sử dụng Class là ArrayList để triển khai
        // ArrayList là 1 Class Collection
        // các phần tử trong listString cũng có kiểu là String
        List<String> listString = new ArrayList<String>();
                    
        List<Integer> listInteger = new LinkedList<Integer>();
    }
    ```
- Ta cũng có thể khai báo 1 List biết trước số phần tử 
    ```
    public static void main(String[] args) {
        List<Float> listFloat = new ArrayList<Float>(1000);
    }
    ```
- Hiển thị các phần tử có trong list 
    - Sử dụng vòng lặp for
    ```
    public static void main(String[] args) {
        // khai báo List Interface có tên là listString
        // kiểu dữ liệu là String
        List<String> listString = new LinkedList<String>();
            
        // thêm các phần tử
        listString.add("One");
        listString.add("Two");
        listString.add("Three");
        listString.add("Four");
            
        // duyệt theo kích thước của listString
        // và sau đó lấy phần tử tại vị trí thứ i thông qua hàm get()
        // sau đó hiển thị giá trị phần tử đó ra
        for (int i = 0; i < listString.size(); i++) {
            System.out.println(listString.get(i));
        }
    }
    ```

    - Sử dụng forEarch 
    ```
    public static void main(String[] args) {
        // khai báo List Interface có tên là listString
        // kiểu dữ liệu là String
        List<String> listString = new LinkedList<String>();
                
        // thêm các phần tử
        listString.add("One");
        listString.add("Two");
        listString.add("Three");
        listString.add("Four");
                
        // hiển thị các phần tử có trong listString
        // bằng cách sử dụng vòng lặp for duyệt theo đối tượng
        // trong đó kiểu dữ liệu của biến element
        // phải trùng với kiểu dữ liệu của listString
        System.out.println("Các phần tử có trong listString là: ");
        for (String element : listString) {
            System.out.println(element);
        }
    }
    ```
- Thêm phần tử vào List ta sử dụng `add()`
    - Có thể sử dụng add để thêm 1 phần tử vào vị trí bất kì trong danh sách 
    ```
    public static void main(String[] args) {
        List<Float> listFloat = new ArrayList<Float>(1000);
                
        listFloat.add(1.0f);
        listFloat.add(10f);
        listFloat.add(0.02f);
        listFloat.add(10.41f);
        listFloat.add(20.17f);
            
        // thêm phần tử có giá trị 0.5f
        // vào vị trí số 3 trong danh sách listFloat
        listFloat.add(3, 0.5f);
            
        System.out.println("Các phần tử có trong listFloat là: ");
        for (float numberFloat : listFloat) {
            System.out.println(numberFloat);
        }
    }
    ```
- Sử dụng `addAll()` để thêm all các phần tử của 1 List vào cuối danh sách List đã tồn tại 
    - Cũng có thể sử dụng `addAll()` để thêm vào 1 vị trí bất kì trong danh sách 
    ```
    public static void main(String[] args) {
        // khai báo một List Interface có tên là listWord
        // listWord có kiểu là String
        List<String> listWord = new ArrayList<String>();
        listWord.add("Apple");
        listWord.add("Banana");
        listWord.add("Orange");
            
        // khai báo List Interface có tên là listString
        // kiểu dữ liệu là String
        List<String> listString = new ArrayList<String>();
        listString.add("Lemon");
        listString.add("Grape");
                
        // thêm các phần tử của listWord
        // vào vị trí số 1 của listString
        listString.addAll(1, listWord);
            
        System.out.println("Các phần tử có trong listString là: ");
        for (String str : listString) {
            System.out.println(str);
        }
    }
    ```
- Để truy cập đến phần tử bất kì, sử dụng phương thức `get()`
    ```
    public static void main(String[] args) {
        // khai báo List Interface có tên là listString
        // kiểu dữ liệu là String
        List<String> listString = new LinkedList<String>();
                    
        // thêm các phần tử
        listString.add("One");
        listString.add("Two");
        listString.add("Three");
        listString.add("Four");

        System.out.print("Phần tử có chỉ số 2 trong listString là: ");
        String str = listString.get(2);
        System.out.println(str);
    }
    ```
- Cập nhật giá trị của phần tử sử dụng pt set(index, element)
    ```
    public static void main(String[] args) {
        // khai báo List Interface có tên là listString
        // kiểu dữ liệu là String
        List<String> listString = new ArrayList<String>();
            
        // thêm các phần tử
        listString.add("One");
        listString.add("Two");
        listString.add("Three");
        listString.add("Four");
        listString.add("Five");
            
        // cập nhật giá trị của phần tử thứ 2
        // trong listString bằng phương thức set()
        listString.set(2, "Zero");
            
        // hiển thị các phần tử trong listString
        System.out.println("Các phần tử có trong listString là: ");
        for (String stringNumber : listString) {
            System.out.println(stringNumber);
        }
    }
    ```
- Xóa phần tử 
    - Có 2 cách xóa 
        - Xóa theo index của phần tử 
        ```
        listString.remove(0);
        ```

        - Xóa trực tiếp
            - Ví dụ trong List có 2 phần tử giống nhau thì nó sẽ xóa cái đầu tiên trong phần tử 
            ```
            public static void main(String[] args) {
                // khai báo List Interface có tên là listString
                // kiểu dữ liệu là String
                List<String> listString = new ArrayList<String>();
                        
                // thêm các phần tử
                listString.add("One");
                listString.add("Two");
                listString.add("Three");
                listString.add("Four");
                listString.add("Five");
                listString.add("Two");
                        
                // xóa phần tử "Two" khỏi danh sách
                listString.remove("Two");
                    
                System.out.println("Các phần tử của listString sau khi xóa: ");
                for (String str : listString) {
                    System.out.println(str);
                }
            }
            ```

- Tìm kiếm 1 phần tử trong list ta có 3 cách 
    - Tìm kiếm trực tiếp phần tử sử dụng `contains()` - Kết quả trả về true hoặc false 
    ```
    public static void main(String[] args) {
        // khai báo List Interface có tên là listString
        // kiểu dữ liệu là String
        List<String> listString = new ArrayList<String>();
                
        // thêm các phần tử
        listString.add("One");
        listString.add("Two");
        listString.add("Three");
        listString.add("Four");
        listString.add("Five");
        listString.add("Two");
                
        // tìm kiếm phần tử "Six" trong danh sách
        if (listString.contains("Six")) {
            System.out.println("Có phần tử Six trong listString.");
        } else {
            System.out.println("Không tìm thấy phần tử Six.");
        }
    }
    ```
    - Tìm kiếm vị trí xuất hiện đầu tiên của 1 phần tử trong List sử dụng `indexOf()`
    ```
    public static void main(String[] args) {
        // khai báo List Interface có tên là listString
        // kiểu dữ liệu là String
        List<String> listString = new ArrayList<String>();
                
        // thêm các phần tử
        listString.add("One");
        listString.add("Two");
        listString.add("Three");
        listString.add("Four");
        listString.add("Five");
        listString.add("Three");
                
        // tìm kiếm phần tử "Three" trong danh sách
        int firstIndex = listString.indexOf("Three");
        System.out.println("Chỉ số xuất hiện đầu tiên của phần tử Three = " +
            firstIndex); // KQ = 2
    }
    ```
    
    - Tìm kiếm phần tử cuối `lastIndexOf()`

- Sắp xếp phần tử 
    - Sử dụng `Collections.sort()`. Mặc định thì sẽ sắp xếp theo tăng dần 
    ```
    public static void main(String[] args) {
        List<String> listString = new ArrayList<String>();
                
        listString.add("F");
        listString.add("B");
        listString.add("D");
        listString.add("C");
        listString.add("G");
        listString.add("A");
                    
        // sắp xếp các phần tử trong listString
        // sử dụng phương thức Collections().sort()
        Collections.sort(listString);
                
        System.out.println("Các phần tử trong listString sau khi sắp xếp: ");
        for (String str : listString) {
            System.out.println(str);
        }
    }
    ```
- Sao chép List 
    - Để sao chép các phần tử của list này vào list khác sử dụng `Collection.copy()`
    - List đích phải nhiều hơn số phần tử của List sao chép 
    ```
    public static void main(String[] args) {
        // danh sách nguồn
        List<String> listSource = new ArrayList<String>();
            
        listSource.add("A");
        listSource.add("B");
        listSource.add("C");
        listSource.add("D");
            
        // danh sách đích
        // số phần tử của listDest phải lớn hơn hoặc bằng
        // với số phần tử của listSource
        List<String> listDest = new ArrayList<String>();
    
        listDest.add("V");
        listDest.add("W");
        listDest.add("X");
        listDest.add("Y");
        listDest.add("Z");
            
        // sao chép các phần tử của listSource
        // vào trong listDest
        Collections.copy(listDest, listSource);
            
        System.out.println("Các phần tử có trong listDest: ");
        for (String str : listDest) {
            System.out.println(str); // In ra: A B C D Z
        }
    }
    ```
- Hóan đổi các vị trí của phần tử `Collection.shuffle()`
    ```
    public static void main(String[] args) {
        // tạo 1 listNumber có kiểu dữ liệu là Integer
        List<Integer> listNumber = new ArrayList<Integer>();
            
        for (int i = 0; i <= 10; i++) {
            listNumber.add(i);
        }
            
        System.out.println("Các phần tử trong listNumber trước khi hoán vị: ");
        // hiển thị các phần tử trong listNumber ở dạng mảng
        System.out.println(listNumber);
    
        Collections.shuffle(listNumber);
            
        System.out.println("Các phần tử trong listNumber sau khi hoán vị: ");
        System.out.println(listNumber);
    }
    ```

## Set Interface 
- Khác với List, List các phần tử bên trong có thể giống nhau còn Set thì mỗi phần tử là duy nhất 
- Set thì dùng 2 class phổ biến để triển khai đó là `HashSet(Sắp xếp không theo thứ tự)` và `TreeSet(Sắp xếp theo thứ tự tăng dần)`
    ```
    public static void main(String[] args) {
        // khai báo Set Interface tên hashsetInteger
        // và sử dụng Class là HashSet để triển khai
        // HashSet là 1 Class Collection
        // các phần tử trong hashsetInteger cũng có kiểu là Integer
        Set<Integer> hashsetInteger = new HashSet<>();
        hashsetInteger.add(41);
        hashsetInteger.add(1);
        hashsetInteger.add(0);
        hashsetInteger.add(8);
        hashsetInteger.add(1);
        hashsetInteger.add(2);
        hashsetInteger.add(10);
                
        // khai báo Set Interface tên treesetInteger
        // và sử dụng Class là TreeSet để triển khai
        // TreeSet là 1 Class Collection
        // các phần tử trong treesetInteger cũng có kiểu là Integer
        Set<Integer> treesetInteger = new TreeSet<>();
        treesetInteger.add(41);
        treesetInteger.add(1);
        treesetInteger.add(0);
        treesetInteger.add(8);
        treesetInteger.add(1);
        treesetInteger.add(2);
        treesetInteger.add(10);     
            
        System.out.println("Các phần tử có trong hashsetInteger: ");
        System.out.println(hashsetInteger);
        System.out.println("Các phần tử có trong treesetInteger: ");
        System.out.println(treesetInteger);
    }
    ```
- Có thể tạo mới 1 Set thông qua 1 Collection đã tồn tại 
    - Ví dụ tạo mới 1 `Set` từ 1 `List` đã tồn tại 
        ```
        public static void main(String[] args) {
            List<Integer> listInteger = new ArrayList<>();
            listInteger.add(3);
            listInteger.add(10);
            listInteger.add(2);
            listInteger.add(10);
                
            // khai báo 1 Set Interface có kiểu là Integer
            // có các phần tử là các phần tử của listInteger
            Set<Integer> setInteger = new TreeSet<>(listInteger);
            
            // hiển thị setInteger ở dạng mảng
            // trong listInteger có 2 phần tử 10
            // nhưng vì các phần tử trong Set không được giống nhau
            // nên chỉ hiển thị 1 phần tử 10
            System.out.println(setInteger);
        }
        ```
- Thông thường đối với HashSet thì khả năng lưu trữ mặc định là 16 phần tử 
- Tuy nhiên thì ta có thể khai báo số phần tử khi khởi tạo Set đó 
    ```
    public static void main(String[] args) {
        Set<Float> setFloat = new HashSet<>(1000);
    }
    ```
- Những thứ như thêm, sửa xóa thì giống như trong List 

## SortedSet Interface 
- Là 1 dạng riêng của Set 
- Điểm vượt trội hơn so với Set đó là nó có thể sắp xếp theo thứ tự tăng hoặc giảm dần (Mặc định là tăng)

- Để khai báo 1 SortedSet thì cũng cần sử dụng class để triển khai (Sử dụng `TreeSet` vì nó sắp xếp theo chiều tăng dần)
    ```
    public static void main(String[] args) {
        // khai báo SortedSet Interface tên sortedSetString
        // và sử dụng Class là TreeSet để triển khai
        // TreeSet là 1 Class Collection
        // các phần tử trong sortedSetString cũng có kiểu là String
        SortedSet<String> sortedSetString = new TreeSet<String>();
            
        // thêm các phần tử vào trong sortedSetString
        sortedSetString.add("Monday");
        sortedSetString.add("Tuesday");
        sortedSetString.add("Wednesday");
        sortedSetString.add("Thursday");
        sortedSetString.add("Saturday");
        sortedSetString.add("Sunday");
            
        // hiển thị sortedSetString ở dạng mảng
        // các phần tử được sắp xếp tăng dần theo chữ cái đầu tiên
        System.out.println("Các phần tử có trong sortedSetString: ");
        System.out.println(sortedSetString);
    }
    ```
- Trích xuất 1 phần trong SortedSet 
    - Cung cấp 3 phương thức để trích xuất `subset()`, `headset()`, `tailset()`
        - subSet()
            ```
            public static void main(String[] args) {
                List<Integer> listInteger = new ArrayList<>();
                    
                // thêm các phần tử vào trong listInteger
                listInteger.add(2);
                listInteger.add(1);
                listInteger.add(4);
                listInteger.add(3);
                listInteger.add(6);
                listInteger.add(5);
                listInteger.add(8);
                listInteger.add(7);
                listInteger.add(0);
                listInteger.add(9);
                    
                // khai báo 1 SortedSet Interface có kiểu là Integer
                // có các phần tử là các phần tử của listInteger
                SortedSet<Integer> sortedsetInteger = new TreeSet<>(listInteger);
                    
                System.out.println("Các phần tử có trong sortedsetInteger: ");
                System.out.println(sortedsetInteger);
                    
                // khai báo 1 SortedSet có tên là subset
                // có các phần tử được trích xuất 
                // trong đoạn [3,7) của sortedsetInteger
                SortedSet<Integer> subset = sortedsetInteger.subSet(3, 7);
                System.out.println("Các phần tử có trong subset: ");
                System.out.println(subset); // [3, 4, 5, 6]
            
                // nếu phần tử đầu và phần tử cuối bằng nhau
                // thì kết quả của phương thức subSet() 
                // sẽ trả về subset không có phần tử nào
                subset = sortedsetInteger.subSet(3, 3);
                System.out.println("Các phần tử có trong subset: ");
                System.out.println(subset);
            }
            ```

        - headSet(): Trích xuất từ phần tử đầu tiên đến phần tử mong muốn 
            ``` 
            public static void main(String[] args) {
                List<Integer> listInteger = new ArrayList<>();
                    
                // thêm các phần tử vào trong listInteger
                listInteger.add(2);
                listInteger.add(1);
                listInteger.add(4);
                listInteger.add(3);
                listInteger.add(6);
                listInteger.add(5);
                listInteger.add(8);
                listInteger.add(7);
                listInteger.add(0);
                listInteger.add(9);
                    
                // khai báo 1 SortedSet Interface có kiểu là Integer
                // có các phần tử là các phần tử của listInteger
                SortedSet<Integer> sortedsetInteger = new TreeSet<>(listInteger);
                    
                System.out.println("Các phần tử có trong sortedsetInteger: ");
                System.out.println(sortedsetInteger);
                    
                // khai báo 1 SortedSet có tên là headset
                // có các phần tử được trích xuất 
                // từ phần tử đầu tiên đến 
                // phần tử đứng trước phần tử 5 trong sortedsetInteger
                SortedSet<Integer> headset = sortedsetInteger.headSet(5);
                System.out.println("Các phần tử có trong headset: ");
                System.out.println(headset);
            }
            ```
        - tailSet() : Trích từ phần tử mong muốn đến phần tử cuối cùng 
            ```
            SortedSet<Integer> tailset = sortedsetInteger.tailSet(5);
            ```
- Tìm phần tử nhỏ và lớn nhất 
    - Hỗ trợ 2 phương thức first() và last()
        ```
        public static void main(String[] args) {
            List<Integer> listInteger = new ArrayList<>();
                
            // thêm các phần tử vào trong listInteger
            listInteger.add(2);
            listInteger.add(1);
            listInteger.add(4);
            listInteger.add(3);
            listInteger.add(6);
            listInteger.add(5);
            listInteger.add(8);
            listInteger.add(7);
            listInteger.add(0);
            listInteger.add(9);
                
            SortedSet<Integer> sortedsetInteger = new TreeSet<>(listInteger);
                
            System.out.println("Các phần tử có trong sortedsetInteger: ");
            System.out.println(sortedsetInteger);
                
            // tìm phần tử lớn nhất và nhỏ nhất trong sortedsetInteger
            int phanTuLonNhat = sortedsetInteger.last();
            int phanTuNhoNhat = sortedsetInteger.first();
            System.out.println("Phần tử lớn nhất và nhỏ nhất trong"
                + " sortedsetInteger là " + phanTuLonNhat + " và " + phanTuNhoNhat);
        }
        ```

## Map 
- Là tập hợp các cặp key value 
- Các phương thức phổ biến 
    - Sử dụng 3 class cơ bản để triển khai 
        - HasMap: Không theo thứ tự nào cả
        - LinkedHashMap: Thứ tự dựa trên lúc thêm vào 
        - TreeMap: Theo thứ tự tăng dần 
- Tạo mới 1 map interface 
    ```
    public static void main(String[] args) {
        // khai báo Map Interface tên hashMap
        // và sử dụng Class là HashMap để triển khai
        // HashMap là 1 Class Collection
        // mỗi phần tử trong hashMap bao gồm 2 phần
        // key (Integer) và value (String)
        Map<Integer, String> hashMap = new HashMap<>();
            
        // Thêm value vào trong hashMap với key tương ứng 
        // sử dụng phương thức put()
        // đối số thứ nhất trong put là key có kiểu là Integer
        // và đối số thứ hai là value có kiểu là String
        hashMap.put(1, "One");
        hashMap.put(0, "Zero");
        hashMap.put(2, "Two");
        hashMap.put(4, "Four");
        hashMap.put(21, "Twenty first");
        hashMap.put(5, "Five");
    }
    ```

- Lấy toàn bộ các entry(1 entry gồm key value tương ứng với key đó) của map ta sử dụng phương thức `entrySet()`
    ```
    public static void main(String[] args) {
        Map<String, String> mapLanguages = new TreeMap<>();
        mapLanguages.put("CSLT", "Cơ sở lập trình");
        mapLanguages.put("C++", "C++");
        mapLanguages.put("C#", "C Sharp");
        mapLanguages.put("PHP", "PHP");
        mapLanguages.put("Java", "Java");
            
        // tạo 1 Set có tên là setLanguages
        // chứa toàn bộ các entry (vừa key vừa value)
        // của mapLanguages
        Set<Map.Entry<String, String>> setLanguages = mapLanguages.entrySet();
            
        System.out.println("Các entry có trong setLanguages:");
        System.out.println(setLanguages); // In ra dưới dạng key value: C# = C Sharp
    }
    ```
- Ngoài ra kể từ java8 trở đi ta có thể lấy all các entry trong Map bằng cách sử dụng forEarch() như sau 
    ```
    public static void main(String[] args) {
        Map<Character, Integer> mapChar = new TreeMap<>();
        mapChar.put('A', 1);
        mapChar.put('B', 2);
        mapChar.put('C', 3);
        mapChar.put('D', 4);
        mapChar.put('E', 5);
        mapChar.put('F', 6);
            
        // Cách duyệt Map với forEach() trong Java 8
        // đối số thứ nhất bên trong forEach là key
        // đối số thứ hai bên trong forEach là value
        mapChar.forEach((keyChar, valueInt) -> System.out.println(
            "Key = " + keyChar + ", value = " + valueInt));
    }
    ```

- Lấy toàn bộ key của map sử dụng `keySet()`. Pthuc này sẽ trả về 1 set bao gồm các key có trong Map
    ```
    public static void main(String[] args) {
        Map<String, String> mapLanguages = new LinkedHashMap<>();
        mapLanguages.put("CSLT", "Cơ sở lập trình");
        mapLanguages.put("C++", "C++");
        mapLanguages.put("C#", "C Sharp");
        mapLanguages.put("PHP", "PHP");
        mapLanguages.put("Java", "Java");
            
        // phương thức keySet()
        // sẽ trả về 1 Set chứa key có trong Map
        for (String key : mapLanguages.keySet()) {
            System.out.println("Key = " + key);
        }
    }
    ```
- Lấy toàn bộ value thì sử dụng `values()`
    ```
    public static void main(String[] args) {
        Map<String, String> mapLanguages = new LinkedHashMap<>();
        mapLanguages.put("CSLT", "Cơ sở lập trình");
        mapLanguages.put("C++", "C++");
        mapLanguages.put("C#", "C Sharp");
        mapLanguages.put("PHP", "PHP");
        mapLanguages.put("Java", "Java");
        
        // phương thức values() sẽ trả về 
        // một tập hợp gồm các values có trong Map
        for (String value: mapLanguages.values()) {
            System.out.println("Value = " + value);
        }
    }
    ```
- Thêm vào sử dụng `put()`
- Xóa sử dụng `remove(K key)`
- Thay thế 1 value của 1 entry trong Map sử dụng `replace()`
    ```
    public static void main(String[] args) {
        Map<String, String> mapCity = new TreeMap<>();
        mapCity.put("QNg", "Quảng Ngãi");
        mapCity.put("QN", "Quảng Nam");
        mapCity.put("BD", "Bình Định");
        mapCity.put("HCM", "Thành phố Hồ Chí Minh");
            
        System.out.println("Danh sách các thành phố trong mapCity: ");
        Set<Map.Entry<String, String>> setCity = mapCity.entrySet();
        System.out.println(setCity);
            
        // thay thế value của entry có khóa là QN
        // thành Quảng Ninh
        mapCity.replace("QN", "Quảng Ninh");
            
        // ngoài ra chúng ta có thế thay thế như sau
        // câu lệnh bên dưới sẽ thay thế entry 
        // có key là BD, value là Bình Định thành Bình Dương
        mapCity.replace("BD", "Bình Định", "Bình Dương");
            
        System.out.println("Danh sách các thành phố trong mapCity sau khi thay thế: ");
        System.out.println(setCity);
    }
    ```
- Sao chép map sử dụng `putAll()`
    ```
    public static void main(String[] args) {
        Map<String, String> mapCity = new TreeMap<>();
        mapCity.put("QNg", "Quảng Ngãi");
        mapCity.put("QN", "Quảng Nam");
        mapCity.put("BD", "Bình Định");
        mapCity.put("HCM", "Thành phố Hồ Chí Minh");
            
        System.out.println("Danh sách các thành phố trong mapCity: ");
        Set<Map.Entry<String, String>> setCity = mapCity.entrySet();
        System.out.println(setCity);
            
        // tạo 1 Map rỗng
        Map<String, String> mapCityCopy = new TreeMap<>();
    
        // phương thức size() sẽ trả về số lượng entry có trong Map
        System.out.println("Số lượng các entry có trong mapCityCopy "
            + "trước khi sao chép = " + (mapCityCopy.size()));
            
        // sao chép các entry của mapCity
        // vào trong mapCityCopy
        mapCityCopy.putAll(mapCity);
            
        System.out.println("Số lượng các entry có trong mapCityCopy "
            + "sau khi sao chép = " + (mapCityCopy.size()));
        System.out.println("Danh sách các thành phố trong mapCityCopy: ");
        Set<Map.Entry<String, String>> setCityCopy = mapCityCopy.entrySet();
        System.out.println(setCityCopy);
    }
    ```

## SortedMap
- Khác hơn ở Map là các entry có trong sortedMap được sắp xếp tăng dần theo khoá 

## LinkedList
- Các phần tử trong linkedList được sắp xếp theo thứ tự và có thể có giá trị giống nhau 
- Tạo mới 1 LinkedList 
    ```
    public static void main(String[] args) {
        // khai báo 1 danh sách liên kết có tên là linkedList
        // có kiểu là Integer 
        LinkedList<Integer> linkedList = new LinkedList<>();
    }
    ```

## ArrayList
- Cũng khá giống với LinkedList
    ```
    public static void main(String[] args) {
        // khai báo 1 ArrayList có tên là arrListName
        // có kiểu là String và có 10 phần tử
        ArrayList<String> arrListName = new ArrayList<>(10);
    }
    ```
## Khi nào nên dùng ArrayList và LinkedList
- Sử dụng ArrayList nhiều hơn khi cần truy xuất phần tử 
- Sử dụng LinkedList khi cần cập nhật và xoá phần tử 

## HashSet 
- Là class phổ biến nhất của Set nên nó có vài điểm tương đồng với Set 
- Thứ tự phần tử trong `HashSet` không dựa vào lúc thêm vào và giá trị của phần tử là duy nhất 

- Initial capacity và Load factor trong HashSet
    - Note sau
- Tạo mới 1 HashSet
    ```
    public static void main(String[] args) {
        // khai báo 1 HashSet có tên là hashSetInt
        // có kiểu là Integer 
        HashSet<Integer> hashSetInt = new HashSet<>();
            
        // khai báo 1 Hashset có kích thước khởi tạo = 32
        HashSet<Character> hashSetChar = new HashSet<>(32);
            
        // khai báo 1 HashSet có kích thước khởi tạo = 16
        // và yếu tố tải = 0.75f (mặc định)
        HashSet<String> hashSetString = new HashSet<>(16, 0.75f);
            
        // khai báo 1 HashSet được tạo thành từ 1 Collection khác
        HashSet<Float> hashSetFloat = new HashSet<>(new TreeSet<>());
    }
    ```
## TreeSet 
- Là class phổ biến nhất của SortedSet 
- Thứ tự mặc định được sắp xếp tăng dần
- Tạo mới 1 TreeSet 
    ```
    public static void main(String[] args) {
        // khai báo 1 TreeSet có tên là treeSetInteger
        // có kiểu là Integer 
        TreeSet<Integer> treeSetInteger = new TreeSet<>();
            
        // khai báo 1 TreeSet có tên là treeSetCharacter
        // được tạo thành từ 1 Class Collection khác 
        TreeSet<Character> treeSetCharacter = new TreeSet<>(new HashSet<>());
    }
    ```

## HashMap
- Bao gồm 2 phần key value, thứ tự các phần tử không theo thứ tự lúc thêm vào
- Tạo mới 1 HashMap
    ```
    public static void main(String[] args) {
        // khai báo 1 TreeSet có tên là treeSetInteger
        // có kiểu là Integer 
        TreeSet<Integer> treeSetInteger = new TreeSet<>();
            
        // khai báo 1 TreeSet có tên là treeSetCharacter
        // được tạo thành từ 1 Class Collection khác 
        TreeSet<Character> treeSetCharacter = new TreeSet<>(new HashSet<>());
    }
    ```

## TreeMap
- Cũng là lớp triển khai của Map giống như HashMap
- Tuy nhiên thì TreeMap được sắp xếp theo thứ tự tăng dần của khoá 
- Tạo mới TreeMap
    ```
    public static void main(String[] args) {
        // khai báo 1 TreeMap tên treeMap1
        // mỗi phần tử trong treeMap1 bao gồm 2 phần
        // key (String) và value (Double)
        TreeMap<String, Double> treeMap1 = new TreeMap<>();
                
        // khai báo 1 TreeMap được tạo thành từ 1 Map
        Map<Float, Integer> map = new HashMap<>();
        TreeMap<Float, Integer> treeMap2 = new TreeMap<>(map);
    }
    ```

## Hướng đối tượng
- Object (Đối tượng) :  Gồm trạng thái và hành vi 
    - Trạng thái: Gồm những đặc điểm của 1 đối tượng. Vd như sinh viên có : Mã, họ tên, ngày sinh,...
    - Hành vi: Những hành động mà đối tượng thực hiện. Vd sinh viên có hành vi: Đi học, chơi game 

## Tính đóng gói 
- Là sự bảo mật thông tin của mỗi lớp và chỉ được truy xuất thông qua hệ thống các phương thức có sẵn của lớp 
- 1 số đặc điểm
    - Ngăn việc gọi phương thức của lớp này tác động hay truy xuất dữ liệu của đối tượng thuộc về lớp khác 
    - Khi khai báo là private bên ngoài sẽ không thể truy cập được vào
    - Thay đổi cấu trúc bên trong của lớp mà không ảnh hưởng tới những lớp bên ngoài có sử dụng lớp đó 
- Để sử dụng tính đóng gói cần 2 bước 
    - Khai báo là private để các đối tượng không thể truy cập trực tiếp / sửa đổi được 
    - Cung cấp các phương thức get/set để truy cập và sửa đổi giá trị của thuộc tính trong lớp 
    
    ```
    package vidu;
 
    public class Person {
        // khai báo các thuộc tính của đối tượng là private
        private String cmnd;
        private String hoTen;
        
        // tạo các phương thức getter/setter
        // 2 phương thức getCmnd() và getHoTen() là phương thức getter
        // dùng để trả về số chứng minh nhân dân và họ tên của đối tượng
        // và kiểu trả về của hai phương thức này tương ứng với kiểu dữ liệu của thuộc tính
        // 2 phương thức setCmnd() và setHoTen() là phương thức setter
        // dùng để gán giá trị cho thuộc tính chứng minh nhân dân và họ tên của đối tượng
        // trong đó tham số truyền vào của 2 phương thức này được gọi là tham số (biến cục bộ)
        // và có kiểu dữ liệu tương ứng với kiểu dữ liệu của thuộc tính (biến đối tượng)
        public String getCmnd() {
            return cmnd;
        }
        
        // this là từ khóa có ý nghĩa là một tham chiếu đặc biệt 
        // chiếu tới đối tượng chủ của phương thức hiện hành
        // this có thể được dùng để truy cập biến đối tượng (instance variable)
        // hoặc gọi phương thức đối với đối tượng hiện hành. 
        // Thông thường, công dụng này của this chỉ có ích
        // khi tên biến đối tượng bị trùng với tham số (biến cục bộ - local variable) của phương thức 
        public void setCmnd(String cmnd) {
            this.cmnd = cmnd;
        }
        public String getHoTen() {
            return hoTen;
        }
        public void setHoTen(String hoTen) {
            this.hoTen = hoTen;
        }
        
    }
    ```
    - this.hoTen là biến, còn hoTen phía sau là tham số truyền vào  

    ```
    package vidu;
 
    public class TestPerson {
    
        public static void main(String[] args) {
            Person person = new Person();
            
            // gán giá trị họ tên cho đối tượng person vừa tạo thông qua setHoTen() 
            // và gán số chứng minh nhân dân thông qua setCmnd()
            person.setHoTen("Trần Văn Bình");   
            person.setCmnd("212321678");
            
            // truy cập đến tên của đối tượng person thông qua phương thức getHoten()
            // và số chứng minh nhân dân thông qua phương thức getCmnd()
            System.out.println("Tên: " + person.getHoTen() + ", số cmnd: " + person.getCmnd());
        }
    
    }
    ```

## Tính kế thừa 
- Kế thừa các thuộc tính và phương thức của lớp cha 
- Lớp con có thể thêm thuộc tính và phương thức mới của riêng nó hoặc cũng có thể ghi đè phương thức có sẵn 
- Có 3 dạng kế thừa 
    - Kế thừa từ class
    - Kế thừa từ Abstract class
    - Kế thừa từ interface 
- Để kế thừa ta sử dụng từ khóa extends 
- Từ khóa super 
    - Được sử dụng để phân biệt các thành phần có cùng tên giữa lớp cha và con
    - Dùng để gọi hàm tạo của lớp cha từ lớp con
    ```
    package vidu;
 
    public class Superclass {
        int number = 10;
    
        public void hienThi() {
            System.out.println("Đây là phương thức hienThi() của lớp cha");
        }
    }
    ```

    ```
    package vidu;
 
    public class Subclass extends Superclass {
        int number = 20;
    
        public void hienThi() {
            System.out.println("Đây là phương thức hienThi() của lớp con");
        }
        
        public void subclassMethod() {
            Subclass subclass = new Subclass();
            
            // gọi phương thức hienThi() của lớp cha
            // sử dụng từ khóa super()
            super.hienThi();
            
            // gọi phương thức hienThi() của lớp con
            subclass.hienThi();
            
            // hiển thị giá trị biến number của lớp cha
            System.out.println("Giá trị biến number của lớp cha = " + super.number);
            
            // hiển thị giá trị biến number của lớp con
            System.out.println("Giá trị biến number của lớp con = " + subclass.number);
        }
    
    
        public static void main(String[] args) {
            Subclass objSubclass = new Subclass();
            objSubclass.subclassMethod();
        }
    
    }
    ```

## Tính đa hình 
- Hiểu nôm na là trong mỗi trường hợp, hoàn cảnh khác nhau thì đối tượng có các hình thái khác nhau
    - Ví dụ như sinh viên thì đến trường có nhiệm vụ là học, nghe giảng, còn khi vào siêu thị thì đóng vai trò là khách hàng ,...
- Để thể hiện tính đa hình, cần 2 điều kiện : 
    - Các lớp phải có quan hệ kế thừa từ 1 lớp cha nào đó 
    - Phương thức đa hình phải được ghi đè ở lớp con
    - Tính đa hình được thể hiện khi đã ghi đè phương thức của lớp cha 
- Ví dụ: 
    ```
    package vidu;
 
    public class Shape {
        public void show() {
            System.out.println("Đây là phương thức show() của lớp Shape");
        }
    }

    public class Rectangle extends Shape {
        public void show() {
            System.out.println("Đây là phương thức show() của lớp Rectangle");
        }
    }

    public class Square extends Shape {
        public void show() {
            System.out.println("Đây là phương thức show() của lớp Square");
        }
    }

    public class Main {
 
        public static void main(String[] args) {
            Shape shape = new Shape();
            shape.show();   // hiển thị dòng "Đây là phương thức show() của lớp Shape"
            
            // bản chất của shape là Shape, nhưng vì khai báo Rectangle nên chúng ta chỉ nhìn thấy những gì mà Rectangle có
            // vì vậy sẽ chạy những hàm của Rectangle
            shape = new Rectangle();
            shape.show();   // hiển thị dòng "Đây là phương thức show() của lớp Rectangle"
            
            // tương tự lúc này shape sẽ đóng vai trò là 1 Square
            shape = new Square();
            shape.show();   // hiển thị dòng "Đây là phương thức show() của lớp Square"
        }
    
    }
    ```

## Tính trừu tượng 
- Là tính chất không thể hiện cụ thể mà chỉ nêu tên vấn đề 
- Che giấu các hoạt động bên trong và chỉ hiển thị ra những tính năng thiết yếu của đối tượng tới người dùng 
    - Ví dụ như gửi tin nhắn ta chỉ có thể nhập được nội dụng rồi bấm gửi còn quá trình gửi đi thì không nhìn thấy được 
- Ưu điểm 
    - Loại bỏ tính phức tạp của đối tượng và chỉ đưa ra những thuộc tính và phương thức cần thiết 
    - Tập chung vào cốt lõi của đối tượng thay vì cách nó thực hiện 

- Phương thức trừu tượng (Abstract method)
    - Để định nghĩa 1 abstract method cần sử dụng từ khóa `abstract` trước tên phương thức 
    ```
    // khai báo 1 phương thức trừu tượng có tên là khaiBaoPhuongThucTruuTuong()
    // phương thức này có phạm vi truy cập là public
    // và không có đối số truyền vào
    public abstract khaiBaoPhuongThucTruuTuong();
    ```
    - Và để sử dụng được nó thì cần ghi đè (override) nó ở trong lớp con

- Lớp trừu tượng (Abstract Class)
    - Là 1 lớp không thể khởi tạo đối tượng từ nó mà nó sẽ ràng buộc lớp con phải có các phương thức trừu tượng của nó thông qua việc ghi đè 

    - Khai báo lớp trừu tượng 
        ```
        public abstract class AbstractClassDemo {
            public void hienThi() {
                System.out.println("Đây là lớp trừu tượng");
            }
        
            // khai báo 1 phương thức abstract có tên là hienThi()
            // phương thức này không có thân phương thức
            // và có kiểu trả về là void
            public abstract void show();
        }
        ```
    - Ví dụ minh họa
        - Animal
            ```
            public abstract class Animal {
                private String tiengKeu;
                
                public abstract void hienThiTiengKeu();
            }
            ```
        - Dog
            ```
            package vidu;

            public class Dog extends Animal {
            
                @Override
                public void hienThiTiengKeu() {
                    System.out.println("Gâu");
                }
            
            }
            ```
        - Main 
            ```
            package vidu;

            public class Main {
            
                public static void main(String[] args) {
                    Dog dog = new Dog();
                    dog.hienThiTiengKeu();
                }
            
            }
            ```
    - Lớp cha có những phương thức trừu tượng nào thì lớp con cũng phải có 

## Overriding & Overloading
- Quy tắc overriding 
    - Danh sách các đối số phải giống với các phương thức ghi đè 
    - Kiểu trả về phải giống với lớp cha
    - Phương thức được khai báo là final hoặc static thì phương thức không thể ghi đè được 
    - Các hàm tạo của lớp cha cũng không thể ghi đè

- Overloading 
    - Được định nghĩa là nạp chồng phương thức 
    - Lưu ý
        - Không thể thực hiện nạp chồng phương thức chỉ bằng cách thay đổi kiểu trả về của phương thức đó
        - Hàm tạo cũng có thể được overloading

    - Thay đổi tham số truyền vào 
        ```
        public class PhepCongHaiSo {
            public int add(int a, int b) {
                return a + b;
            }
            
            public int add(int a, int b, int c) {
                return a + b + c;
            }
            
        }


        public class TestOverloading {

            public static void main(String[] args) {
                PhepCongHaiSo test = new PhepCongHaiSo();
                System.out.println("Tổng = " + test.add(11, 12));
                System.out.println("Tổng = " + test.add(11, 12, 13));
            }
        
        }
        ```
    - Thay đổi kiểu dữ liệu của đối số truyền vào 
        ```
        public class PhepCongHaiSo {
            public int add(int a, int b) {
                return a + b;
            }
            
            public float add(float a, float b) {
                return a + b;
            }
            
        }

        public class TestOverloading {

            public static void main(String[] args) {
                PhepCongHaiSo test = new PhepCongHaiSo();
                System.out.println("Tổng = " + test.add(11, 12));
                System.out.println("Tổng = " + test.add(11.1f, 12.2f));
            }
        
        }

        ```

    - Thay đổi trình tự kiểu dữ liệu của các đối số 
        ```
        public class DisplayOverloading {

            public void hienThi(int a, char b) {
                System.out.println(a + "\t" + b);
            }
            
            public void hienThi(char b, int a) {
                System.out.println(b + "\t" + a);
            }
        }

        public class TestOverloading {
        
            public static void main(String[] args) {
                DisplayOverloading displayOverloading = new DisplayOverloading();
                displayOverloading.hienThi(5, 'a');
                displayOverloading.hienThi('a', 5);
            }
        
        }
        ```
    - Ngoài ra trong trường hợp ta chưa xác định đối số cần truyền vào thì có 1 cách nâng cao như sau
        ```
        public class AdvancedOverloadMethod {
            // Dấu ... là quy tắc tạo Parameter List
            // ...x lúc này là một mảng một chiều linh động 
            // tức là nó tự động co giãn được đối với các đối số truyền vào.
            public int fn4(int ...x) {
                int sum = 0;
            
                // duyệt qua từng phần tử trong mảng một chiều x
                for (int i : x) {
                    sum += i;
                }
                return sum;
            }
        }
        ```
        ```
        public class TestAdvancedOverloadMethod {
        
            public static void main(String[] args) {
                AdvancedOverloadMethod demo = new AdvancedOverloadMethod();
                System.out.println(demo.fn4(1, 2, 3));
                System.out.println(demo.fn4(1, 2, 3, 4));
            }
        
        }
        ```
- Khi nào sử dụng 
    - Overriding sử dụng khi trong cùng 1 phương thức, ta muốn thay đổi phần thân của nos
    - Overloading sử dụng khi trong cùng 1 phương thức ta muốn làm thêm 1 công việc khác 
    
## Static 
- Static chủ yếu dùng để quản lý bộ nhớ 
- Thuộc về lớp chứ k thuộc về các đối tượng tạo ra từ lớp  
- Đặc điểm chung các thành phần được khai báo static 
    - Được cấp phát 1 lần duy nhất ngay khi biên dịch chương trình 
    - Có thể dùng chung cho mọi đối tượng 
    - Được truy xuất trực tiếp từ tên lớp mà không phải khởi tạo đối tượng của lớp đó 
    - Được hủy khi kết thúc chương trình 
- Biến tĩnh, thuộc tính tĩnh 
    - Là biến dùng chung cho mọi đối tượng thuộc lớp 
    - Biến tĩnh cũng tương tự như hằng nhưng linh hoạt hơn do biến tĩnh có thể thay đổi giá trị khi cần thiết 
    - Cú pháp 
        ```
        [access modifier] static [kiểu dữ liệu] tenBien = [giá trị khởi tạo];
        ```
        - Biến được truy xuất trực tiếp từ tên lớp 
        ```
        [Tên_lớp].[Tên_thuộc_tính];
        ```

    - VD: 
        ```
        package example_static;

        public class StaticVariable {
        
            int nonStaticVariable = 10;
            static int staticVariable = 100;    // khai báo biến tĩnh và khởi tạo giá trị
            
            public int getNonStaticVariable() {
                return nonStaticVariable;
            }
        
            public void setNonStaticVariable(int nonStaticVariable) {
                this.nonStaticVariable = nonStaticVariable;
            }
        
            public static void main(String[] args) {
                StaticVariable demo = new StaticVariable();
                System.out.println("Giá trị biến nonStaticVariable = " + demo.getNonStaticVariable());
                
                // truy cập thuộc tính tĩnh
                System.out.println("Giá trị biến staticVariable = " + StaticVariable.staticVariable);
            }
            
        }
        ```

## Interface 
- Là 1 kiểu tham chiếu tương tự như class nhưng có thể chứa các hằng số và tên phương thức không có phần thân 
- 1 lớp thì mô tả các thuộc tính và hành động của đối tượng còn interface thì mô tả hành động của lớp đó 
- Interface không thể đưọc theo lớp mà chỉ có thể được mở rộng từ các lớp khác hoặc kế thừa từ interface khác 
- Ngoại trừ lớp trừu tượng thì all các lớp mở rộng interface phải định nghĩa lại all các phương thức của interface 

- Khai báo 
    - 1 interface có thể được kế thừa từ nhiều interface khac  (Lớp thì mỗi lớp chỉ kế thừa đc 1 lớp)
    ```
    package vidu;
    
    public interface Interface {
    
        // Đây là phương thức trừu tượng
        // phương thức trừu tượng của Interface không cần khai báo từ khóa abstract và public
        void createAbstractMethod();
    }

## Đa luồng 
- 1 chương trình được gọi là đa luồng khi ctrinh đó có 2 luồng trở lên chạy song song với nhau 
- Luồng gồm 4 phần chính 


## Exception 
- Là 1 sự kiện xảy ra 