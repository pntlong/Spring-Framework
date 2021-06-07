# 1. Mock
**Mock Object** (MO) là một đối tượng ảo, mô phỏng các tính chất và hành vi giống hệt như đối tượng thực. Được truyền vào bên trong khối, mã để kiểm tra tính đúng đắn của các hoạt động bên trong.
* Đơn giản hơn đối tượng thực nhưng vẫn giữ được sự tương tác với các đối tượng khác.
* Không lặp lại nội dung đối tượng thực.
* Cho phép thiết lập các trạng thái riêng trợ giúp cho việc thực hiện unit test.

**Ứng dụng**
* Đối tượng thật có những hành vi không đoán trước được.
* Đối tượng thật khó cài đặt.
* Đối tượng thật chậm.
* Đối tượng thật có / là giao diện người dùng.
* Đối tượng thật không tồn tại.

# 2. Unit Test
**Unit test** là một loại kiểm thử phần mềm trong đó các đơn vị hay thành phần riêng lẻ của phần mềm được kiểm thử

* Được thực hiện trong quá trình phát triển ứng dụng.

* Cô lập một phần code và xác minh tính chính xác của đơn vị đó

* Một unit bao gồm: function, procedure, class, method

**Các trạng thái cơ bản**
* Fail (trạng thái lỗi)
* Ignore (tạm ngừng thực hiện)
* Pass (trạng thái làm việc)

**Ứng dụng**
* Tạo môi trường để kiểm tra bất kỳ đoạn code nào.
* Phát hiện thuật toán thực thi không hiệu quả
* Phát hiện vấn đề thiết kế, xử lý hệ thống..
* Phát hiện các lỗi nghiêm trọng có thể xảy ra trong những tình huống hẹp

```
@Test
public void testSum(){
    Assert.assertEquals(3, MathUtil.sum(1,2));
}
```

# 3. Intergration test
**Kiểm thử tích hợp (Integration testing)** là một giai đoạn trong kiểm thử phần mềm. Mỗi module phần mềm riêng biệt được kết hợp lại và kiểm thử theo nhóm.

**Cần thực hiện intergration test**

* Một Module nói chung được thiết kế bởi một lập trình viên có hiểu biết và logic lập trình có thể khác với các lập trình viên khác. Kiểm thử tích hợp là cần thiết để đảm bảo tính hợp nhất của phần mềm.
* Tại thời điểm phát triển module vẫn có thể có thay đổi trong yều cầu của khách hàng, những thay đổi này có thể không được kiểm tra ở giai đoạn unit test trước đó.
* Giao diện và cơ sở dữ liệu của các module có thể chưa hoàn chỉnh khi được ghép lại.
* Khi tích hợp hệ thống các module có thể không tương thích với cấu hình chung của hệ thống.
* Thiếu các xử lý ngoại lệ có thể xảy ra.