# Part 1 : Fundamentals (Các nguyên tắc cơ bản)
- Chương 1: Tóm tắt những thay đổi của java
- Chương 2: 
- Chương 3: Giải thích đầy đủ cùng ví dụ của các khái niệm về lambda expression (Giống như arrow function trong js) và phương pháp tham chiếu 


## Java 8, 9, 10, 11
- Chap này gồm: 
    - Tại sao java lại tiếp tục thay đổi 
    - Thay đổi nền tảng máy tính 
    - Áp lực để thay đổi
    - Giới thiệu các tính năng cốt lõi mới của java 8 & 9z

- Big story
    - Java 8 thay đổi sâu sắc nhất (Java 9 thêm nhiều tính năng quan trọng nhưng k sâu sắc ).
    - Những thay đổi cho phép viết code dễ dàng hơn
        ```
        VD: Thay vì viết mã dài dòng 

        Collections.sort(inventory, new Comparator<Apple>() {
            public int compare(Apple a1, Apple a2){
                return a1.getWeight().compareTo(a2.getWeight());
            }
        });

        -- Có thể viết ngắn gọn bằng Java 8
        inventory.sort(comparing(Apple::getWeight));
        ```

    - Java 8 cung cấp API mới (gọi là luồng) 

- Kiem tra port dang chay   
    lsof -i tcp:8080


# Chap 2: Passing code with behavior parameterization
 