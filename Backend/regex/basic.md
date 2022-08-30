# Characters 
- `/'kí tự muốn match'/g` : Match với các characters
- Vì trong regex có 1 vài kí tự đặc biệt nên  nếu ta muốn lấy thì phải thêm Escape `\`
    ```
    /\./g
    ```

## Character class 
- Muốn match nhiều thì sử dụng `[]`
    ```
    //gray
    //grey
    
    /gr[ae]y/g

- 1 số Special Character đặc biệt 
    - \w: Match với chữ hoặc số & dấu `_` 
    - \W: not word
    - \d: Dạng số 
    - \d+: Các số liền nhau 
    - \D: Những cái không phải là số 
    - \s: Khoảng trắng 
    - \S: not khoảng trắng 
    - \.: Match với tất cả các kí tự nằm trên cùng 1 hàng 
    - \^: Nghịch đảo (Trong character mới có nghĩa như vậy)

## Anchors 
- Đại diện cho 1 số vị trí đặc biệt của string 
    - `^` : Bắt đầu 
    - `$` : Kết thúc
    

