> https://wanago.io/2020/08/03/api-nestjs-uploading-public-files-to-amazon-s3/
# Uploading public files to Amazon S3
- Mặc dù việc lưu trữ file trong DB là khả thi, nhưng đây có thể không phải là cách tiếp cận tốt nhất. Các file có thể chiếm nhiều dung lượng và có thể ảnh hưởng đến hiệu suất của ứng dụng. Ngoài ra nó làm tăng kích thước của CSDL và do đó, làm cho việc sao lưu lớn hơn và chậm hơn. Một giải pháp thay thế tốt là lưu file riêng biệt bằng nhà cung cấp bên ngoài, chẳng hạn như Google Cloud, Azure hoặc Amazon AWS

# Connectiong to Amazon S3
- Amazon S3 cung cấp dung lượng lưu trữ mà chúng ta có thể sử dụng với bất kỳ loại file nào. Chúng ta sắp xếp các file thành nhóm và quản lý chúng trong API của chúng tôi thông qua SDK
- Sau khi tạo tài khoản AWS, chúng ta có thể đăng nhập với tư cách là người dùng root. Mặc dù chúng ta có thể cấp quyền cho root để sử dụng S3 thông qua API của mình, nhưng đây không phải là cách tốt nhất

## Setting up a user
- Hãy tạo 1 user mới có quyền hạn hạn chế. Để thực hiện, chúng ta cần mở bảng `Identity and Access Management (IAM) và tạo user