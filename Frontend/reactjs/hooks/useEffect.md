# useEffect
## Hook này ra đời để làm gì? Dùng nó khi nào 
- Dùng khi muốn thực hiện các side effect 
    - Side effect: Khi có tác động xảy ra dẫn đến dữ liệu của chương trình bị thay đổi
    - Tạo ra sự thay đổi dữ liệu bên cạnh hoạt động chính 
- Giúp Update DOM, Call Api, Listen DOM events, remove listener/unsucribe, clear timer

## Các kiểu useEffect
- useEffect(callback)
    - Gọi callback mỗi khi component re-render
    - Gọi callback sau khi component thêm element vào DOM 
        - Khi view xử lý tạo ra DOM element & thêm vào trong DOM sau đó mới chạy đến callback của useEffect
        - Tuy nhiên thì code vẫn được chạy từ trên xuống (Chạy xong cất callback đi và gọi lại khi DOM được xử lý xong)
    - Call API 
- useEffect(callback, [])
    - Chỉ gọi callback 1 lần sau khi component mounted
    - Sử dụng khi muốn thực hiện logic gì đó 1 lần sau khi component được mounted và không muốn gọi lại khi component re-render
- useEffect(callback, [deps])
    - deps đơn giản nó là biến - Có thể là props truyền từ ngoài vào, là state trong component 
        - Nói chung thì nó là biến chứa 1 giá trị dữ liệu 
    - Callback sẽ được gọi lại mỗi khi deps thay đổi 
        - Khi component re-render -> useEffect sẽ kiểm tra deps trước và sau khi render có khác nhau không -> Nếu khác nhau sẽ gọi lại callback 
    - Vậy thì làm sao để kiểm tra được deps trước và sau có thay đổi hay không 
        - Nó sử dụng toán tử `===` nếu khác nhau sẽ gọi lại callback

- `Cả 3 trường hợp trên`
    - Callback luôn được gọi khi component mounted
    - CleanUp function luôn được gọi trước khi component được unmount
    - CleanUp function luôn được gọi trước khi callback được gọi (Trừ lần component được mounted)
        - Trước khi gọi callback mới thì sẽ dọn dẹp các phần trước đó
        ```js
        return () => {
            //Code
        }
        ```

# useEffect with DOM 
- Cách listen DOM event component 
- Vấn đề xảy ra khi listen DOM event 