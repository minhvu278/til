## 1 số khái niệm cơ bản 
- Black box testing: 
    - Khi thực hiện việc test không quan tâm đến quá trình xử lý
    - Chỉ quan tâm đến đầu vào và mong muốn đầu ra như thế nào 

- While box testing 
    - Cần biết được logic bên trong nó xử lý như nào (Đọc code của dev)

- Unit testing: Dev viết và test trước khi bàn giao cho test 
- Integration testing: Test tích hợp
    - Ví dụ có 2 modul A B thì phải đảm bảo ghép với nhau sẽ không bị lỗi 
    
- System testing: Test hệ thống để xem có phù hợp với các hệ thống khác không hay là có hoạt động tốt không

## Quy trình testing tổng quát 
- Planning Testing ->  Analysis & Design ->  Execute Testing  -> Test Report

## Phân tích yêu cầu dự án 
- Input: 
    - SRS document QA viết 
    - Design 
    - Other document 
- Output:
    - Q&A list

## Viết testcase
- Tại sao phải viết test case 
    - Positive testcase - Test tích cực 
    - Negative testcase - Test tiêu cực

## Các loại báo cáo 
- Daily report - Báo cáo hàng ngày 
- Weekly report - Báo cáo hằng tuần
- Intergration report - Báo cáo việc test tích hợp của dự án trước khi bàn giao sản phẩm


## Tester manual 
- Kiểm thử phần mềm là gì 
    - Là quá trình thực hiện kiểm tra chương trình phần mềm với mục đích 
        - Tìm lỗi phần mềm 
        - Chứng minh phần mền hoạt động đúng 

- Lí do phải kiểm thử phần mềm 
    - Bug có thể gây ra nhiều vấn đề nghiêm trọng
    - Vì thế kiểm thử để tìm bugs -> đảm bảo chất lượng của sản phẩm -> Tăng độ tin tưởng và hài lòng của khách hàng 

- 7 nguyên lí cơ bản của kiểm thử 
    - Kiểm thử toàn bộ là không thể: 
        - Thay vì kiểm thử toàn bộ ta sẽ dựa vào độ ưu tiên(priorties), đánh giá rủi ro(risks)
        - Sử dụng kĩ thuật thiết kế test phù hợp kiểm thử 
    
    - Cụm lỗi (defect clustering)
        - Nguyên lý Pareto (80-20 Rule): 
            - 80% lỗi tập chung ở 20% modul 
            - 20% effort của mình tìm được 80% lỗi dự án

    - Thuốc trừ sâu (Pesticide paradox)
        - Không thể lặp đi lặp lại 1 bộ dữ liệu test vì sẽ k tìm ra được lỗi mới 
        - Cần phải cập nhât thường xuyên để tìm ra lỗi mới 

    - Kiểm thử chỉ hiện ra lỗi chứ không chứng minh được phần mềm zero bugs
    
    - Kiểm thử không chỉ tìm ra các lỗi mà còn kiểm tra phần mềm có đáp ứng nhu cầu nghiệp vụ không

    - Kiểm thử sớm (Early testing)
        - Lỗi được phát hiện sớm sẽ có chi phí sửa lỗi thấp hơn

    - Kiểm thử phụ thuộc vào ngữ cảnh
        - Cách tiếp cận, phương pháp, kĩ thuật và các loại kiểm thử tùy thuộc vào ứng dụng 

- Quy trình kiểm thử phần mềm
    - Test planning & control  -> Test Analysis & Design  -> Test Implementation & Execution  -> Evaluating Exit criteria & reporting  -> Test Closure Activities
        - Test planning & control (Lập kế hoạch và kiểm soát)
            - Planning 
                - Xác định phạm vi, rủi ro và muc đích kiểm thử 
                - Phương pháp kiểm thử
                - Tài nguyên kiểm thử: Con người, môi trường,...
                - Lên kế hoạch phân tích kiểm thử, thiết kế kiểm thử, thực hiện kiểm thử và đánh giá 
                - Xác định điều kiện kết thúc 
            - Control 
                - So sánh tiến độ thực tế so với kế hoạch đồng thời đưa ra được các hành động cần thiết để đáp ứng mục tiêu và nhiệm vụ của dự án 
        - Test Analysis & Design (Phân tích và thiết kế) 
            - Dựa vào test basic: Bao gồm tài liệu thiết kế ES, Q&A của khách hàng 

        - Test Implementation & Execution (Hoàn thiện và thực hiện kiểm thử)
            - Hoàn thiện testcase và điền pass hay fail  

        - Evaluating Exit criteria & reporting (Đánh giá điều kiện kết thúc và báo cáo)
            - Evaluating Exit criteria: là quá trình đánh giá xem lúc nào dừng việc test 
            - Evaluating Exit criteria được thực hiện khi: 
                - 1 lượng lớn test case được thực hiện với tỉ lệ % pass nhất định 
                - Tỉ lệ lỗi dưới mức nhất định
                - Khi đến deadlines

        - Test Closure Activities: Các hoạt động kết thúc việc kiểm thử được thực hiện khi phần mềm sẵn sàng được chuyển giao  