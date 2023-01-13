# 1 số lý do nên học TypeScript
- Javascript và TypeScript là 2 trường phái mà hay đấu đá với nhau không phải do conflict mà là do có những người viết code JS thoải mái quen khi chuyển sang TypeScript thì nó bị gò bó nên sẽ ghét.
- Còn 1 số người bắt đầu từ các ngôn ngữ rất strict về kiểu dữ liệu thì lại rất thích TypeScript.
- Vậy thì khi nào nên sử dụng JS, khi nào nên sử dụng TS thì hãy đọc bài viết dưới đây để có thể hiểu hơn về khi nào cần sử dụng thằng nào và cách cài đặt và sử dụng của nó nhé
# TypeScript là gì?
- TypeScript là một dự án mã nguồn mở được phát triển bởi Microsoft
- Được coi là một phiên bản nâng cao của Javascript bởi việc bổ sung tùy chọn kiểu tĩnh và lớp hướng đối tượng mà điều này không có ở Javascript
- **Javascript is TypeScript**: JS trong hiện tại và tương lai đều có trong TS cộng thêm 1 số tính năng nữa mà TS cung cấp cho JS hiện tại - Vì thế nên là nếu biết JS thì cũng có thể code được TS
## So sánh Javascript và TypeScript 
- Tùy thuộc vào cá nhân (như đã chia sẻ ở phần trên) hoặc hoàn cảnh thì sẽ chọn
- **Javascript**
    - Linh hoạt - Không bị ràng buộc dữ liệu (Biến đó là kiểu dữ liệu gì cũng được)
    - Không cần định nghĩa kiểu dữ liệu hoặc tìm kiếm kiểu dữ liệu khi sử dụng libs
    - Code nhanh khi làm 1 mình
    - Cần hiểu rõ về JS để tránh các lỗi vặt
- `Đi nhanh lúc đầu và càng về sau càng tốn efforts`
- **TypeScript**
    - Gặp khó khăn lúc đầu với type system vì sẽ gặp lỗi liên quan đến kiểu dữ liệu
    - Có nhắc code, đỡ bị lỗi vặt (Như sai chính tả)
    - Khá chậm lúc đầu khi phải tìm hiểu kiểu dữ liệu để khai báo
    - Code team thì được lợi nhiều từ việc auto complete (Gợi ý code khi gõ)
- `Chậm lúc đầu và sẽ nhanh và an toàn hơn cho những lần sau`
## Làm thế nào để thực thi được file TypeScript
- Đối với JS thì có thể chạy bằng node hay trên trình duyệt, tuy nhiên thì thằng TS này không chạy như thế được. Để thực thi được thì cần 1 thằng ở giữa biến đổi TS thành JS (Khá giống với thư viện babel dùng để chuyển đổi sang JSX).
- Để chạy được thì cần cài thư viện cho project (Có thể chọn cài local hoặc global - Nếu test thử thì nên cài trên local để tránh bị conflict)
    ```js
    # Yarn
    yarn global add typescript ts-node ts-lib @types/node
    # Npm
    npm i -g typescript ts-node ts-lib @types/node
    // Locally
    npm i -D typescript ts-node ts-lib @types/node
    ```
    - **typescript**:  Có thằng typescript compiler, giúp chuyển đổi TS -> JS
    - **ts-node**:  Nó là node dành cho TS
- Ví dụ tạo thử 1 file index.ts như sau:
    - Cách này sẽ dùng thằng tsc compile để compile thằng index.ts -> index.js
    ![alt](./image/ts-compile.png)
    - Cách nhanh hơn thì có thể sử dụng ts-node (Đỡ phải compile :v)
    ![alt](./image/ts-node.png)
- Lưu ý là phải compile sang js nhé: Trong trường hợp nếu chỉ có code js thì ok nó vẫn sẽ chạy mà không cần phải compile. Nhưng như trên vd có sử dụng `const channelName: string = "Bae"` mà không compile thì nó sẽ bị lỗi
![alt](./image/error-ts.png)
## Set-up unit test với ts-jest
- Đầu tiên thì cần khởi tạo project
    ```js
    npm init
    ```
    ![alt](./image/init.png)
    - Cái nào điền sẵn rồi thì chỉ cần enter, 1 số chỗ cần điền là description, test command, license - Và còn bước yes no nữa thì cứ mạnh dạn ấn yes nhé
- Chạy xong thì nó sẽ tạo cho 1 file pakage.json
    ![alt](./image/pakage.png)
- Cần cài thêm:
    ```
    npm install --save-dev jest typescript ts-jest @types/jest
    ```
- Tạo các config mặc định của thằng jest
    ```js
    npx ts-jest config:init
    ```
- Tạo tsconfig.json
    ```
    tsc --init
    ```
- 1 file test thường sẽ có dạng như này
    ![alt](./image/ts-test.png)
# Static type checking
- Type script giúp phát hiện lỗi ngay trong lúc code (Js thì phải chạy lên thì mới biết được lỗi ở đâu)
- Tránh lỗi typo
- Tiết kiệm được thời gian debug
- Chỉ cần hover vào là sẽ hiển thị lỗi
    ![alt](./image/err-str.png)
- Trong trường hợp không nhớ trong object có gì thì nó sẽ tự nhắc
    ![alt](./image/auto-complete.png)
- tsc - typescript compiler
- Ta có thể sử dụng được tsc sau khi cài typescript
    ```js
    npm i -g typescript
    ```
    - Sử dụng tsc -> compiler toàn bộ code trong project hiện tại
    - Sử dụng tsc tenfile.ts -> Chỉ compiler mình file này
- Khi có lỗi sẽ không cho nó compiler ra thì cần đặt flag **noEmitOnError: true** trong tsconfig.json
## Một số kiểu dữ liệu cơ bản
- Explicit types: Khai báo kiểu tường minh
    ```js
    let count: number = 123;
    let studentName: string = 'Alice';
    let isActive: boolean = true;
    const numberList: number[] = [1, 2, 3];
    ```
- Infered types: Có thể hiểu được kiểu dữ liệu tương ứng mà không cần khai báo kiểu dữ liệu cụ thể
    ```js
    let count = 123;
    ```
    - Thường thì ta nên dùng cách này, tuy nhiên trong các trường hợp biến phức tạp thì cần khai báo rõ kiểu dữ liệu
- Eraised types
    - Khi compiler từ TS -> js thì những thứ liên quan đến kiểu dữ liệu sẽ bị bỏ
# Các kiểu dữ liệu thường gặp
- Các kiểu dữ liệu bạn đã biết bên Javascript
    - Primitive: number, boolean, string, null, undefined, symbol
    - Reference: array, object, function
- Còn bên type sẽ gặp các kiểu như: any, void,...
- VD về any:
![alt](./image/assign.png)
- Khi chạy đoạn code này bên Js thì sẽ vẫn chạy được bình thường nhưng bên TS thì nó sẽ vẫn đang hiểu thằng *count* là số nên trong trường hợp mà vẫn muốn gán thì có thể sử dụng thằng **any**
    ![alt](./image/any.png)
- Tuy nhiên thì chỉ nên sử dụng any trong trường hợp mới chuyển từ js sang để nó work với code hiện tại rồi đổi dần sang TS(Nếu dùng any thì code luôn JS chứ k cần chuyển sang TS làm gì)
## Literal types
- Chỉ định một giá trị cụ thể làm kiểu dữ liệu
    ```js
    let count: 1;
    let name: 'Bae';
    ```
    - Khi khai báo như này thì nó chỉ nhận đúng giá trị đó thôi
    - Nó vẫn sẽ là tập hợp của kiểu dữ liệu đó. Vd như count: 1 thì nó vẫn là tập hợp của number
- Còn nếu sử dụng const
    ```js
    const count: 1
    ```
    - Nó sẽ nhận 1 là kiểu dữ liệu luôn (k phải là number như let)
- Đối với object
    ```js
    const student = {
        id: 1,
        name: 'Easy',
    }
    student.name = 'Typescript is easy! :P';
    ```
    - Tuy là sử dụng const nhưng mà các phần tử bên trong vẫn có thể thay đổi được. Vì thế các phần tử bên trong nó vẫn sẽ hiểu là tập hợp kiểu dữ liệu
    -Trong trường hợp mà không muốn sửa thì có 1 tips nhỏ đó là thêm **as const**. Khi hover vào nó sẽ chỉ hiện lên là `readonly` chỉ cho đọc chứ k cập nhật lại được giá trị
        ```js
        const student = {
            id: 1,
            name: 'Easy',
        } as const
        student.name = 'Typescript is easy! :P';
        ```
    ![alt](./image/readonly.png)

# 1 số lưu ý khi làm việc với function
## Về return type
- Ta hoàn toàn có thể chỉ định cho hàm đó giá trị trả về là gì 
    - Trường hợp không có return: Nó sẽ hiểu bạn trả về kiểu dữ liệu là **void**(Không trả về cái gì cả)
    ```js
    function sayHello() {
    console.log('Hello bae');
    }
    // function sayHello(): void
    ```
    - Định nghĩa kiểu trả về: 
    ```js
    function sum(a: number, b: number): number {
        return a + b;
    }
    ```
## Optional and default parameter
- Optional parameter
    - Sử dụng **?** để chỉ định tham số đó truyền hoặc không truyền - Trường hợp không truyền thì nó sẽ là undefined
    ```js 
    // function getLength(numberList?: number[] | undefined): number
    function getLength(numberList?: number[]) {
        return Array.isArray(numberList) ? numberList.length : 0;
    }
    ```
- Default parameter
    - Trường hợp mà không truyền vào thì sẽ lấy 1 giá trị nào đó làm giá trị mặc định 
    ```js
    // function getLength(numberList?: number[]): number
    function getLength(numberList: number[] = []) {
        return Array.isArray(numberList) ? numberList.length : 0;
    }
    ```
# Enum trong Typscript 
- Là 1 nhóm các kiểu dữ liệu gom lại thành 1 nhóm để có thể dễ dàng truy xuất hơn. 
    - Ví dụ như tập hợp màu sắc, thay vì viết 1 hẳng số cho màu xanh, 1 hằng số cho màu đỏ thì ta có thể gom lại thành 1 enum để có thể **color.red, color.green** - Rất tiện mà gọn hơn nhiều đúng không :v
- Khai báo và sử dụng enum
    - Có thể gán bất kì số nào cho biến enum
    ```js 
    enum Status {
    PENDING, // 0
    IN_PROGRESS, // 1
    DONE, // 2
    CANCELLED, // 3
    }
    
    const stats1: Status = Status.PENDING;
    const stats2: Status = 1;
    const stats3: Status = -1;
    ```
    - Có hỗ trợ reverse mapping: Có thể lấy chiều nào cũng được 
    ```js 
    enum Status {
    PENDING, // 0
    IN_PROGRESS, // 1
    DONE, // 2
    CANCELLED, // 3
    }

    console.log(Status[0]); // 'PENDING'
    console.log(Status['DONE']); // 2
    ```
