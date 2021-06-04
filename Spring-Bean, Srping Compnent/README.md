# 1. Spring Bean
Các đối tượng tạo thành xương sống của ứng dụng và được quản lý bởi Spring IoC container được gọi là **Bean**. Một bean là một đối tượng được khởi tạo, lắp ráp, và được quản lý bởi một Spring IoC container. Các bean này được tạo ra bằng siêu dữ liệu cấu hình mà bạn cung cấp cho container, ví dụ dưới dạng định nghĩa `XML <bean/>`.

# 2. Spring Component
Là một class-level annotation. Nó yêu cầu Spring sử dụng class này để tạo một bean nếu có nơi nào khác sử dụng class này như một dependency. Việc khởi tạo class hoàn toàn do Spring kiểm soát và chỉ một bean được tạo cho mỗi class.
```
@Component
class UserService {
    public void updateUser(User user) {
    …
    }
}
```
Khi Spring start thì nó sẽ quét các class được đánh dấu Component thì nó sẽ tạo bean
